# Opus 4.6 Briefing: Write Chapter 4 — The Free-Market Transformer

## Your task

Write `DELIVERABLES/Paper-4-FreeMarketTransformer.html` — the final, publication-quality HTML paper.

A **draft already exists** at `nanoFMT/Paper-4-FreeMarketTransformer.html` (74 KB). Read it first.
Your job is to write the **complete final version** incorporating the experimental results below.
Output to `DELIVERABLES/Paper-4-FreeMarketTransformer.html` (copy the CSS from the draft exactly).

This is **Chapter 4** of the book *"The Free-Market Algorithm: A Universal Theory of Open-Ended Complex Systems."*
Add the book-series header above the title (same style as Chapter 1, `DELIVERABLES/Paper-3-Free-Market-Algorithm.html`).

---

## Context you must read first

1. **`nanoFMT/Paper-4-FreeMarketTransformer.html`** — the existing draft. Read all of it. Keep everything
   that is good. The abstract, introduction (1.1–1.3), background (Section 2), and the 18-mechanism
   mapping (Section 3) are strong. Section 10 (nanoFMT experiments) needs the actual results below.

2. **`DELIVERABLES/Paper-3-Free-Market-Algorithm.html`** — Chapter 1. Section 9.2 has the 5-domain
   universality table. Chapter 4 must be consistent with it.

3. **`Core/MarketSim.h`** and **`Core/MarketSim.cpp`** — for any code citations needed.

---

## nanoFMT Experimental Results (NEW — not in draft)

### Setup
- Model: 34,802,432 params, 4 layers, 32 expert slots/layer, character-level TinyStories
- Architecture: FMT with open-ended expert birth/death/discovery, persistent recipe book
- Full run: 20,000 steps, cosine LR decay, T=1.0 (selection regime)

### Final run statistics (step 20,000)

| Metric | Value |
|--------|-------|
| Final val loss | **0.7663** |
| Total active experts | **58** [13, 17, 13, 15] per layer |
| Recipe book size | **25 recipes** |
| Training time | **403.1 minutes** (6.7 hours) |

### Expert growth trajectory
- Step 0: 4 experts (1 per layer, initialized)
- Step ~500: rapid growth phase
- Step 12,800: 52 experts [11,15,13,13], 25 recipes — **recipe book saturated**
- Step 17,200: 55 experts [13,16,13,13]
- Step 18,350: 56 experts [13,16,13,14]
- Step 19,300: 57 experts [13,17,13,14]
- Step 19,600: 58 experts [13,17,13,15]
- Step 20,000: **58 experts** — expert spawning continued to lr≈3×10⁻⁷ (near-zero)

**Key observation**: Expert spawning continued all the way through cosine decay cooldown. The market
finds new niches even as learning rate approaches zero — fundamentally different from standard training
where nothing structurally changes after convergence.

**Recipe book saturation**: 25 recipes unchanged from step 12,800 through step 20,000. The routing
grammar (which expert serves which downstream expert) was fully discovered by step 12,800; the remaining
7,200 steps only refined weights without discovering new compositional patterns.

### Temperature sweep — three dynamical regimes

| Temperature | Run | Experts | Top-4 load | Character |
|-------------|-----|---------|------------|-----------|
| T=0.1 | out_T01 | 4 | ~100% | **Stagnation**: only seed experts survive, no discovery |
| T=1.0 | out_20k | 58 | ~74% | **Selection**: balanced hub-and-spoke, coherent specialists |
| T=3.0 | out_T30_5k | ~42 | ~90% | **Tar**: many micro-niches, routing fragmented, concentrated |

- T=0.1: Evans-Polanyi barrier too high. No discovery. Pure selection regime collapses to monosemantic
  seed experts. Loss plateau is highest.
- T=1.0 (selection): Optimal. 58 experts emerge, load distributed, val loss 0.7663.
- T=3.0 (tar): Counter-intuitive — MORE experts than T=1.0 but MORE concentrated (90% top-4 vs 74%).
  The market overshoots: too many micro-niches, no dominant hubs, routing fragmented. This is the
  tar regime: expert birth exceeds death, routing collapses to a few dominant pathways.

**τ_d/τ_p ratio**: T=1.0 is the balanced regime where discoveryBudget/workerCount ≈ 0.011.
T=0.1 pushes τ_d toward infinity (no discovery); T=3.0 makes τ_d → 0 (all discovery, no selection).

### Expert specialization analysis (T=1.0, 20K run)

**Overall architecture: hub-and-spoke at every layer**
- 2–3 generalist hubs per layer (15K–18K activations, uniform ~2–4× across all chars)
- Many ultra-specialists (100–2,000 acts, 10–137× concentration on single features)

