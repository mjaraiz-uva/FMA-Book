# Opus 4.6 Briefing: Write Chapter 5 — Adaptive Immunity as a Free Market

## Your task

Write `DELIVERABLES/Paper-5-Immune-System.html` — a complete, publication-quality HTML paper
in the same style as the existing DELIVERABLES papers (see style notes below).

This is **Chapter 5** of the book *"The Free-Market Algorithm: A Universal Theory of
Open-Ended Complex Systems."*

---

## Context you must read first

1. **`DELIVERABLES/Paper-3-Free-Market-Algorithm.html`** — Chapter 1. Read especially:
   - Section 3 (The Free-Market Algorithm) — formal specification, agent cycle, pseudocode
   - Section 4 (Assembly Theory connection) — three regimes, τ_d/τ_p
   - Section 9.2 (Universality) — the five-domain table; Chapter 5 must be consistent with it

2. **`DELIVERABLES/Paper-5-Immune-System-skeleton.md`** — the full research skeleton with:
   - Complete 18-mechanism FMA→Immunity mapping table
   - 6 falsifiable predictions (P1–P6) with experimental protocols
   - Three regimes in immunity
   - Training-inference collapse in immunity
   - Germinal center as local free market
   - Assembly Theory connection
   - Key literature list

3. **`Core/MarketSim.h`** and **`Core/MarketSim.cpp`** in the MolecularDeployer repo —
   every mechanism claim must cite a specific function. Key functions:
   - `WorkerMonthlyActivity()` — the agent cycle (birth/death/produce/discover in same loop)
   - `WorkerTryDiscovery()` — Evans-Polanyi gated discovery
   - `ProducerDecay()` — complexity-proportional decay
   - `ComputeGFCF()` — demand cascade
   - `CensusCoverage()` — diversity preservation
   - `WitnessBoost()` — amplified demand on new discovery

---

## Paper structure (12 sections, ~8,000–10,000 words)

### 0. Abstract
Three claims:
1. **Structural**: Every named FMA mechanism has a precise biological counterpart in adaptive immunity.
2. **Existence proof**: FMA was validated independently in economics and chemistry before this
   comparison — this is not post-hoc metaphor fitting.
3. **Predictions**: Six novel falsifiable predictions, including Evans-Polanyi T-cell activation
   kinetics (α≈0.5, same coefficient as chemistry Paper-3) and cytokine storm as tar regime.

### 1. Introduction
- 1.1 The central planning problem in immunology: antigen space ~10^18; no central planner
  can pre-specify required specialists; clonal selection as distributed discovery
- 1.2 What FMA adds to 70 years of clonal selection theory (Burnet 1957): quantitative
  formalism, testable predictions, unification of phenomena previously treated separately
- 1.3 Contributions: 18-mechanism mapping, 6 predictions, training-inference collapse in biology

### 2. Background
- 2.1 Clonal selection and expansion (Burnet, Jerne)
- 2.2 Affinity maturation and germinal centers (Victora & Nussenzweig 2012)
- 2.3 T cell exhaustion (Wherry 2011)
- 2.4 Cytokine storm (Fajgenbaum & June 2020, NEJM)
- 2.5 Immunological memory
- 2.6 FMA summary (cite Chapter 1; do NOT re-derive the algorithm)

### 3. The Complete FMA→Immunity Mapping (18 mechanisms)
Full HTML table: mechanism | FMA code function | immune analog | why it maps
Use the skeleton's 18-row table as your source. Write one paragraph per the 6 most important
mechanisms (Evans-Polanyi, depth penalty, recipe book, census coverage, witness, GFCF).
The remaining 12 get table rows only.

### 4. The Training-Inference Collapse in Immunity
- The false dichotomy: primary response = training, secondary = inference
- FMA's simultaneity: `WorkerTryDiscovery()` and `WorkerRunProducer()` in same loop, same step
- Memory B cells continue affinity maturation during secondary response
- Not continual learning — recipes additive, no catastrophic forgetting by construction
- Original antigenic sin (Fabian 1960) as a consequence of recipe book persistence

### 5. Three Dynamical Regimes
Stagnation (tolerance/anergy) | Selection (normal adaptive immunity) | Tar (cytokine storm)

**Key insight on tar**: cytokine storm is NOT "too much immunity" — it is failure of the
producer death mechanism. Birth/death ratio imbalance, not absolute cytokine levels.
Clinical implication: early IL-6 blockade (Tocilizumab) is more effective than late
intervention because it restores birth/death balance, not just downstream cytokine suppression.

### 6. Superposition in Immunity
- HIV/AIDS: CD4+ T cell depletion destroys the routing/coordination layer (not just workers)
- Lymphopenia → lymphopenia-induced proliferation → oligoclonal expansion = superposition
- Census coverage prediction: IL-7 therapy should preferentially expand rare clones

### 7. The Germinal Center as a Local Free Market
- O(k) locality property: B cells compete for antigen on FDCs locally, not globally
- Affinity maturation converges to local optimum
- Two antigens in same GC impair each other (Prediction P6)
- Contrast with global loss minimization in neural networks

