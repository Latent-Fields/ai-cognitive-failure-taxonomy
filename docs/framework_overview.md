# Framework Overview

## What this taxonomy is

A structured catalogue of failure modes in AI systems, organised by the architectural
conditions that produce them rather than by the outputs they generate.

The central claim: most AI failures that matter are not random or mysterious. They are
predictable consequences of specific architectural configurations interacting with specific
environmental conditions. Naming the architecture is more useful than naming the behaviour.

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