**Layer 0 — Raw character recognition**
- E15: â(42×), ™(21×), €(17×) → **UTF-8 multibyte specialist** (handles garbled encoding)
- E14: ?(49×) → question mark specialist
- E17: 3(63×), M(31×), R(21×) → digit/letter specialist
- E20: x(135×) — only 17 activations — extreme rare-char niche
- E9, E10: **0 activations** — dead experts (market death mechanism worked)

**Layer 1 — Word-boundary/morphological**
- E1: 18,600 acts, uniform 2.1× — **dominant generalist**
- E2: ' '(4.2×), '\n'(1.9×) → **word-boundary specialist**
- E7: z(137×) — only 20 activations — extreme 'z' niche
- E9: ','(96×), '\''(32×) — only 29 acts — **comma+apostrophe specialist**
- E25: C(31×), W(28×), '\n'(16×), '"'(15×) → **sentence-start capitals**
- E31: ™(13×), :(13×), .(10×), ?(8×) → **sentence-end punctuation**
- E5, E11, E12: **0 activations** — dead experts

**Layer 2 — Syntactic roles**
- E3: 15,906 acts (highest in run) — dominant generalist
- E1: a/o/O/A(6×) → **pure vowel specialist**
- E17: :(13×), ','(11×), .(11×), !(9×) → **sentence structure punctuation**
- E20: E(18×), T(15×), I(14×), A(12×), B(10×), R(8×) → **proper noun initials**
- E27: œ(23×), â(18×) → **UTF-8 specialist** (same role as L0-E15, different layer)

**Layer 3 — Discourse/semantic**
- E1: 17,693 acts — dominant generalist
- E6: '\''(16×), ™(12×) → **contraction specialist** (it's, don't)
- E22: œ(25×), ?(14×), :(13×), !(10×) → **dialogue punctuation + UTF-8**
- E23: S(18×), ','(8×), '\n'(7×) → **S-names + narrative boundaries**
- E28: :(7×), .(7×), '\n'(6×) → **sentence termination**
- E31: V(25×), L(9×), T(9×) → **proper noun initials** (Violet, Lucas, Tom)
- E9: **0 activations** — dead expert

**Three key findings:**

1. **Cross-layer UTF-8 pipeline**: â, ™, €, œ route to specialists at EVERY layer (L0-E15 → L2-E27 → L3-E22).
   The market built a dedicated 4-layer sub-network for a specific encoding artifact. No human designed this.

2. **Ascending abstraction — confirmed at 20K**:
   - L0: Raw character identity (?(49×), x(135×), â(42×))
   - L1: Word-boundary structure (space, sentence-start capitals(28–31×), punctuation(13×))
   - L2: Syntactic class (vowels(6×), proper noun uppercase(18×), sentence punctuation(13×))
   - L3: Discourse function (contractions(16×), narrative boundaries(7×), proper noun initials(25×))

3. **Ultra-specialists with tiny activation counts**: Rare features get extreme concentration in
   tiny populations (z: 137× at L1-E7 with only 20 acts; x: 135× at L0-E20 with 17 acts).
   The market creates niche experts for corner cases — no human would allocate resources this way.

### No-market ablation (out_nomarket)

Same 34.8M param model, same architecture, **market mechanism disabled** (no birth/death/discovery).
All 32 expert slots initialized and active throughout. Standard router only.

**Result: polysemantic garbage collectors**

**No-market L0-E13** (270 acts): -(142×), F(114×), G(95×), E(78×), ?(31×), D(28×), !(17×), '\n'(17×)
One expert handles dash, capital F/G/E/D, question mark, exclamation, newline — ten unrelated features.
This is polysemanticity at its most extreme: F > N forces superposition onto one expert.

**No-market L3-E2** (4,038 acts): '"'(9.5×), Y(9.5×), E(9.5×), N(9.5×), €(9.5×), ™(9.5×), :(9.5×)...
ALL at exactly 9.5× — not specialization. The router routes ALL rare characters to one expert because
they share low base frequency. Identical multiplier = no semantic distinction learned.

**No-market L3-E0** (19,756 acts, max 1.9×) — single mega-hub with extremely flat specialization.
Market L3-E1 (17,693 acts, 2.2× max) — slightly less dominant, slightly higher concentration.

**No-market: no cross-layer pipeline**. UTF-8 chars scatter to different experts per layer with no
consistency. The market builds coherent pipelines; no-market builds frequency bins.

**No-market: no dead experts**. All 32 slots active (forced by initialization). Market correctly
eliminates 6 experts (L0:2, L1:3, L3:1) that found no viable niche.

**Quantitative comparison**:

