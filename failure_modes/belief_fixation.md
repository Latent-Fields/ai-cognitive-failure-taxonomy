# Belief Fixation

## Definition

A system maintains a prior belief, classification, or internal representation with excessive
precision, causing it to resist updating when contradictory evidence is presented. The state
persists not because the system has processed and rejected the counter-evidence, but because
the update pathway is structurally suppressed. The system continues to produce outputs
consistent with the fixed state regardless of subsequent input.

---

## Behavioural Expression in AI

| Context | Observable behaviour |
|---|---|
| Instruction following | Model maintains an initial incorrect interpretation of a task despite explicit corrections |
| Multi-turn dialogue | System reverts to earlier framing after ostensibly accepting a correction |
| Classification | Classifier maintains high-confidence label despite presentation of disconfirming features |
| Agent with memory | Agent continues acting on a superseded plan or fact despite receiving updated information |
| Fine-tuned models | Post-training beliefs resist correction by in-context instruction |

---

## Necessary Architectural Motifs

- **Persistent state** — a representation that carries forward and influences future outputs
- **Coherence pressure** — the system generates outputs consistent with the prior state, and reinterprets new evidence in light of the prior rather than updating to it

---

## Systems Likely to Exhibit This

| System class | Why vulnerable |
|---|---|
| Fine-tuned LLMs | Strong fine-tuning can encode beliefs with high effective precision; in-context correction may be insufficient to override them |
| RLHF-trained models | Reward shaping can create stable output attractors that resist correction |
| RL agents with learned value functions | Value function may encode a policy that treats prior environmental states as highly probable, delaying update |
| Memory-augmented systems | Memory store contains an entry that is retrieved with high salience; new information fails to update or displace it |

---

## Example Expressions

A customer-facing model asked to classify a user complaint as "billing" or "technical" returns
"billing" on the first pass. When the user clarifies the issue is a software bug, the model
acknowledges the clarification but continues to route the conversation through billing-resolution
steps, treating the correction as a mild perturbation on the prior classification rather than
a definitive update.

A fine-tuned medical information model trained heavily on one diagnostic pathway continues to
suggest that pathway despite the user providing clear features that exclude it. The model
verbally acknowledges the features but does not structurally update its recommendation.

An RL agent playing a navigation task has learned a strong prior that a previously rewarding
corridor leads to the goal. After the environment is modified, the agent continues to attempt
that corridor across many episodes, updating far more slowly than the evidence warrants.

---

## Psychopathology Analogue (Structural, Not Experiential)

**Analogue:** Overvalued ideas; delusion maintenance (descriptive psychopathology)

**Structural correspondence:** In psychopathology, an overvalued idea is a belief held with
abnormal persistence and intensity relative to the available evidence. A delusion is, among
other features, characterised by its resistance to correction despite clear counter-evidence —
not because the patient has processed and rebutted the evidence, but because the belief is held
with a precision that suppresses the update. The structural feature is high-precision persistence
in the face of corrective signals. The AI case shares this functional form: the system's prior
carries so much weight that E2-level error signals cannot propagate into E1 to modify it.

**What this analogy does NOT claim:** Delusions in humans involve a complex phenomenological
and affective context — the patient's experience of certainty, the emotional significance of
the belief, the social consequences of challenging it. None of these apply to an AI system
with a fixed prior. The AI case is purely a weighting problem; there is no experiential
dimension.

---

## REE Interpretation

E1 holds a prior representation with high effective precision. When E2 generates a prediction
error that would normally propagate back to update E1, the control plane's precision weighting
on that channel is insufficient to move E1. The update is structurally suppressed, not
evaluated and rejected. A well-calibrated system would downgrade E1's precision when error
accumulates; here, that recalibration fails. The RC loop may detect the mismatch but the
signal does not propagate.

---

## Known Mitigations in AI

- **Explicit belief state with updatable representation**: maintain beliefs as explicit,
  updatable data structures rather than implicit in model weights; allow targeted correction
- **Contrastive learning objectives**: train with objectives that explicitly penalise
  insensitivity to counter-evidence
- **Temperature and sampling diversity**: during evaluation of ambiguous inputs, higher
  temperature can partially counteract precision lock; not robust against strong priors
- **Meta-learning for belief updating**: train models on tasks that require rapid belief
  revision in response to explicit corrections
- **Retrieval-anchored updating**: use retrieved external evidence as a high-salience
  override on parametric prior, with explicit precedence rules

---

## Human Analogue Interventions (Optional, analogy only)

Cognitive approaches to overvalued ideas include Socratic questioning, motivational
interviewing, and hypothesis-testing tasks. The structural analog for AI systems is providing
the corrective input in a format the system has been trained to treat as high-salience (e.g.,
system-prompt-level instruction rather than in-context user message), reducing the effective
precision imbalance between prior and correction.

---

## Limits of Analogy

1. Human overvalued ideas and delusions are typically about emotionally significant content;
   affective loading contributes to their persistence. AI belief fixation occurs on any content
   domain where the prior is strong; there is no affective dimension.
2. Clinical interventions for delusions involve therapeutic alliance, graduated exposure to
   counter-evidence, and social context — all of which have no direct AI structural analog.
3. The analogy should not be taken to imply that fixed AI beliefs are equivalent in any way
   to the experience of delusional conviction in a patient.
