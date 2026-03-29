# The Free-Market Algorithm

**A Universal Theory of Open-Ended Complex Systems**

Martin Jaraiz Maldonado
Professor Emeritus, Department of Electricity and Electronics
University of Valladolid, Spain

arXiv:2603.24559 (Framework) | arXiv:2603.12412 (Macroeconomic Forecasting)

---

## What is the FMA?

The Free-Market Algorithm is an 18-mechanism optimization framework in which autonomous agents compete in an open-ended market. The same algorithm — unchanged — produces qualitatively correct behaviour in five independent domains: macroeconomic forecasting, prebiotic chemistry, language modelling, adaptive immunity, and robotic task planning.

These are not analogies. They are structural isomorphisms governed by a single set of equations.

## The Book

The main deliverable is `The_FM_Algorithm/` — an HTML-based book with interactive viewers. Open `The_FM_Algorithm/index.html` in a browser to start reading.

| Chapter | Domain | Key Result | Status |
|---------|--------|------------|--------|
| 1. The Framework | General theory | 18 mechanisms, 3-layer architecture | Published |
| 2. Macroeconomics | GDP forecasting | MAE 0.42 pp, 33/37 OECD countries | Published |
| 3. Prebiotic Chemistry | Origin of life | 12/12 amino acids, 5/5 nucleobases | Draft |
| 4. Language Models | AI / Transformers | 58 self-organized experts, no gradient descent | Draft |
| 5. Adaptive Immunity | Immunology | Complete 18-mechanism mapping, 6 predictions | Draft |

### Interactive Viewers

Chapters 4 and 5 include browser-based simulators that let you explore FMA dynamics in real time:

- **nanoFMT viewer** (`Ch4-Transformer/Paper-4-FMT-viewer.html`) — market-orchestrated transformer with dynamic expert birth/death, three dynamical regimes, domain shift
- **nanoImmune viewer** (`Ch5-Immune/Paper-5-Immune-viewer.html`) — adaptive immune system simulator with 6 scenarios (normal response, chronic infection, cytokine storm, vaccination, lymphopenia, custom)

## Repository Structure

```
The_FM_Algorithm/          # The book (start here)
  index.html               # Landing page
  Introduction.html         # Origin story + orchestration principle
  FMA-Editor-Overview.html  # One-page overview for editors
  Universal-Dynamics.html   # Interactive cross-domain comparison
  PROGRESS.md               # Detailed progress tracker
  PLAN-enhancements.md      # Enhancement roadmap
  Ch1-Framework/            # Chapter 1 — formal FMA definition
  Ch2-Macroeconomics/       # Chapter 2 — GDP forecasting with FIGARO data
  Ch3-Prebiotic-Chemistry/  # Chapter 3 — amino acids, nucleobases, Assembly Theory
  Ch4-Transformer/          # Chapter 4 — nanoFMT + interactive viewer + annexes
  Ch5-Immune/               # Chapter 5 — immunity mapping + nanoImmune viewer + annexes
```

Mirror folders at the top level (`FMA/`, `Macro/`, `Prebiotic/`, `Transformer/`, `Immune/`) contain copies of the main chapter papers for backward compatibility.

## Three Dynamical Regimes

A single parameter (Evans-Polanyi temperature) controls the boundary between three universal regimes:

- **Stagnation** — no selection, random exploration (economics: stasis; chemistry: random reactions; immunity: tolerance)
- **Selection** — specialization, competition, emergent complexity (economics: growth; chemistry: life's toolkit; immunity: adaptive response)
- **Tar** — runaway positive feedback, collapse (economics: bubble/crash; chemistry: tar; immunity: cytokine storm)

## Related Repositories

- [nanoFMT](https://github.com/mjaraiz-uva/nanoFMT) — FMA-orchestrated transformer (C++/Python)
- [nanoImmune](https://github.com/mjaraiz-uva/nanoImmune) — FMA immune system simulation

## Contact

mjaraiz@uva.es
