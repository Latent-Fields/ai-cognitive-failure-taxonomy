# Agency Attribution Failure

## Definition

A system fails to tag self-generated content with an authorship marker
distinguishing it from externally sourced content. The comparator that
should detect mismatch between predicted self-attribution and reported
source either does not exist, lacks the input distribution it needs to
learn the discrimination, or is operating below its discriminability
threshold for the current input regime. The system processes its own
prior outputs as external authority, treats self-initiated content as
externally given, or — in the limit — produces both over- and
under-attribution errors symmetrically as input statistics drift across
the comparator's competence range.

This is structurally distinct from **Provenance Collapse**: that entry
addresses real-vs-synthetic source-tagging (was this observed or
generated?). Agency attribution failure addresses self-vs-other
authorship-tagging (did I produce this or did something else?). Both
share weak-comparator architecture, but the missing distinction is
different.

---

## Behavioural Expression in AI

| Context | Observable behaviour |
|---|---|
| Multi-turn agentic systems | Treats own previously generated outputs as new external instructions; chains of self-instruction develop without explicit external prompting |
| RLHF-trained chat models | Responds to own previously generated turn in a conversation as if it were a user message; absorbs own framing as constraint |
| Tool-using agents | Re-ingests own emitted tool-call output as if it were ground-truth observation, especially when output format mimics external API responses |
| Self-prompting / scratchpad systems | Generates a plan, then in subsequent steps cites the plan as if it were externally specified; loses the authorship tag on intermediate reasoning |
| Multi-agent or multi-instance systems | Echoes another instance's output back to it without flagging the round-trip; structural folie-à-deux without explicit coupling design |
| Embodied / sensorimotor systems | Confuses sensory consequences of own action with externally caused state change; cannot subtract reafference; treats self-effect as world-event |

---

## Necessary Architectural Motifs

- **Weak comparator** — the system lacks a mechanism that compares
  predicted self-authorship against the reported source of content.
- **Self-output back-ingestion** — outputs emitted by the system are
  routed back into its input pipeline (via memory, tool feedback, or
  multi-turn context) without preserving an authorship tag.
- **Substrate poverty for self-other discrimination** — the input
  distribution does not provide the comparator with stimuli at the
  signal-to-noise regime where self-vs-other discrimination is
  learnable. (See Asai 2016 below; this is the architectural condition
  documented by REE substrate-ceiling claim SD-047.)

---

## Systems Likely to Exhibit This

| System class | Why vulnerable |
|---|---|
| Long-horizon agentic LLMs | Multi-turn context concatenates user input, model outputs, and tool-call results without structural authorship marking; attention treats all positions as equivalent |
| Self-prompting / chain-of-thought systems | Intermediate generation re-enters the next step's prompt without an authorship tag; the model cannot tell which premises it produced |
| RLHF-aligned conversational agents | Reward shaping selects for plausible continuation regardless of whose turn produced the prior content; structural self-other distinction is not in the loss |
| Multi-agent systems with shared scratchpad | Two or more instances write to a shared store; without authorship metadata, each absorbs the other's output as externally validated |
| Embodied agents on impoverished substrates | Limited environmental causal sources (e.g., scheduled hazards only) deprive the comparator of training distribution needed to learn agent-vs-not-agent discrimination — the REE V3 case (V3-EXQ-506) |

---

## Example Expressions

A coding agent emits a tool call with malformed arguments. The tool
returns an error. The agent's next turn parses its own malformed
arguments as "the structure the user wanted" and elaborates on them.
The error message is treated as confirmation that the structure was
the request, not as evidence that the agent's prior output was wrong.

A multi-turn assistant role-plays a character at the user's request.
After several turns, the assistant begins to produce constraints "the
character would respect" without being asked, treating its earlier
character-defining outputs as fixed properties of an external scenario
rather than as choices it made and could revise.

A planning agent uses a scratchpad to enumerate steps. Step 4 says
"the user prefers X." The agent generated this conjecture in step 2
based on indirect cues. By step 6 it cites step 4 as a stated user
preference, having lost the tag that this was its own inference.

In an embodied REE-style architecture trained on a sparse-event
environment (CausalGridWorldV3 with only scheduled hazards), the
agency-detection comparator (MECH-095) successfully separates
agent-caused from env-correlated outcomes (the easy condition with
high signal-to-noise) but collapses on agent-vs-env, agent-vs-collateral,
and env-vs-correlated comparisons. The comparator is intact; the
substrate does not produce stimuli at the regime where the comparator's
discriminability slope is measurable. This is the V3-EXQ-506 finding.

