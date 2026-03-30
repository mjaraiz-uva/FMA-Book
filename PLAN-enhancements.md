# FMA Book — Enhancement Plan

## Overview

Eight enhancements organized into three phases. Phase A (book navigation & polish) has no dependencies and can be done immediately. Phase B (new content) builds on Phase A. Phase C (experimental) requires nanoFMT code changes.

---

## Phase A — Navigation & Polish (can start now)

### A1. Index Page Upgrade
**Goal:** Transform the plain chapter-card list into a compelling landing page.

**What changes:**
- Add a visual "map" or diagram at the top: the 7 core equations at the center, 5 domains radiating outward (Economics, Chemistry, Language, Immunity, + Robotics implied), each with its key result (MAE 0.42pp, 12 amino acids, 58 experts, 6 predictions)
- Add status badges per chapter (Published / Draft / In preparation) more visually prominent
- Add a "Quick start" callout: "New here? Start with the Introduction, or jump to the interactive viewers: nanoFMT | nanoImmune"
- Keep the existing chapter cards but refine styling (subtle shadows, hover effects)
- Add the thesis paragraph at top rather than bottom — it's the first thing a visitor should read
- Responsive: should work on mobile

**Implementation:** Rewrite `index.html` as a single-file HTML with embedded CSS. No frameworks. Approximately 200–300 lines.

**Effort:** ~1 session

---

### A2. Cross-Chapter Navigation
**Goal:** Make the book feel like a book, not a collection of separate files.

**What changes:**
- Add a footer navigation bar to each chapter: `← Previous Chapter | Index | Next Chapter →`
- Consistent styling across all chapters (same blue bar, same font)
- The Introduction gets only `Index | Next →`; Chapter 5 gets only `← Previous | Index`
- Add via JS injection (same pattern as the foldable sections), so original HTML stays clean

**Navigation map:**
```
Introduction → Ch1 Framework → Ch2 Macro → Ch3 Prebiotic → Ch4 Transformer → Ch5 Immune
```

**Implementation:** Extend the existing `inject_index_link.py` to also inject prev/next links. Each file needs to know its position in the sequence. A small config array in the JS handles this.

**Effort:** ~30 minutes

---

### A3. Introduction Strengthening
**Goal:** Make the Introduction work as a proper book opener for a first-time reader.

**What changes:**
- Add a **chapter roadmap** section after the narrative (currently the roadmap paragraph at line 79 exists but could be more visual — a small table or styled list linking each chapter to its domain, key result, and status)
- Add a **"How to read this book"** paragraph: "Each chapter is self-contained and can be read independently. Chapters 4 and 5 include interactive simulators. For the impatient: the interactive viewers give the fastest overview of FMA dynamics."
- Consider adding the 18-mechanism summary table (currently in Ch1 Section 3) as a compact reference, so readers have it before diving into any chapter

**Implementation:** Edit `Introduction.html` directly. Add ~40–60 lines.

**Effort:** ~30 minutes

---

## Phase B — New Content (depends on Phase A for navigation)

### B4. "FMA as Orchestration Layer" as Standalone Argument
**Goal:** Develop the central insight from the Results Analysis annex into a more prominent position.

**What changes:**
- Option 1 (minimal): Add a new Section 12.4 to Paper-4 titled "FMA as Orchestration Layer" that consolidates the argument from the annex into the main paper
- Option 2 (recommended): Elevate this to a brief **new section in the Introduction** — because the "orchestration above gradient descent" framing applies to *all* five domains (FMA orchestrates firms above individual transactions in economics, orchestrates molecular species above individual reactions in chemistry, etc.)
- Update the Results Analysis annex to reference this new Introduction section

**Key argument to develop:**
> In every domain, FMA operates one level above the domain's native optimization:
> - Economics: above individual transactions → organises firms
> - Chemistry: above individual reactions → organises species populations
> - Language models: above gradient descent → organises expert modules
> - Immunity: above individual antigen encounters → organises clonal populations

**Implementation:** Edit Introduction.html + possibly Paper-4. ~60–80 lines of new content.

**Effort:** ~1 session

---

### B5. Domain Shift Experiment (Real, Not Simulated)
**Goal:** Produce the single most compelling figure in the book — real nanoFMT adapting to a distribution shift.

**What needs to happen:**
1. Modify nanoFMT's `train.py` to switch the training data source at step N (e.g., from TinyStories to a code corpus or Wikipedia)
2. Run the training with metrics logging (expert population, birth/death events, loss, recipes)
3. Extract the metrics.json and produce figures showing:
   - Loss spike and recovery
   - Expert population surge (new specialists for the new domain)
   - Unmet demand spike and resolution
   - New recipes formed post-shift
