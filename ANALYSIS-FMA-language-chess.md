# Can the Free-Market Algorithm Orchestrate Language Models, Play Chess, or Rival LLMs?

*Analysis prepared 2026-03-30, revised 2026-03-29 — M. Jaraiz / Claude*

## 0. The Orchestration Reframe

**Previous framing (abandoned):** FMA competes with gradient descent by learning characters/words from scratch, treating language as a chemistry analogue.

**Current framing:** FMA does not replace gradient descent. It operates *one level above*, orchestrating the population of neural expert modules that gradient descent trains internally. This is consistent with what FMA does in every other domain: it manages the population of problem-solvers, not the internal optimization of individual solvers.

> In economics, FMA orchestrates firms above individual transactions.
> In chemistry, FMA orchestrates species above individual reactions.
> In AI, FMA orchestrates expert modules above gradient descent.
> In immunity, FMA orchestrates clones above antigen binding.

This reframe resolves the structural mismatch identified in Section 4 of the original analysis: FMA's local, myopic optimization *should not* try to compete with gradient descent's globally coherent parameter updates. Instead, FMA handles what gradient descent cannot: dynamic architecture — the birth, death, specialization, and routing of expert modules.

---

## 1. Chess: Can FMA Orchestrate a Chess System?

### 1.1 The Original Problem (unchanged)

Chess is fundamentally a lookahead problem. FMA agents are myopic optimizers — they evaluate based on local outcomes. A market-based approach that scores moves by immediate results would systematically miss deep sacrificial combinations. AlphaZero solves this with MCTS + neural value networks; FMA has no native equivalent.

### 1.2 The Orchestration Alternative

Rather than trying to learn chess from scratch, FMA could *orchestrate a collection of chess-playing modules*:

- **Opening book expert**: trained (by gradient descent) on opening databases
- **Tactical expert**: trained on tactical puzzles (forks, pins, skewers)
- **Endgame expert**: trained on endgame tablebases
- **Positional expert**: trained on quiet middle-game evaluations

FMA's role: decide *which expert to consult* at each board state, manage expert birth/death based on utility (retire the opening expert by move 20), and form recipes (expert chains that work well together for specific position types).

### 1.3 Honest Assessment

- **Might work:** Orchestrating heterogeneous chess modules, routing to specialists based on position type, managing the ensemble's composition dynamically.
- **Probably fails:** Learning chess from scratch without lookahead. The fundamental impedance mismatch with FMA's local optimization remains.
- **Core advantage over fixed ensembles:** Dynamic architecture. A fixed MoE has a static expert roster; FMA can birth new specialists for novel position types and retire stale ones.

---

## 2. FMA vs. LLMs: Structural Comparison (Revised)

### 2.1 What Gradient Descent Does Well

- Updates all parameters simultaneously with a globally coherent signal — remarkably efficient
- Scales predictably with compute (neural scaling laws)
- Discovers distributed representations that generalize across contexts
- Sample-efficient for learning abstract features

### 2.2 What FMA Does That Gradient Descent Cannot

1. **Dynamic architecture** — expert modules born/die based on utility. No fixed model size. The architecture adapts to the task distribution without retraining.
2. **Monosemantic experts** — market competition produces pure specialists. Standard MoE routing produces polysemantic garbage-collector experts (confirmed in nanoFMT).
3. **Training-inference collapse** — every forward pass is simultaneously learning and producing output. No two-phase training/deployment.
4. **Domain shift without retraining** — when the task distribution changes, FMA's birth/death mechanism automatically grows new specialists and retires obsolete ones. Gradient-based models require fine-tuning or retraining.
5. **Interpretable specialization** — each expert has a readable role, unlike entangled distributed representations.
6. **Recipe book as persistent memory** — successful expert activation chains are stored and reused across sessions.

### 2.3 The Language-Chemistry Analogy (Demoted)

The original analysis proposed a deep isomorphism between language and chemistry:

```
Characters → Words → Sentences → Paragraphs
     ↕          ↕         ↕            ↕
Atoms → Molecules → Pathways → Organisms
```

**Revised assessment:** This analogy is useful pedagogically but does not imply comparable computational difficulty. Language has long-range dependencies and arbitrary conventions; chemistry has local interactions and universal physical laws. FMA's success in chemistry rests on thermodynamic gradients providing strong local fitness signals. Language lacks such gradients at the character/word level.

**The analogy becomes accurate at the orchestration level:** Just as FMA orchestrates molecular species above individual reactions, it orchestrates expert modules above individual parameter updates. The analogy works for *populations of problem-solvers*, not for individual problem-solving.

---

