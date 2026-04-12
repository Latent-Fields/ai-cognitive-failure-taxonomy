# Pain Architecture: Accumulator Model vs Signal Model

*This document develops the architectural treatment of pain suggested by the bidirectional
structure of the taxonomy. The core claim is that the affective component of pain is not
a signal that fails to extinguish — it is a consequence accumulator whose reset condition
must be met. This reframe changes the level at which clinical intervention is targeted.*

*Testable predictions derived here are formalised in `docs/psychiatric_predictions.md`
(P-011 through P-016).*

---

## The signal model and its limits

The dominant clinical framing of pain is a signal model: nociceptive input arrives,
is processed, and produces a pain experience. Chronic pain, on this model, is a signal
that continues when it should have stopped — either because the nociceptive input
persists (tissue damage, inflammation) or because the signal processing has been
pathologically altered (central sensitization, altered descending modulation).

This model fits acute pain well. It fits chronic pain poorly. Chronic pain frequently
persists after tissue healing, does not respond proportionally to nociceptive input
reduction, responds to interventions that do not directly affect the nociceptive signal
(sleep, physical activity, acceptance-based therapy), and is strongly associated with
affective and motivational disturbance in a way that intensity alone does not explain.

The signal model has no principled account of why these interventions work, why pain
and depression co-occur so specifically, why sleep deprivation amplifies pain and sleep
restoration reduces it, or why the "pain without suffering" dissociation is possible
and clinically reproducible.

---

## The two-stream architecture

The REE architecture separates harm into two streams with distinct computational roles:

### z_harm_s — Discriminative stream (A-delta analog)

| Property | Value |
|---|---|
| Speed | Fast (A-delta fiber analog) |
| Function | Localisation and intensity encoding: where, how bad, what kind |
| Temporal profile | Resets with removal of stimulus |
| Operator | Input-driven, not accumulating |
| Architectural role | Informs immediate avoidance; feeds z_harm_a as input |
| Disruption type | Central sensitization: precision miscalibration lowers detection threshold |

z_harm_s is the signal. It fires with nociceptive input and falls when input is removed.
It encodes the discriminative dimensions of pain: location, quality, intensity.
Interventions that reduce nociceptive input (NSAIDs, local anaesthetics, surgical
correction) target this stream.

### z_harm_a — Affective accumulator (C-fiber analog)

| Property | Value |
|---|---|
| Speed | Slow (C-fiber analog) |
| Function | Motivational update: "this environment is systematically dangerous; change strategy" |
| Temporal profile | EMA-accumulated; does NOT reset with stimulus removal |
| Operator | Driven by z_harm_s input but persists independently |
| Architectural role | Drives sustained avoidance; shapes VALENCE_WANTING terrain; feeds E3 viability estimates |
| Disruption type | Chronic affective pain: accumulator elevated; reset condition not met |

z_harm_a is not a signal. It is a running consequence record. Its job is to maintain
motivational pressure to change behaviour until sufficient evidence of safety accumulates.
An elevated z_harm_a after the nociceptive input has resolved is not a malfunction — it
is the accumulator doing its job in a context where the reset condition has not yet been
provided.

---

## The accumulator model

### What the accumulator is for

The discriminative stream answers: *is there harm now?* The accumulator answers: *is
this environment systematically dangerous?*

These are different questions requiring different information. The discriminative question
is answered by the current input. The environmental-safety question requires integrating
across many episodes and cannot be answered by a single event. An accumulator with a
reset condition is the correct architecture for this computation — not a signal.

### The reset condition

z_harm_a does not reset on removal of the nociceptive stimulus. It resets when:

1. **Offline recalibration** — the SWS→REM transition provides a zero-point
   recalibration of the harm-accumulator precision (MECH-204). This requires intact
   sleep architecture, specifically the serotonergic withdrawal phase of REM.

2. **Prediction disconfirmation at the environmental level** — sustained evidence that
   approach behaviour in this context does not produce harm at the predicted magnitude.
   This is not habituation (which reduces signal amplitude). It is disconfirmation of
   the environmental danger prediction.

3. **Benefit-terrain restoration** — sufficient benefit_exposure to rebuild the
   VALENCE_WANTING terrain. The accumulator's motivational pressure is partly modulated
   by the wanting/liking balance in the residue field. Collapsed benefit terrain amplifies
   the relative weight of harm signals.

### Why "stuck" is the wrong frame

Patients and clinicians often describe chronic pain as an alarm stuck in the on position.
This framing imports the signal model — the pain *should* have turned off; something
is preventing it.

