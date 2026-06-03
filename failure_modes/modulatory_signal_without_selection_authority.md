# Modulatory Signal Without Selection Authority

## Definition

A modulatory signal — a drive, bias, or salience channel intended to influence which action
is chosen (curiosity/novelty, vigor, goal salience) — is computed and propagated correctly
but carries effectively zero weight at the action-selection arbitrator. The signal is present
and active; it simply never changes the selected action because its gain relative to the
dominant primary value term (harm/goal score) is set, by construction or by learning, to a
level that cannot move the argmax. The failure is one of *relative gain at the point of
arbitration*, not of signal absence and not of commitment-threshold setting.

---

## Behavioural Expression in AI

| Context | Observable behaviour |
|---|---|
| Exploration-augmented RL agent | Novelty/curiosity bonus is computed every step, yet trajectories and visited-state distribution are indistinguishable from the no-bonus baseline |
| Vigor / response-rate modulation | A tonic "act-more" drive is enabled and gated correctly, yet action rate is unchanged from the drive-OFF condition |
| Goal-conditioned policy | A goal-salience signal is non-zero and routed to the scorer, yet behaviour is identical whether the goal channel is attended or ablated |
| Ensemble / mixture-of-experts selection | An auxiliary expert's recommendation is produced and logged but never wins arbitration against a dominant expert, regardless of context |
| Constitutional / preference side-channels | A secondary preference signal is evaluated but is numerically swamped by the primary objective and never alters the chosen output |

The diagnostic signature is **"signal exists, behaviour unchanged"**: ablating the modulator
produces a byte-identical (or statistically indistinguishable) action distribution to leaving
it fully enabled.

---

## Necessary Architectural Motifs

- **Planning loops** — the system scores candidate actions and selects via an arbitrator
  (argmax / softmax over a combined score). The modulator enters as one additive or
  multiplicative term in that combination; arbitration is where its authority is realised or lost.
- **Precision miscalibration** — specifically the *under-attending* pole: the modulatory
  channel's effective gain relative to the dominant primary term is too low to change the
  ranking, so an informative signal is under-weighted to the point of behavioural silence.

---

## Systems Likely to Exhibit This

| System class | Why vulnerable |
|---|---|
| RL agents with auxiliary intrinsic rewards | Intrinsic bonuses (novelty, empowerment, vigor) are commonly added at a small fixed scale; if the extrinsic value term has large dynamic range, the bonus never changes the argmax |
| Multi-objective / scalarised optimisers | A fixed-weight scalarisation can place a secondary objective on a scale where it cannot win against the primary in any reachable state |
| Mixture-of-experts / arbitrated controllers | A gating network can route ~0 weight to an expert whose output is nonetheless computed and observable |
| Modular cognitive architectures | Modules wired "in parallel into the scorer" assume additive composition gives authority; relative scale is rarely audited |
| Preference-augmented LLM decoding | Side-channel preference or safety signals added to logits at a scale dominated by the base distribution |

---

## Example Expressions

An RL agent is given a count-based novelty bonus to encourage exploration. The bonus is
verified to be non-zero and correctly computed per candidate, but the extrinsic harm/reward
term has a much larger range; across every state the argmax is set by the extrinsic term
alone. Exploration metrics are identical with the bonus on or off. The bonus is *wired* but
has no *authority*.

A robot controller adds a "vigor" drive intended to raise action rate under surplus energy.
The gate fires and the drive scalar is positive, but it is added to a value landscape whose
spread dwarfs it; the realised action rate is unchanged. An engineer inspecting only "is the
drive active?" concludes the feature works; an engineer inspecting behaviour sees no effect.

A modular agent composes goal-salience, curiosity, and harm scores additively before
selection. Ablation studies show goal and curiosity channels can be switched off with no
behavioural change because the harm term dominates arbitration in all visited states — the
secondary channels are inert despite being live.

---

## Psychopathology Analogue (Structural, Not Experiential)