## 3. Revised Experimental Plan

### 3.1 Orchestration Experiments (Primary)

#### Experiment 1: Domain Shift (nanoFMT)
- **Task:** Train nanoFMT on TinyStories, then abruptly switch to code/Wikipedia at step N
- **FMA prediction:** Birth/death mechanism creates new specialists for the new domain; recipes diverge; loss recovers without retraining
- **Success:** Faster recovery than retraining from scratch; new monosemantic experts visible in viewer
- **Resources:** nanoFMT repo + GPU; ~1 session

#### Experiment 2: Multi-Task Orchestration
- **Task:** One FMT handling stories + code + arithmetic simultaneously
- **FMA prediction:** Market allocates separate expert pools per task type; recipes encode task-specific chains
- **Success:** Per-task performance comparable to separate models; zero cross-task interference
- **Resources:** Modified nanoFMT + 2–4 GPU hours

#### Experiment 3: Scale Sweep
- **Task:** Run nanoFMT with 20, 50, 100, 200, 500 experts
- **FMA prediction:** Monosemanticity advantage grows with pool size (more room for specialization). At small sizes, census coverage forces polysemanticity.
- **Success:** Quantitative relationship between pool size and expert purity
- **Resources:** 5 training runs; ~4 hours total

#### Experiment 4: Recipe Transfer
- **Task:** Train nanoFMT on TinyStories, save recipe book. Initialize a new population with old recipes.
- **FMA prediction:** Second run converges faster (recipes encode structural knowledge that transfers)
- **Success:** >2× speedup in convergence with recipe initialization
- **Resources:** 2 training runs + comparison

### 3.2 Compositional Generalization (Secondary — retained from original)

The original experiment testing whether FMA discovers abstract production rules (balanced parentheses over {a,b} transferring to {p,q}) remains informative but is now secondary. The primary question is no longer "can FMA learn language from scratch?" but "can FMA orchestrate language-processing modules better than static ensembles?"

### 3.3 What "Success" Looks Like (Revised)

**Convincing results:**
- Domain shift handled autonomously (no retraining, no hyperparameter adjustment)
- Multi-task orchestration with clean expert specialization
- Monosemanticity quantified as a function of pool size
- Recipe transfer accelerates convergence

**NOT convincing:**
- "FMA matches GPT-4 on language" (wrong goal — FMA is not a language model, it is an orchestration layer)
- "FMA achieves state-of-the-art on GLUE" (wrong domain — FMA orchestrates, it does not compete)

---

## 4. Risks and Honest Challenges (Revised)

### 4.1 Strongest Arguments Against

1. **Overhead may not justify itself.** If gradient descent + standard MoE routing already handles domain shift adequately (via fine-tuning), FMA's orchestration layer is unnecessary complexity.

2. **Birth/death stochasticity.** FMA's population dynamics are inherently noisier than gradient descent. At scale, this noise may become a liability rather than a source of exploration.

3. **Recipe book scalability.** In chemistry, a few hundred reactions cover the interesting space. In language, the space of useful expert chains may be too large for a recipe book to provide meaningful compression.

4. **The monosemanticity advantage may not survive scaling.** nanoFMT's clean specialization may be a small-model phenomenon that disappears when expert pools reach thousands.

### 4.2 What Would Falsify the Orchestration Hypothesis

| Prediction | Falsification |
|---|---|
| Domain shift handled by birth/death | No new experts born after distribution shift |
| Monosemanticity from market competition | Experts remain polysemantic regardless of pool size |
| Recipe transfer accelerates convergence | No speedup with recipe initialization |
| Multi-task routing is emergent | Market routing degrades to random; explicit routing required |
| Dynamic architecture outperforms fixed MoE | Fixed 8-expert MoE matches or beats dynamic FMT |

### 4.3 The Core Question (Revised)

The question is no longer "can FMA learn language?" but "does dynamic architecture orchestration provide measurable advantages over static architecture?"

**Current honest assessment:** Plausible. The nanoFMT results (monosemanticity, three regimes, expert hierarchy) already demonstrate that FMA orchestration produces qualitatively different behaviour from standard MoE. The remaining question is whether these qualitative differences translate into quantitative advantages at practical scales.

---

## 5. Recommended Next Steps

1. **Implement Experiment 1** (domain shift) — this is the single most compelling demonstration, already partially planned as B5 in the enhancement plan
2. **Run Experiment 3** (scale sweep) — cheapest way to test whether monosemanticity scales
3. If positive on both: implement Experiments 2 and 4
4. **Either way: the result is publishable** as "Market-Based Orchestration of Expert Modules in Neural Networks"
