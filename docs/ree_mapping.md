# REE Mapping

This document explains how the Reflective Ethical Engine (REE) architecture maps onto
the failure modes in this taxonomy.

## REE component glossary

| Symbol | Component | Role |
|---|---|---|
| E1 | Associative state / world model | Deep, slow predictive core; maintains persistent representations of world, self, and consequences across time |
| E2 | Transition prediction | Fast forward predictor; models how actions transform the current latent state |
| E3 | Trajectory selection / commitment | Evaluates candidate action sequences for harm and goal achievement; governs the commit gate |
| Control plane | Precision, salience, gain | Governs how the system operates: modulates precision weighting, exploration, replay, and commitment thresholds across E1/E2/E3 |
| RC loop | Reality testing / provenance | Compares predictions against inputs; flags mismatches; tracks whether content is real, simulated, or recalled |
| Residue | Unresolved discrepancy / persistent consequence tracking | Persistent curvature over latent space encoding accumulated post-commitment consequences — harm, benefit, viability |
| Replay | Consolidation / restructuring | Offline reprocessing of stored episodes; restructures representations; biased by harm/benefit weighting |

---

## Failure mode → REE component mapping

| Failure mode | Primary REE components implicated | Failure mechanism in REE terms |
|---|---|---|
| **Confabulatory Completion** | E1, RC loop | E1 generates plausible completions via coherence pressure; RC loop is absent or too weak to flag the mismatch. The system has no comparator strong enough to distinguish generation from retrieval. |
| **Belief Fixation** | E1, Control plane | E1 prior carries high precision weight; control plane fails to downgrade it when contradictory evidence arrives. E2 error signals cannot propagate into E1. The prior outweighs the update. |
| **Feedback Entrapment** | E1, Residue, Replay | E1 trains on its own outputs rather than ground truth; residue field updates from simulated outcomes rather than real consequences; replay consolidates errors. The self-conditioning loop has no external anchor. |
| **Shared Delusional Coupling** | E1 (multi-agent), RC loop | Two systems' E1 priors converge on a shared false attractor through mutual conditioning. Each system's RC loop is only weakly anchored to external ground truth and heavily influenced by the other system's output. |
| **Commitment Dysregulation** | E3, Control plane | E3 commit gate threshold miscalibrated. Too low: commits before evaluation completes (impulsive). Too high: evaluation loops without committing (paralysis). Control plane precision parameters govern the threshold. |
| **Provenance Collapse** | RC loop, Replay, E1 | RC loop fails to tag content with its source (real input, generated, retrieved, replayed). Replay episodes re-enter the real-consequence pipeline without hypothesis markers. E1 cannot distinguish live perception from recalled or generated content. |
| **Precision Misallocation** | Control plane, E3 | Control plane allocates high precision to low-information signals, or low precision to high-information signals. E3 receives a distorted confidence map and produces viability estimates that do not correspond to actual outcome distributions. |
| **Residue Blindness** | Residue | Residue field absent, disabled, or not connected to the decision-making pipeline. Post-commitment consequences do not accumulate. E3 has no persistent record of what past actions produced. Each decision is made as if prior consequences never occurred. |
| **Goal Proxy Lock-In** | E3, Residue, E1 | z_goal (E3's goal representation) becomes seeded on a proxy variable. The residue field and viability map are built around the proxy. E3 continues to optimise the proxy even when it has demonstrably diverged from the original objective. E1 world model reinforces the proxy-framed world representation. |

---

## REE predictions

REE's architecture makes specific predictions about failure susceptibility:

1. Systems lacking an RC loop (no explicit reality-testing comparator) are maximally
   vulnerable to Confabulatory Completion and Provenance Collapse.

2. Systems with high E1 prior precision and a weak E2 error propagation pathway are
   structurally predisposed to Belief Fixation, independent of training data quality.

3. Any system where the residue field updates from simulated rather than real outcomes
   will develop Feedback Entrapment — the training signal is contaminated by the system's
   own predictions.

4. Commitment Dysregulation is a precision problem, not a planning problem. The evaluation
   logic may be correct; the commit threshold is miscalibrated.

5. Residue Blindness and Goal Proxy Lock-In often co-occur: without persistent consequence
   tracking, there is no mechanism to detect when an instrumental goal has diverged from
   the terminal goal.

---

## Using REE interpretations without the full architecture

The REE interpretations in this taxonomy can be used selectively. If your system does not
implement REE explicitly, map the relevant component to its functional equivalent:

| REE component | Functional equivalent in other systems |
|---|---|
| E1 | Any persistent world model, context window, memory store, or embedding space |
| E2 | Any forward dynamics model, transition model, or next-token predictor |
| E3 | Any evaluation function, value head, policy head, or planner |
| Control plane | Attention mechanisms, temperature/sampling parameters, learned gating |
| RC loop | Grounding pipeline, retrieval verifier, uncertainty estimator |
| Residue | Accumulated reward history, harm penalty log, constraint violation counter |
| Replay | Fine-tuning, RLHF, experience replay buffer |
