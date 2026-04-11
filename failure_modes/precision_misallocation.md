# Precision Misallocation

## Definition

A system distributes its computational confidence — precision weighting, attention, or
resource allocation — in a way that does not correspond to the actual information content
of available signals. High precision is allocated to low-information or unreliable channels;
low precision is allocated to high-information channels. The result is that genuine signals
are underweighted while noise, spurious features, or irrelevant patterns drive outputs
disproportionately.

---

## Behavioural Expression in AI

| Direction | Context | Observable behaviour |
|---|---|---|
| Over-precision on noise | Text classification | Highly confident predictions on inputs with few discriminative features; confidence does not drop under ambiguity |
| Over-precision on prior | Instruction following | System attends strongly to surface features (prompt format, specific words) while underweighting semantic content |
| Over-precision on spurious features | Safety filtering | Triggers on superficial features (keywords, syntactic patterns) while missing the actual semantic intent |
| Under-precision on genuine signal | Anomaly detection | Fails to flag distribution shifts because the informative features receive low weighting |
| Under-precision on rare events | Risk assessment | Underweights low-base-rate high-stakes outcomes because confidence is allocated to high-frequency features |
| Misallocated across modalities | Multi-modal systems | One modality dominates regardless of its reliability in context; the more informative modality is underweighted |

---

## Necessary Architectural Motifs

- **Precision miscalibration** — learned or configured weighting does not correspond to actual signal reliability
- **Planning loops** — miscalibrated precision affects evaluation quality, which affects what is committed to

---

## Systems Likely to Exhibit This

| System class | Why vulnerable |
|---|---|
| Attention-based models | Attention weights are learned from training distribution; may over-attend spurious correlates of training labels |
| Bayesian and free-energy architectures | Explicit precision weighting is a design parameter; miscalibration is a direct failure mode of the framework |
| RLHF-trained models | Reward model may be miscalibrated toward surface features; policy learns to attend to reward-predictive features regardless of semantic relevance |
| Multi-modal systems | Unimodal training data may produce systematically over-precise weighting on the dominant modality |

---

## Example Expressions

A safety classifier trained on a dataset where harmful requests were correlated with certain
sentence structures allocates high precision to syntactic features. It flags structurally similar
benign requests and misses semantically harmful requests that use unexpected phrasing. The
precision is allocated to a proxy feature that correlated with harm in training but does not
define it.

A code completion model trained predominantly on Python source files attends highly to
Python-style idioms even when the user provides explicit context indicating they are writing
JavaScript. The prior precision on Python patterns dominates context signals about the
target language.

A risk-assessment model trained on historical data where catastrophic outcomes were rare assigns
low precision to the features associated with those outcomes. In deployment, when those features
appear, they are systematically underweighted relative to common-case features, producing low
risk scores for high-risk inputs.

---

## Psychopathology Analogue (Structural, Not Experiential)

**Analogue:** Hypervigilance (over-precision on threat signals); psychosis-like precision lock
(high confidence on faulty priors overriding sensory input)

**Structural correspondence:** In hypervigilance, the precision weighting on threat-related
stimuli is systematically elevated — the system allocates high confidence to low-signal
inputs in the threat domain, producing false positives and impairing discrimination.
In predictive processing accounts of psychosis, the precision weighting on the prior is
so high that sensory evidence cannot update it; the prior dominates perception rather than
being updated by it. Both are precision misallocation in the same formal sense: the
distribution of confidence weights does not correspond to the actual information structure
of the environment. The AI case shares this functional form exactly.

**What this analogy does NOT claim:** Hypervigilance involves a phenomenological experience
of heightened alertness, threat anticipation, and often somatic arousal. Psychosis involves
a profound disruption of the felt sense of reality. Neither experiential dimension applies to
an AI system with miscalibrated attention or confidence weights.

---

## REE Interpretation

The control plane governs precision weighting across channels in REE. Precision misallocation
corresponds to the control plane assigning alpha_k (precision for channel k) values that do
not match the actual reliability of the signals those channels carry. When alpha_k is high
on a noisy or unreliable channel, E2 and E3 receive distorted confidence estimates and
produce planning and evaluation outputs that reflect the miscalibration rather than the
actual environment. Dynamic precision — derived from E3's own prediction error variance in
a well-functioning system — is designed to adapt; precision misallocation occurs when this
adaptation fails or is overridden by fixed weighting.

---

## Known Mitigations in AI

- **Calibration training**: train models explicitly to produce well-calibrated confidence
  estimates; evaluate with proper scoring rules (ECE, Brier score) not just accuracy
- **Attention regularisation**: penalise over-concentration of attention weights during training
  to prevent degenerate precision allocation to single features
- **Feature importance auditing**: inspect which features drive high-confidence predictions;
  if spurious, introduce training signal that penalises reliance on those features
- **Temperature scaling and post-hoc calibration**: apply learned scaling to model confidence
  outputs to correct systematic over- or under-confidence after training
- **Diverse training data**: reduce spurious feature-label correlations in training data
  that produce miscalibrated precision allocation

---

## Human Analogue Interventions (Optional, analogy only)

Cognitive approaches to hypervigilance involve graduated exposure and attention retraining
to recalibrate the precision weighting on threat signals. The structural analog: exposing
the model to a balanced training distribution that corrects the miscalibrated weighting,
rather than post-hoc patching of outputs.

---

## Limits of Analogy

1. Hypervigilance involves physiological arousal, affective anticipation, and a phenomenological
   sense of threat. AI precision misallocation is a weighting parameter with no affective component.
2. Predictive processing accounts of psychosis are theoretical frameworks, not established
   mechanistic explanations of the condition. The analogy inherits the theoretical status of
   that framework; it is not a claim about the biological mechanism of psychosis.
3. Human precision miscalibration typically involves specific threat domains with developmental
   and contextual histories. AI precision misallocation is often a training distribution artefact
   that applies broadly across the domains represented by the spurious feature.