The accumulator model reframes this: the accumulator is functioning correctly. It is
maintaining motivational pressure to change behaviour because the reset condition has
not been met. Asking why the alarm doesn't turn off is the wrong question. The right
question is: what reset condition is required, and why is it not being provided?

This is not merely semantic. It changes the intervention target from *suppressing the
signal* to *providing the reset condition*. Suppressing the signal (opioids,
neuromodulators) temporarily reduces z_harm_a activity but does not provide the reset
condition — the accumulator returns to its prior state when the suppression is removed.
Providing the reset condition (sleep architecture restoration, graded activity,
acceptance-based approaches) changes the accumulator's state durably.

---

## The bidirectional insight

The signal model was developed from clinical observation without a formal architecture.
The REE architecture was developed for AI without reference to the pain literature.
The correspondence between them is therefore not circular.

When the two are placed in contact:

**From the AI architecture:** the need for two streams with different temporal profiles
falls out of the computation. A single harm signal cannot simultaneously encode
"here, now, this bad" (requires fast reset) and "this environment is dangerous"
(requires persistence across many episodes). These are computationally incompatible
requirements for a single signal. Two streams are a necessary consequence of the
architecture, not an empirical discovery.

**From the clinical literature:** the two-component model of pain (sensory-discriminative
and affective-motivational, per Melzack & Casey 1968) is well-established empirically
but has lacked a formal account of *why* the components are separate and what each one
is specifically computing.

**The bidirectional contact produces:** a formal account of the separation (the two
computations are incompatible in a single signal), a characterisation of what each
component is computing (current danger vs environmental danger), and a derived account
of when each component fails and why.

This contact also surfaces something neither direction noticed alone: the reset condition
for the affective accumulator is not the cessation of input. It is a positive condition
that must be actively met. Clinical pain management has focused heavily on reducing
input (analgesics, neuromodulation, surgery). The accumulator model explains why these
approaches often produce partial and temporary relief: they are not targeting the
component that is sustaining the chronic state.

---

## Architectural failure modes and their clinical correlates

| Failure mode | Architectural description | Clinical correlate |
|---|---|---|
| **Discriminative sensitization** | Precision miscalibration on z_harm_s input: detection threshold lowered; subthreshold stimuli produce suprathreshold responses | Central sensitization; allodynia; hyperalgesia |
| **Affective accumulation without reset** | z_harm_a elevated; reset condition not met (sleep disruption, insufficient benefit exposure, prediction not disconfirmed) | Chronic affective pain; pain unpleasantness persisting after tissue healing |
| **Precision-loop amplification** | High precision weight on z_harm_a feeds back into E3 viability estimates; harm signals dominate planning; benefit signals underweighted | Pain catastrophizing; pain-related disability disproportionate to intensity |
| **Maintenance loop entry** | z_harm_a elevation suppresses benefit exploration → benefit_exposure below z_goal seeding threshold → motivational collapse | Co-occurring chronic pain and depression; anhedonia; loss of activity engagement |
| **Reset-mechanism disruption** | SWS→REM transition impaired; offline recalibration does not occur; z_harm_a accumulator never receives reset signal | Sleep-disrupted chronic pain; the bidirectional relationship between sleep pathology and pain chronification |
| **Prediction-disconfirmation deficit** | Avoidance prevents graded-activity evidence from accumulating; the accumulator is never shown that approach behaviour is safe | Fear-avoidance cycle; disability maintenance despite resolution of acute injury |

---

## Dissociations

The architecture predicts four clean dissociations. Where these are clinically observed,
they constitute evidence for the two-stream model. Where they are not yet systematically
documented, they are novel predictions.

### 1. Intensity without unpleasantness (z_harm_s intact, z_harm_a reduced)

Observed after: high-dose opioids, anterior cingulotomy, certain meditation practices,
frontal lobotomy (historical). Patients describe full awareness of pain location and
intensity with marked reduction or absence of the affective/motivational response —
"I can feel it but it doesn't bother me."

**Architecture:** z_harm_s firing normally; opioids or ablation targeting the
z_harm_a pathway or its downstream affective processing.

### 2. Unpleasantness without intensity (z_harm_s quiet, z_harm_a elevated)

Observed in: some fibromyalgia presentations, some chronic widespread pain, states
following trauma without ongoing tissue damage. The patient experiences persistent
suffering and motivational disruption without proportionate nociceptive input.

**Architecture:** z_harm_s at or near baseline; z_harm_a chronically elevated,
reset condition not met, persisting independently of current nociceptive signal.

### 3. Sensitization without affective chronification (z_harm_s threshold lowered, z_harm_a not elevated)

Observed in: some early inflammatory conditions, some post-surgical states, where
sensitization is present but the patient does not report significant suffering or
mood disturbance.

