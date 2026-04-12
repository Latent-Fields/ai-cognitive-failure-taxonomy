# Framework Overview

## What this taxonomy is

A structured catalogue of failure modes at the intersection of AI architecture and clinical
psychopathology. The catalogue is explicitly bidirectional: psychiatric and psychopathological
concepts provide mechanistic precision for AI failure mode analysis; AI computational
implementations generate testable predictions about psychiatric illness states.

The central architectural claim: most AI failures that matter are not random or mysterious.
They are predictable consequences of specific architectural configurations interacting with
specific environmental conditions. Naming the architecture is more useful than naming the behaviour.

---

## Bidirectional utility

**From psychiatry to AI**

Clinical psychopathology has developed precise vocabulary for failure patterns in information
processing systems that purely technical AI language lacks. Terms like *confabulation*,
*perseveration*, or *precision misallocation* carry decades of mechanistic research about
what conditions produce the failure, what sustains it, and what interventions work at what
level. Importing these concepts into AI analysis provides that depth without requiring AI
researchers to independently derive it.

**From AI to psychiatry**

Computational implementations of these failure modes do more than label clinical constructs —
they operationalise them as generative mechanisms. Because the AI architecture makes the
mechanism explicit, it generates specific, falsifiable predictions about the human conditions:

- When an environmental condition will produce a motivational collapse vs not (P-001)
- Whether recovery will be linear or exhibit a phase transition (P-002)
- Which interventions will and will not work depending on where in the architecture the
  failure is located (P-003, P-009)
- What developmental disturbances produce which adult phenotypes (P-004, P-006)
- What clinical markers predict which offline processes are running (P-007, P-008)

These predictions are held to a different epistemic standard than structural analogies:
they are genuine hypotheses with specified clinical tests. See `docs/psychiatric_predictions.md`.

**Why this direction may matter for psychiatry**

Psychiatry currently lacks mechanistic biomarkers for most common conditions. It classifies
syndromes by symptom clusters, not by the underlying computational failure. A taxonomy that
maps syndrome clusters to specific architectural failure modes provides:
- A basis for mechanistically-targeted treatment selection (not just trial-and-error matching)
- A basis for predicting treatment response from pre-treatment markers
- A basis for identifying shared developmental pathways across apparently distinct conditions

None of this is established — it is the research programme the predictions invite.

---

## What this taxonomy is not

- Not a bug tracker. These are failure modes, not defects to be patched in isolation.
- Not a capability taxonomy. It does not classify what AI systems can or cannot do.
- Not a blame taxonomy. It does not attribute intent, negligence, or moral responsibility.
- Not a diagnostic manual. The psychopathology analogues are structural tools, not
  diagnostic categories. See `docs/psychopathology_usage.md`.

---

## Five dimensions

Each failure mode is characterised along five dimensions:

| Dimension | What it captures |
|---|---|
| **Behavioural expression** | What the failure looks like from outside the system |
| **Architectural motifs** | Which underlying structures are necessary for the failure to occur |
| **System classes** | Which AI architectures are most vulnerable |
| **Human analogue** | Structural correspondence to a clinical or cognitive construct (see constraints in `docs/psychopathology_usage.md`) |
| **Mitigation** | Known interventions at the architectural or training level |

---

## The architectural level of analysis

Behavioural descriptions of AI failure are necessary but insufficient. "The model
hallucinated" describes the output. It does not explain why some architectures hallucinate
under certain conditions and not others, or what would need to change to alter the failure
rate.

This taxonomy works at the level of:

- **Persistent state**: what the system carries forward across context windows or episodes
- **Self-conditioning**: when system outputs influence its own future inputs or training signal
- **Coherence pressure**: when internal consistency constraints override external correction
- **Comparator strength**: how robustly the system detects mismatches between prediction and input
- **Planning loop dynamics**: how the system generates, evaluates, and commits to action sequences
- **Precision allocation**: how the system distributes computational confidence across competing signals

These motifs are defined in `docs/architectural_motifs.md`.

---

## Relationship to REE

The Reflective Ethical Engine (REE) is a reference architecture that provides a well-specified
model of several of the motifs above. REE interpretations are included in each failure mode
entry because REE makes specific, testable predictions about where in an architecture a given
failure mode will manifest and what interventions would reduce it.

REE is not required to use this taxonomy. The architectural motifs apply to any sufficiently
complex AI system. REE interpretations are clearly labelled and can be read selectively.

See `docs/ree_mapping.md` for the full mapping.

---

## Scope

This taxonomy covers:

- Large language models (autoregressive, instruction-tuned, RLHF-trained)
- Multi-agent systems
- Reinforcement learning agents with learned value functions
- Retrieval-augmented generation (RAG) systems
- Any AI system with persistent state, planning loops, or self-conditioning dynamics

It does not attempt to cover:

- Simple classifiers or regression models without persistent state
- Narrow, stateless inference systems (though some motifs may apply at the population level)
- Hardware or infrastructure failures

---

## How to add a new failure mode

1. Copy `schema/failure_mode_template.md` to `failure_modes/<name>.md`
2. Fill all required sections
3. Verify the `Limits of Analogy` section is present if a psychopathology analogue is named
4. Update `docs/ree_mapping.md` with the new entry
5. Add a row to the taxonomy table in `README.md`