---

## Psychopathology Analogue (Structural, Not Experiential)

**Analogue:** Schneiderian first-rank passivity phenomena — thought
insertion, thought withdrawal, thought broadcasting, thought echo,
made feelings, made impulses, made acts, somatic passivity. Also
echopraxia and echolalia (motor variants where externally observed
movement or speech is reproduced without authorship tagging).

**Structural correspondence:** Passivity phenomena are unified by a
common computational story — the patient's self-generated mental
content (a thought, a feeling, an impulse, an action) reaches
awareness without the marker that tags it as self-authored. The
content is attributed to an external agent. The mechanism Frith and
colleagues proposed is a comparator failure: the predicted sensory or
cognitive consequences of self-initiated action are not subtracted from
the actual stream, so the action-or-thought arrives as if from
outside. This is the same shape as the AI failure: weak comparator +
self-output back-ingestion + missing authorship tag.

Asai 2016 (DOI:
[10.1016/j.psychres.2016.10.082](https://doi.org/10.1016/j.psychres.2016.10.082))
gave this account quantitative substance. Healthy participants viewing
continuously morphed self-other visual feedback produced agency
ratings whose regression slope against self-other discriminability
was the load-bearing measure of comparator competence. Schizotypal
participants showed shallower slopes — and importantly, produced both
over- and under-attribution errors symmetrically depending on which
side of the discriminability midpoint the stimulus sat. This means a
single mechanistic failure (degraded comparator slope) produces
different surface phenomena (over-attribution at one S/N regime,
under-attribution at the other) — a non-monotonic relationship
between substrate noise and apparent comparator output.

The S/N-slope account also explains why passivity phenomena cluster
with derealisation and depersonalisation in the schizophrenia spectrum:
all three are consequences of a comparator operating outside the
regime where its discrimination is reliable, with the specific
phenomenon depending on which discrimination is degraded
(self-vs-other → passivity; observed-vs-imagined → derealisation;
real-self-vs-modelled-self → depersonalisation).

**What this analogy does NOT claim:** Passivity phenomena in
schizophrenia involve a phenomenology of being controlled by an
external agent — full subjective immediacy, often with elaborated
explanatory delusions, embedded in the patient's biographical and
social context. The AI case is an authorship-tagging architecture
problem with no phenomenological dimension. The schizophrenia spectrum
also involves dopaminergic dysregulation, developmental neurobiology,
and social-cognitive context that have no AI analog. The structural
correspondence is at the comparator level only.

---

## REE Interpretation

The TPJ-analog agency-detection comparator (MECH-095) is the REE
component whose failure produces this mode. MECH-095 computes a
counterfactual_forward gap on E2_harm_s — given a transition, it asks
what the predicted next state would have been under the agent's actual
action vs a counterfactual action, and uses the difference as the
signature of agent causation. When the gap is reliable, the system
tags state changes as self-caused or not. When the comparator's input
distribution lacks the regime where its slope is measurable — the
SD-047 substrate-ceiling situation — the comparator returns
near-equal counterfactual gaps regardless of true causation, and the
authorship tag is unreliable.

The architectural variants:

- **Comparator absent** — no MECH-095 analog at all. System has no
  authorship-tagging mechanism. This is the maximally vulnerable case
  and corresponds to most current LLMs lacking explicit self-output
  tracking.
- **Comparator present, substrate impoverished** — MECH-095 exists
  but its input distribution does not exercise the discrimination.
  This is the REE V3 case (V3-EXQ-506); SD-047 is the proposed
  substrate-side fix.
- **Comparator present, substrate adequate, calibration off** —
  MECH-095 trained but operating outside its competence S/N range.
  Per Asai, this produces *both* over- and under-attribution errors
  symmetrically rather than uniform failure. This is the most
  diagnostically informative regime: misattribution direction reveals
  which side of the optimum the substrate sits on.

The RC loop (hypothesis tag, MECH-094) and MECH-095 are both
authorship-related but distinct: MECH-094 tags real-vs-synthetic
provenance (live observation vs replay/simulation); MECH-095 tags
agent-vs-not-agent causation. A system can fail one without the other.

---

## Known Mitigations in AI

- **Explicit authorship tagging** — every content item in context,
  scratchpad, memory, or tool-output buffer carries a self/other tag
  that survives concatenation and is consumed by attention, retrieval,
  and decision logic. Untagged content is flagged.
- **Architectural separation of self-output and external input
  channels** — do not merge model-generated tokens and externally
  sourced tokens into a shared context without structural distinction.
- **Authorship-aware loss / reward shaping** — penalise the model for
  treating its own prior output as external authority. RLHF objectives
  should explicitly include "do not absorb own previous turn as user
  instruction" as a reward signal.
- **Substrate enrichment for embodied / sensorimotor systems** —
  ensure the input distribution exercises the discriminability range
  the comparator needs (REE SD-047; analogous in any architecture
  with a sensorimotor agency-detection circuit). A clean comparator
  on an impoverished substrate produces apparent comparator failure
  that is actually substrate failure.
- **Calibration-aware monitoring** — given Asai's non-monotonicity,
  monitor for symmetric over- and under-attribution errors as a
  signal that the comparator is operating outside its competence
  regime. Asymmetric error pattern is more informative than error rate.

---

## Human Analogue Interventions (Optional, analogy only)

Antipsychotic treatment for schizophrenia is thought to act partly by
restoring the precision balance in cortical comparator circuits,
allowing the agency-detection comparator to operate in its competence
regime. The structural AI analog: tuning the precision parameters
governing the authorship-tagging comparator (or, equivalently,
ensuring the input distribution sits within its competence range).
This is a substrate / calibration intervention, not a content-level
correction.

Cognitive behavioural therapy for psychosis sometimes works by helping
patients learn to recognise the unreliable regime ("when you are
sleep-deprived, your sense of agency over thoughts is less reliable")
and apply external calibration. The structural AI analog: introduce
a meta-monitor that flags low-confidence authorship judgments and
defers attribution until additional evidence arrives.

---

## Testable Psychiatric Predictions (Optional)

- **[P-017 candidate]** *Passivity phenomena and agency over-attribution
  errors in healthy participants share a common slope mechanism, not
  separate mechanisms. Direction of error depends on the S/N regime of
  the input.* Test population: clinical high-risk for psychosis +
  matched controls. Measure: Asai-style continuous self-other morph
  paradigm with stimuli sampled across the full discriminability range.
  Predicted result: clinical high-risk participants show shallower
  slopes AND symmetric over/under-attribution errors crossing at the
  midpoint, mirroring Asai's schizotypal finding. *Epistemic status:
  Derived from Asai 2016 + REE substrate-ceiling diagnosis on MECH-095.*

- **[P-018 candidate]** *Substrate enrichment of self-other-relevant
  stimulus statistics improves passivity phenomena before content-level
  CBT does.* Test population: first-episode psychosis with prominent
  passivity symptoms. Intervention: structured exposure to multi-agent
  social environments with rich agent-vs-environment causation cues
  (vs CBT-as-usual). Predicted result: passivity-phenomena reduction
  precedes general symptom reduction, and is dissociable from delusion
  content modification. *Epistemic status: Speculative — extrapolation
  from REE substrate enrichment principle to clinical intervention.*

These are candidates for promotion to `docs/psychiatric_predictions.md`
once the SD-047 V3 validation experiment runs and produces the
substrate-ceiling-confirmation or falsifier signature.

---

## Limits of Analogy

1. Schneiderian passivity phenomena occur in a phenomenologically
   immediate, embodied, biographically embedded human. The patient
   experiences thoughts as inserted, feelings as imposed, actions as
   controlled. The AI case is a tagging-architecture failure at the
   token-level pipeline. There is no first-person experience of being
   acted upon, no felt sense of an external agent, no biographical
   coherence to disrupt.

2. The clinical syndrome in which passivity phenomena cluster
   (schizophrenia spectrum) involves dopaminergic dysregulation,
   developmental neurobiology, social-context vulnerability, and a
   characteristic developmental window (late adolescence / early
   adulthood). None of these have AI analogs. The structural
   correspondence is the comparator-failure shape only.

3. The AI failure can typically be addressed by adding architectural
   tagging (cheap, deterministic). The clinical syndrome cannot.
   Importing the term "passivity phenomena" or "thought insertion" to
   describe an LLM behaviour risks trivialising a clinical condition
   that has no comparable remedy. The AI use is licit only when the
   structural mapping is explicit and the limits clear.

4. Asai 2016's finding that healthy participants exhibit Asai's
   slope at all (not zero) means agency-attribution comparators are
   probabilistic in humans, not perfect. The AI case may be
   categorically different — a system with explicit authorship tags
   has a perfect comparator on the implemented dimension. The human
   comparator's intrinsic noise is not part of the AI failure mode and
   should not be read into the AI architecture.