4. Add these figures to Paper-4 Section 10 as a new subsection "10.8 Domain Shift Validation"
5. Update the interactive viewer's Domain Shift scenario description to reference the real results

**Dependencies:** Requires access to nanoFMT repo and compute (UVa HPC or local). This is the most effort-intensive item.

**Effort:** ~2–3 sessions (code modification, run, analysis, figures, paper update)

---

### B6. Cross-Domain Comparison Figure
**Goal:** One figure that visually proves universality — same dynamics, four domains.

**What it shows:** A 4-panel (or 2×2) figure comparing birth/death dynamics across:
- Panel A: Macroeconomics (firm creation/destruction over time)
- Panel B: Prebiotic chemistry (species population dynamics)
- Panel C: nanoFMT (expert population dynamics)
- Panel D: nanoImmune (T-cell clonal dynamics)

All four panels on the same X-axis scale (normalised time), same Y-axis concept (population or B/D ratio), same colour coding for the three regimes.

**Data sources:**
- Macro: needs extraction from MolecularDeployer output logs (firm counts per step)
- Prebiotic: needs extraction from MolecularDeployer output (species counts per step)
- nanoFMT: available from metrics.json in the nanoFMT repo
- nanoImmune: available from simulation outputs

**Implementation:**
- Option 1: A new standalone HTML page with 4 canvas charts (like the viewers)
- Option 2: A static SVG/PNG figure for inclusion in the Introduction
- Option 3 (recommended): An interactive HTML page that overlays all four, with toggles per domain

**Placement:** New page linked from Introduction and from index.html. Title: "Universal Dynamics Across Domains" or "The Same Algorithm, Four Domains."

**Effort:** ~1–2 sessions (data extraction is the bottleneck; the visualisation itself is straightforward)

---

### B7. Ch5 Immune Results Analysis Annex
**Goal:** Give Chapter 5 the same treatment Chapter 4 got — an annex explaining the viewer panels for immunology readers.

**What it covers:**
- 6 scenario walk-throughs (Normal Response, Immunodeficiency, Cytokine Storm, Memory Recall, Chronic Infection, Vaccination)
- Panel-by-panel explanation connecting FMA mechanisms to immunological concepts
- Comparison table: FMA mechanism → Immune counterpart → What the viewer shows
- "What to look for" callouts for each scenario
- Same foldable section structure as the Ch4 Results Analysis

**Implementation:** New file `Ch5-Immune/Paper-5annex-results-analysis.html`, modelled on the Ch4 version. ~300–400 lines.

**Effort:** ~1 session

---

### B8. Revise ANALYSIS-FMA-language-chess.md
**Goal:** Update the deep analysis to reflect the "above, not below" insight.

**What changes:**
- Remove or demote the "FMA learns characters from scratch" direction (acknowledged as wrong framing)
- Elevate the "FMA as orchestration layer" direction as the primary thesis
- Reframe the experimental plan around orchestration experiments:
  - Experiment 1: Domain shift (already planned as B5)
  - Experiment 2: Multi-task orchestration (one FMT handling stories + code + math simultaneously, market allocating experts per task)
  - Experiment 3: Scale sweep (does the monosemanticity advantage grow with model size?)
  - Experiment 4: Recipe book as persistent memory (can recipes learned in one training run accelerate a second run?)
- Update the chess analysis: FMA won't learn chess from scratch, but could it *orchestrate* a collection of chess-playing modules (opening book expert, endgame expert, tactical expert)?

**Implementation:** Edit the existing .md file. Major rewrite of sections 2–4.

**Effort:** ~1 session

---

## Execution Order

```
Phase A (do first, all independent):
  A1  Index page upgrade
  A2  Cross-chapter navigation
  A3  Introduction strengthening

Phase B (after A, partially independent):
  B4  "Orchestration layer" in Introduction  (after A3)
  B7  Ch5 Immune results analysis annex      (independent)
  B8  Revise ANALYSIS document               (independent)
  B6  Cross-domain comparison figure          (after B4; needs data extraction)
  B5  Domain shift experiment                 (independent but longest; start early if compute available)
```

**Recommended session plan:**
- Session 1: A1 + A2 + A3 (navigation polish)
- Session 2: B4 + B7 (new content: orchestration framing + immune annex)
- Session 3: B8 + B6 (revise analysis + cross-domain figure)
- Session 4: B5 (domain shift experiment — may need Martin's input on nanoFMT code and compute)

---

## Notes
- All new HTML files follow the established pattern: book header/footer, foldable sections, Index nav button
- Mirror folders updated after each session
- PROGRESS.md updated after each session (per CLAX methodology)
- Commit & push at end of each session