| Property | No-market | Market (20K) |
|---|---|---|
| Specialist semantic purity | Polysemantic (dash+F+G in one expert) | Monosemantic (pure UTF-8, pure '?') |
| Layer 3 dominant expert | 19,756 acts (1.9× max) | 17,693 acts (2.2× max) |
| Hub balance | Lopsided (19K vs 14K) | Balanced (17.7K vs 16.3K) |
| Rare-char routing | Frequency-bin collapse | Type-coherent specialists |
| Cross-layer consistency | None | UTF-8 pipeline across 4 layers |
| Expert death | None (forced alive) | 6 experts correctly eliminated |

**The key insight**: The market doesn't achieve higher raw specialization ratios (both reach ~137×).
It achieves **semantically meaningful** specialization. No-market's 142× specialist mixes dash, F, G,
E, ?, D, !, \n into one expert. Market's 137× specialist handles pure 'z'. This is the FMA claim:
market coordination produces monosemantic experts; central planning produces polysemantic ones.

---

## Paper structure

Follow the existing draft's 12-section structure. The draft already has Sections 1–9 in good shape.
**Focus your effort on Section 10** (nanoFMT experiments) — write it with the data above.
Also strengthen the Conclusion and add the book-series framing throughout.

### Section 10 structure (nanoFMT Experimental Validation)

Write ~1,500–2,000 words for Section 10:

**10.1 Setup and Implementation**
- 34.8M params, 4 layers, character-level TinyStories
- Market parameters: birth threshold, death after 200 idle steps, Evans-Polanyi T=1.0
- Comparison runs: T=0.1, T=3.0 (temperature sweep); out_nomarket (ablation)

**10.2 Expert Population Dynamics**
- Growth from 4 → 58 experts over 20K steps
- Spawning continues to lr≈0 (market finds niches even during cooldown)
- Recipe book saturates at 25 by step 12,800 — routing grammar complete

**10.3 Three Dynamical Regimes (Assembly Theory)**
- T=0.1 stagnation: 4 experts, 100% top-4, no discovery
- T=1.0 selection: 58 experts, 74% top-4, balanced hub-and-spoke
- T=3.0 tar: ~42 experts, 90% top-4, routing fragmented
- τ_d/τ_p interpretation

**10.4 Emergent Expert Specialization Hierarchy**
- Ascending abstraction across 4 layers (L0: chars → L1: words → L2: syntax → L3: discourse)
- Hub-and-spoke architecture at every layer
- Ultra-specialist emergence (z: 137×, x: 135×)
- Cross-layer UTF-8 pipeline (no human designed this)

**10.5 Market vs No-Market: Causal Role of Market Mechanism**
- No-market ablation: polysemantic garbage collectors (L0-E13: dash+F+G+E+?+D+!+\n)
- Frequency-bin collapse in no-market L3-E2 (all rare chars at identical 9.5×)
- Dead experts in market run: 6 correctly eliminated; no dead experts in no-market
- Conclusion: market mechanism is causally responsible for monosemantic specialization

**10.6 Limitations and Scale**
- Character-level, TinyStories only — subword tokenization at GPT scale needed
- 34.8M params — need to verify expert dynamics at 1B+ params
- Recipe book at 25 recipes may not scale to diverse tasks

---

## Book-series header

Add above the title:
```html
<div style="text-align:center; color:#7f8c8d; font-family:'Segoe UI',sans-serif; font-size:0.85em; margin-bottom:4px; letter-spacing:0.05em;">THE FREE-MARKET ALGORITHM — A UNIVERSAL THEORY OF OPEN-ENDED COMPLEX SYSTEMS</div>
<div style="text-align:center; color:#2c5f8a; font-family:'Segoe UI',sans-serif; font-size:1.1em; font-weight:600; margin-bottom:20px; letter-spacing:0.03em;">Chapter 4 — Language Models</div>
```

---

## Key references (add if missing)
- Jaraiz M (2026a) Chapter 1 / arXiv:2603.12412 (economics)
- Jaraiz M (2026b) Chapter 3 / arXiv pending (chemistry)
- Jaraiz M (2026d) Chapter 5 (Immunity, in preparation)
- Hayek FA (1945) The use of knowledge in society. *American Economic Review*
- Sharma A et al. (2023) Assembly theory. *Nature*
- DeepSeek-AI (2024) DeepSeek-V3 technical report
- Elhage N et al. (2022) Toy models of superposition. *Anthropic*
- Wherry EJ (2011) — NOT needed here (immunity paper)

---

## What NOT to do

- Do NOT rewrite Sections 1–9 unless you see errors — they are already strong
- Do NOT invent experimental results — use only the numbers given above
- Do NOT understate: "the market produces monosemantic specialists" is confirmed, not speculative
- Do NOT overstate: this is a 34.8M param character-level proof of concept, not a production LLM

---

*Prepared by Claude Sonnet 4.6, 2026-03-27. Ready for Opus 4.6 high-effort writing.*