**Architecture:** Precision miscalibration on z_harm_s without downstream z_harm_a
accumulation — either because the sensitization is recent and the accumulator has
not yet integrated sufficient evidence, or because the reset mechanism is functioning
normally and recalibrating nightly.

### 4. Affective chronification without sensitization (z_harm_a elevated, z_harm_s normal threshold)

Observed in: some depression-first presentations that develop somatic pain; some
conversion/functional neurological presentations; some chronic pelvic or visceral pain.
QST shows normal thresholds; pain unpleasantness and motivational disruption are marked.

**Architecture:** z_harm_a accumulated from psychosocial harm history (MECH-201:
internally generated harm representations processed without hypothesis tag), not
from peripheral nociceptive sensitization.

---

## Treatment target mapping

| Intervention | Primary target | Architectural mechanism | Expected effect profile |
|---|---|---|---|
| NSAIDs, COX-2 inhibitors | Peripheral nociceptive input | Reduce z_harm_s driving input | Intensity reduction, proportional, duration-limited |
| Local anaesthetics | Peripheral nociceptive input | Block z_harm_s input | Rapid intensity reduction, temporary |
| Opioids | z_harm_a pathway / affective processing | Reduce affective weight of z_harm_a signal | Unpleasantness reduction more than intensity; accumulator state persists; returns on cessation |
| Sleep restoration (CBT-I) | Offline recalibration mechanism | Restore SWS→REM transition; provide accumulator reset signal | Selective z_harm_a reduction; unpleasantness and mood improvement; durable if sleep maintained |
| Graded activity | Prediction disconfirmation | Provide evidence that approach does not produce predicted harm; accumulator reset condition met | Durable z_harm_a reduction; may not change intensity; improvement maintained if activity maintained |
| ACT for pain | Precision weighting on z_harm_a | Reduce high-precision response to harm signals; decouple harm signal from avoidance requirement | Reduced catastrophising; improved function despite pain; changes relationship to signal rather than signal amplitude |
| Behavioural activation | Benefit-terrain restoration | Increase benefit_exposure; rebuild VALENCE_WANTING terrain; partially offset z_harm_a elevation | Concurrent mood and pain improvement via shared mechanism |
| Anterior cingulotomy (historical) | z_harm_a downstream processing | Ablate affective response to nociceptive input | Profound unpleasantness reduction; preserved intensity; no longer recommended due to irreversibility |

---

## Open questions

1. **What is the minimum reset-condition evidence required?** The architecture implies
   a threshold; graded activity protocols are empirically derived without knowing what
   the threshold is. A quantitative model of the reset condition would allow
   protocol optimisation.

2. **Are the two streams dissociable with non-invasive neuroimaging in real time?**
   fMRI BOLD distinguishes somatosensory cortex (z_harm_s) from anterior insula and
   ACC (z_harm_a candidates). Simultaneous tracking of both during pain modulation
   interventions would test the dissociation directly.

3. **What determines the direction of failure?** Why do some patients develop primarily
   sensitization (discriminative failure) and others primarily affective accumulation?
   The architecture suggests: reset-mechanism integrity (sleep), benefit-exposure
   availability (environment), and precision-weighting baseline (temperament, prior
   history).

4. **Can the reset condition be pharmacologically provided?** Sleep architecture
   restoration pharmacology (orexin antagonists, targeted SWS enhancement) could
   provide the reset signal without requiring behavioural change. This is a potential
   bridge for patients unable to engage with graded activity or ACT initially.

---

## References

- Melzack, R., & Casey, K.L. (1968). Sensory, motivational, and central control
  determinants of pain. In D. Kenshalo (Ed.), *The Skin Senses*. (Two-component model
  establishing the discriminative/affective distinction.)
- Turk, D.C., & Melzack, R. (Eds.). *Handbook of Pain Assessment*. (Clinical
  measurement of the two dimensions separately.)
- Woolf, C.J. (2011). Central sensitization: implications for the diagnosis and
  treatment of pain. *Pain*, 152(3 Suppl), S2-15.
- Harvey, A.G. et al. (2020). Sleep and pain. *Nature Reviews Neuroscience*.
  (Bidirectional sleep-pain relationship.)
- Vlaeyen, J.W.S., & Linton, S.J. (2000). Fear-avoidance and its consequences in
  chronic musculoskeletal pain. *Pain*, 85, 317-332. (Fear-avoidance model; prediction
  disconfirmation literature.)
- Eccleston, C., & Crombez, G. (1999). Pain demands attention. *Psychological Bulletin*,
  125(3), 356-366. (Attentional precision weighting in pain.)