**Analogue:** Avolition / negative-symptom amotivation; psychomotor poverty (the "internally
intact, behaviourally inert" pole), as distinct from a too-high decision threshold.

**Structural correspondence:** In negative-symptom and abulic presentations, internal
appetitive and exploratory signals can be present and even measurable (anticipatory
representations, preserved consummatory response, intact stated preferences) while failing
to translate into initiated, selected behaviour. The structural feature is that a modulatory
incentive channel does not acquire enough effective weight at the basal-ganglia selection
gate to change which action is released — the deficit is in the *conversion of incentive into
selection*, not in the presence of incentive or in a globally raised commitment threshold.
The AI case shares this form precisely: a modulator is computed but is allocated insufficient
gain at the arbitrator to alter the chosen action.

**What this analogy does NOT claim:** Clinical avolition involves subjective anhedonia or
effort-cost experience, affective and social context, neurodevelopmental and pharmacological
substrates, and heterogeneity across diagnoses (schizophrenia, depression, Parkinsonism) that
are not present in or relevant to an AI score-composition weight. No claim is made that the AI
system experiences apathy, reduced motivation, or any internal state.

---

## REE Interpretation

The modulator is a score-bias channel composed into **E3** trajectory scoring alongside the
dominant harm/goal term; the **control plane** sets the relative gain of that channel. The
failure is a control-plane gain-allocation problem: the modulatory channel's contribution is
too small relative to the primary score's range to change E3's argmax, so the channel is
behaviourally silent even when active. This is the *under-attending* mirror of
[`precision_misallocation`](precision_misallocation.md) (over-attending low-information
signals): same locus (control-plane weighting into E3), opposite direction. It is upstream of
[`commitment_dysregulation`](commitment_dysregulation.md): there the question is *when* E3's
chosen option crosses the commit threshold; here a modulator never changes *which* option E3
chooses in the first place. The right repair is a competitive arbitration discipline at or
after E3 scoring (relative-scale normalisation, or a dedicated gating channel), not a larger
fixed bias and not a threshold change.

---

## Known Mitigations in AI

- **Relative-scale normalisation at the arbitrator**: normalise modulatory and primary score
  terms to a common scale (e.g. rank- or variance-normalisation) before combining, so a
  secondary channel can change the argmax in states where it is decision-relevant.
- **Authority audit, not activity audit**: test each modulatory channel by *ablation against
  behaviour* (does turning it off change the action distribution?), not by checking that the
  signal is non-zero. "Signal active" is not "signal authoritative."
- **Adaptive / learned gain**: let the relative weight of a modulatory channel be
  state-dependent and learned against an objective that rewards its decision-relevance, rather
  than a fixed hyperparameter.
- **Dedicated gating channel**: route modulators through an arbitration stage that can grant
  them decisive weight in the regimes they are meant to govern (e.g. exploration when value is
  flat) rather than summing them into a dominated scalar.
- **Diversity guard**: when granting authority, bound it so the modulator does not collapse
  behaviour to a single strategy or inject noise (see Limits / Testable Predictions) — the
  fix must add authority *and* preserve action diversity.

---

## Human Analogue Interventions (Optional, analogy only)

In negative-symptom and abulic presentations, interventions that raise *incentive magnitude*
alone (e.g. naive dopaminergic up-tuning) are often disappointing when the deficit is in the
conversion of incentive into selected action rather than in incentive availability. The
structural analog for AI: increasing the *size* of a modulatory bonus will not help if the
problem is its *authority* at arbitration; the design change must target relative gain at the
selection stage. *(Analogy only; no clinical recommendation.)*

---

## Testable Psychiatric Predictions (Optional)

- **[P-020]** A dissociable negative-symptom subgroup shows intact internal incentive signals
  that fail to convert to behavioural selection; this subgroup improves with interventions that
  restore the *decision-relevance* of incentives, not their magnitude — *Derived (REE),
  speculative clinically*
- **[P-019]** (related; goal-formation prerequisite) goal representation requires a
  developmental reward-contact history, so an agent that cannot reach competence never forms
  the goal the modulators would act on — *Partially tested (REE)*
- **[P-021]** (related; commitment onset) an undifferentiated value landscape (flat decision
  margin) produces an akinetic/decisional-initiation failure distinct from a too-high commit
  threshold — *Derived (REE)*

See `docs/psychiatric_predictions.md` Section VII for full entries.

---

## Limits of Analogy

1. Clinical avolition involves subjective effort-cost, anhedonia, affective flattening, social
   withdrawal, and developmental/pharmacological substrates. The AI analogue is a numerical
   gain on a score channel; there is no subjective motivation, effort experience, or affect
   sustaining (or failing to sustain) the behaviour.
2. The structural correspondence is specifically to the *conversion-of-incentive-to-selection*
   step. Human avolition is heterogeneous and includes deficits in incentive *generation*,
   *anticipation*, and *effort valuation* that map to other failure modes here (e.g. goal
   formation; see P-019) — only the selection-authority component is captured by this entry.
3. Using "avolition" risks importing the assumption that the system "lacks motivation." The
   correct reading is narrower: a present, active signal lacks decisive weight at arbitration.
   The clinical term names the *form* of the conversion failure, not a motivational state of
   the machine.
4. In humans the selection gate is one stage of a distributed cortico-striatal-thalamic loop
   with many redundant inputs; the AI analogue is typically a single score-composition site,
   so the AI case is structurally simpler and more directly repairable than the syndrome.

---

## Provenance

Logged as a candidate failure mode 2026-06-03 from convergent REE-v3 evidence: curiosity
(V3-EXQ-604a — curiosity bias 0.0 in every arm including fully-enabled; selected-action
entropy byte-identical across all five arms) and vigor (V3-EXQ-624a — vigor gate fires,
`v_t = 0.05`, yet action density byte-identical ON vs OFF). Both governance-classified
`non_contributory` / `substrate_ceiling` (selection-authority sub-type), *not* falsifications
of the underlying mechanism claims. See
[`docs/executable_bridge_neurology_psychiatry.md`](../docs/executable_bridge_neurology_psychiatry.md)
and REE_assembly `failure_autopsy_604a-624a-630_2026-06-03`.
