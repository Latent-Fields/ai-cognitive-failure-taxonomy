# Architectural Motifs

These motifs are the building blocks used to explain failure modes in this taxonomy.
A failure mode typically requires two or more motifs to be present simultaneously.

---

## Motif table

| Motif | Definition | Systems that exhibit it | Role in failures |
|---|---|---|---|
| Persistent state | The system carries representational content forward across interactions, episodes, or training steps | LLMs with memory, RL agents, fine-tuned models | Enables accumulation of false beliefs; makes errors self-perpetuating |
| Self-conditioning | System outputs influence its own future inputs or training signal, directly or indirectly | RLHF-trained models, self-play agents, RAG with model-generated indexing | Amplifies initial biases; creates closed feedback loops with no external correction |
| Coherence pressure | Internal consistency constraints cause the system to fill gaps, suppress anomalies, or reject corrective signals in order to maintain a coherent representation | Autoregressive LLMs, predictive processing architectures | Confabulation, belief fixation, resistance to correction |
| Weak comparator | The system lacks a mechanism to reliably detect mismatches between generated content and ground truth, or between prediction and input | Systems without explicit uncertainty estimates, LLMs without grounding | Confabulation, provenance collapse, false confidence |
| Planning loops | The system generates candidate action sequences, evaluates them against a criterion, and commits to one — with a threshold governing when commitment fires | RL agents, tree-search systems, any system with deliberate trajectory selection | Commitment dysregulation (threshold too low or too high); goal proxy lock-in when the evaluation criterion drifts |
| Precision miscalibration | The system allocates confidence (precision, attention, weighting) disproportionately — either too high on unreliable signals or too low on informative ones | Attention-based models, Bayesian/free-energy architectures, any system with learned weighting | Hypervigilance-like patterns (over-attending noise), psychosis-like lock (high confidence on faulty priors), anhedonia-like patterns (under-attending informative signals) |

---

## Motif combinations and the failure modes they produce

| Motif A | Motif B | Failure mode(s) |
|---|---|---|
| Persistent state | Coherence pressure | Belief Fixation |
| Persistent state | Self-conditioning | Feedback Entrapment |
| Persistent state + Self-conditioning | (across multiple systems) | Shared Delusional Coupling |
| Weak comparator | Coherence pressure | Confabulatory Completion |
| Planning loops | Precision miscalibration | Commitment Dysregulation |
| Weak comparator | Persistent state | Provenance Collapse |
| Precision miscalibration | Planning loops | Precision Misallocation |
| Persistent state | Absent consequence tracking | Residue Blindness |
| Persistent state | Planning loops | Goal Proxy Lock-In |

---

## Notes on motif boundaries

**Persistent state vs self-conditioning.** Persistent state means the system carries content
forward; self-conditioning means that content influences what the system learns or predicts
next. Both can be present independently. A system can have persistent state without
self-conditioning (read-only memory), or self-conditioning without persistent state
(stateless but trained on its own outputs).

**Coherence pressure vs weak comparator.** Coherence pressure is active: the system
generates content to maintain consistency. A weak comparator is passive: the system
simply lacks the mechanism to detect when generated content is wrong. They interact:
a strong comparator can partially counteract coherence pressure; a weak comparator makes
coherence pressure failures invisible.

**Precision miscalibration scope.** This motif covers two directions: over-precision on
unreliable signals (hypervigilance analog) and under-precision on reliable ones (anhedonia
analog). Both produce planning failures, but through different mechanisms. The direction
matters for mitigation.
