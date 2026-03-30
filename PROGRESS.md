# The Free-Market Algorithm — Book Progress

## Current Status (2026-03-29)

Five-chapter book structure complete with HTML versions, consistent branding, two interactive viewers (Ch4 Transformer, Ch5 Immune), and a one-page Introduction with Martin's origin story. All chapters now have collapsible/foldable sections (JS-based) and "← Index" navigation buttons. New Ch4 Annex B (Results Analysis) frames FMA as an AI orchestration layer above gradient descent. Phase A enhancements complete: visual index page, cross-chapter navigation, Introduction roadmap. Phase B complete: orchestration principle in Introduction, Ch5 results analysis annex, cross-domain interactive figure, ANALYSIS revision, editor one-page overview. All pushed to github.com/mjaraiz-uva/DELIVERABLES.

## Chapters

### Introduction
- [x] Written with Martin's personal origin story (2026-03-29)
- [x] "reduces to a single step" wording for training/inference
- [x] nanoFMT explained for outsiders ("a minimal language model written from scratch in which there is no gradient descent")
- [x] Prebiotic arXiv reference removed (pending appeal)
- [x] Footer: arXiv:2603.24559 only
- [x] Chapter roadmap table with domain, key result, and status per chapter (Phase A3, 2026-03-29)
- [x] "How to read this book" callout box with links to interactive viewers (Phase A3, 2026-03-29)
- [x] "The Orchestration Principle" section with cross-domain table: native optimization vs FMA orchestration (Phase B4, 2026-03-29)

### Chapter 1 — The Framework (Paper-3)
- [x] HTML with book header/footer
- [x] arXiv:2603.24559
- [x] Author's Disclosure removed, AI Assistance Statement kept

### Chapter 2 — Macroeconomics (Paper-1)
- [x] HTML with book header/footer
- [x] arXiv:2603.12412

### Chapter 3 — Prebiotic Chemistry (Paper-2)
- [x] HTML with book header/footer
- [x] Draft in preparation (arXiv pending appeal)
- [x] References: arXiv links restored for published papers
- [ ] Interactive viewer (deferred — needs structured data from MolecularDeployer C++)

### Chapter 4 — Language Models (Paper-4)
- [x] HTML with book header/footer
- [x] Interactive viewer (Paper-4-FMT-viewer.html) — 1083 lines, 6 scenarios, 8 charts, tutorial guide
- [x] LLM explainer annex (Annex A)
- [x] Results analysis annex (Annex B) — "FMA as AI Orchestration Layer", panel-by-panel, 5 foldable sections (2026-03-29)
- [x] Y-axis ticks and values on all charts
- [x] Run/Reset buttons moved above FMA Parameters

### Chapter 5 — Adaptive Immunity (Paper-5)
- [x] HTML with book header/footer
- [x] Interactive viewer (Paper-5-Immune-viewer.html) — light/dark theme, 6 scenarios
- [x] Evaluation report (PDF and HTML)
- [x] Regime thresholds recalibrated to 1.0/5.0
- [x] Exhaustion Y-axis fixed to 0-0.25
- [x] Results analysis annex (Annex B) — "FMA as Immunological Orchestration Layer", 6 foldable sections, 6-scenario analysis, 6 predictions table (Phase B7, 2026-03-29)
- [x] Annexes bar added to Paper-5 footer; "Results Analysis" link added to viewer header (Phase B7, 2026-03-29)

## Book Infrastructure
- [x] index.html visual landing page with thesis box, domain map, quick-start callout, refined chapter cards (Phase A1, 2026-03-29)
- [x] Cross-chapter navigation: Previous/Index/Next footer bar on all 6 chapters (Phase A2, 2026-03-29)
- [x] Consistent headers/footers across all chapters
- [x] DELIVERABLES folder structure: Macro/, Prebiotic/, FMA/, Transformer/, Immune/
- [x] GitHub repo: github.com/mjaraiz-uva/DELIVERABLES
- [x] All chapters: collapsible/foldable sections with Expand/Collapse all buttons (JS-based, 2026-03-29)
- [x] All chapters: "← Index" navigation button at top (2026-03-29)
- [x] Both viewers: header nav links (Paper, Index) added (2026-03-29)
- [x] Universal-Dynamics.html: interactive 4-panel cross-domain comparison with EP temperature slider (Phase B6, 2026-03-29)
- [x] FMA-Editor-Overview.html: one-page HTML overview for Nature/Springer editors (2026-03-29)
- [x] ANALYSIS-FMA-language-chess.md: revised from "compete with gradient descent" to "orchestrate above gradient descent" (Phase B8, 2026-03-29)

## Failed Approaches / Decisions
- Regime thresholds 0.3/2.0 didn't work for immune dynamics — recalibrated to 1.0/5.0 (2026-03-28)
- PIL cropping needed for truncated PNGs (black bands from Windows file copy)
- Mounted files can't be overwritten directly — write to working dir first, then copy
- "collapses" for training/inference dichotomy rejected in favor of "reduces to a single step" (2026-03-29)
- "fades away / vanishes / disappears" also rejected — too soft for a structural change
- DOM-restructuring approach to foldable sections (wrapping h2 in `<details>`) broke HTML on complex files — switched to JS-based runtime approach that doesn't touch original structure (2026-03-29)
- FMA competing with gradient descent "from below" (learning characters/words) is the wrong framing — FMA operates *above* transformers as an orchestration layer (2026-03-29)

## Next Steps
- [ ] B5: Domain shift experiment — needs nanoFMT code modification + compute (modify train.py to switch data source at step N, extract metrics, produce figures)
- [ ] Replace schematic curves in Universal-Dynamics.html with real simulation data from MolecularDeployer, nanoFMT, nanoImmune
- [ ] Prebiotic interactive viewer (blocked on structured C++ output from MolecularDeployer)
- [ ] Publishing strategy execution: Nature Article pre-submission enquiry + Springer Nature monograph proposal
- [ ] Commit & push Phase B changes to github.com/mjaraiz-uva/DELIVERABLES
- [ ] Consider PROGRESS.md updates as standard session close-out

## Methodology
Following recommendations from Carlini 2026 parallel-agent study (CLAX CLAUDE.md):
- Update this file after every meaningful unit of work
- Record failed approaches so they aren't re-attempted
- Document for the next session, not for users