### 8. Assembly Theory Connection
- Affinity maturation = increasing assembly index of BCR paratope
- τ_d/τ_p ratio maps to GC dynamics; AID overexpression → tar → lymphoma
- Three AT regimes in immunology

### 9. Six Novel Predictions
P1: Evans-Polanyi T-cell activation (α≈0.5 with altered peptide ligands)
P2: Exhaustion scales with cascade depth, not dose
P3: IL-7 preferentially expands rare clones (census coverage)
P4: Memory quality scales with antigen assembly index
P5: Cytokine storm predicted by birth/death ratio, not IL-6 alone
P6: Two antigens in same GC impair mutual affinity maturation

Each prediction: hypothesis | experimental setup | measurement | expected result | falsification criterion

### 10. Cancer Immunotherapy as FMA Engineering
- Cancer as tar regime at cellular level: uncontrolled clonal expansion, loss of death signal
- Checkpoint inhibitors (PD-1/CTLA-4): removing depth penalty suppression → restore producer death
- CAR-T therapy: engineering specialists with prescribed receptors = Target mode (FMA Mode 2)
- Cancer vaccines: providing demand signal for anti-tumour specialists
- Adoptive cell transfer: seeding the market with proven specialists
- FMA prediction: combination therapy should target birth/death ratio, not individual checkpoints

### 11. Discussion
- 11.1 FMA as universal biology: economics → chemistry → computation → language → immunity
- 11.2 What immunity teaches FMA: possible feedback to algorithm design (e.g., cytokine-inspired
  adaptive learning rates, GC-inspired local expert competition)
- 11.3 Prior immune network theories (Jerne 1974, Perelson 1989) and what FMA adds
- 11.4 Limitations and open questions

### 12. Conclusion
The adaptive immune system did not read Hayek. It discovered the free market by natural selection,
running the same algorithm that governs macroeconomic forecasting and prebiotic chemistry.
The seven equations of Chapter 1 — unmodified — describe clonal selection, affinity maturation,
immunological memory, T-cell exhaustion, and cytokine storm as instances of one dynamical system.

---

## Style requirements

- HTML file, same CSS as `Paper-3-Free-Market-Algorithm.html` (copy the `<style>` block exactly)
- Use `.insight` boxes for key findings, `.highlight` for warnings, `.success` for validated claims
- Use `.equation` class for key equations
- Include SVG figures where helpful (agent cycle in immunity, three-regime diagram, GC market figure)
- Use `<sup>` for reference numbers
- Section numbering: 1–12, subsections 1.1, 1.2, etc.
- Abstract: ~250 words
- Each of sections 3–10: 400–800 words
- Total: 8,000–10,000 words

---

## What NOT to do

- Do NOT re-derive the FMA algorithm — cite Chapter 1 throughout
- Do NOT write a general immunology review — assume a technically literate reader
- Do NOT overstate: say "maps precisely onto" not "proves that"
- Do NOT understate: this is not metaphor, it is mechanistic correspondence

---

## Key references (minimum required)
- Burnet FM (1957) Clonal selection theory
- Jerne NK (1955) Natural selection theory of antibody formation
- Victora GD & Nussenzweig MC (2012) Germinal centers. *Annu Rev Immunol*
- Wherry EJ (2011) T cell exhaustion. *Nature Immunology*
- Fajgenbaum DC & June CH (2020) Cytokine storm. *NEJM*
- Hayek FA (1945) The use of knowledge in society. *American Economic Review*
- Sharma A et al. (2023) Assembly theory. *Nature*
- Jaraiz M (2026a) Chapter 1 / arXiv:2603.12412 (economics)
- Jaraiz M (2026b) Chapter 3 / arXiv pending (chemistry)
- Jaraiz M (2026c) Chapter 4 (FMT, in preparation)

---

## Cancer immunotherapy extension (Section 10)

This section is NOT in the skeleton — write it from first principles using the FMA mapping.
The key insight: cancer is a tar regime failure at the cellular level. The tumour microenvironment
suppresses producer death (via PD-L1, CTLA-4, IDO, TGF-β) and amplifies producer birth
(via VEGF, IL-6, EGF). Therapies restore FMA dynamics:

| Therapy | FMA mechanism restored |
|---------|----------------------|
| PD-1/PD-L1 blockade | Removes artificial depth penalty suppression → producer death resumes |
| CTLA-4 blockade | Lowers Evans-Polanyi barrier for T cell activation → birth rate normalises |
| CAR-T | Target mode: specialist with prescribed receptor seeded directly |
| Cancer vaccines | Provides authentic demand signal for anti-tumour specialists |
| IL-2 therapy | GFCF cascade amplification for anti-tumour producers |
| Adoptive cell transfer | Seeds recipe book with proven anti-tumour producers |

FMA prediction for combination therapy: synergy should be strongest between therapies that
target BOTH birth (checkpoint blockade) AND death (Treg depletion / IL-10 blockade) signals,
because cytokine storm risk is determined by birth/death ratio, not individual pathway inhibition.

---

*Prepared by Claude Sonnet 4.6, 2026-03-27. Ready for Opus 4.6 high-effort writing.*
