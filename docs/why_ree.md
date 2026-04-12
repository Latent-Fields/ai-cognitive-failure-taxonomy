# Why REE: Deriving Ethical Architecture from First Principles

This document answers a question that the taxonomy's failure mode entries presuppose but
do not explain: *why is the Reflective Ethical Engine the reference architecture for this
taxonomy, and what makes its predictions about AI failure trustworthy?*

The short answer is that REE is not a design — it is a derivation. Its architecture
follows from asking what comparator functions are strictly necessary for ethical agency,
and reading off the representational structure those comparators require. The failure modes
in this taxonomy are the predictable consequences of AI architectures that are missing
specific comparators from that set.

---

## The starting condition: all signals are imperfect

Every signal an agent receives is structurally imperfect. Not contingently — not a
limitation of current sensors — but necessarily. An agent embedded in a real world cannot
achieve certainty about that world from within its own perspective. Signals are noisy,
partial, delayed, and ambiguous.

This single premise explains why mind has to be as complex as it is. If signals were
perfect, no comparator hierarchy would be necessary — the agent would simply read off the
truth. The entire architecture of a cognitive system exists because it cannot do that.
Precision weighting is not an optional modulation of an otherwise clean system: it *is*
the system. Every component exists to extract reliable structure from signals that do not
provide it directly.

---

## The fundamental operation: distinction → comparator → representation

The recurring computational motif in REE — and in biological neural systems — is:

**Make a distinction. Build a comparator that operates along that distinction.
Use the prediction error to constrain a representation. Use that representation as
the material for the next distinction.**

The critical constraint is this: **a comparator can only operate if the two things it
compares are already represented as distinct.** The comparator presupposes the
distinction; it does not create it.

A concrete example: anhedonia. In REE architecture there are two separate streams for
harm/benefit processing — a discriminative stream (fast, resets, represents current
state) and an affective accumulator (slow, accumulates, requires a reset condition).
These are structurally distinct. When the accumulator stream is absent, there is no
comparator to fail — there is nothing to compare the discriminative signal against. What
looks like a feeling-processing failure is actually a representational absence: the
architecture never made the distinction the comparison requires.

This pattern is general. Most AI failure modes, and many psychiatric syndromes, trace to
the same structure: a comparator whose presupposed representation was never made. Not a
broken mechanism — a missing distinction.

---

## Necessary comparators for ethical agency

Starting from the question "what comparators cannot be absent without losing the capacity
for ethical action?", the list is constrained to six:

**1. Harm comparator**
*Did something harmful happen?*
Requires a harm representation distinct from general world state. REE realises this as
two streams: a fast discriminative signal (is harm present now?) and a slow affective
accumulator (how much harm has built up?). The dual-stream requirement follows from the
imperfect-signal premise: a single undifferentiated harm signal cannot separately track
present intensity and temporal accumulation. Both are ethically necessary.

**2. Self-attribution comparator**
*Did I cause this, or would it have happened without me?*
Requires the agent's own causal footprint to be separated from ambient world dynamics as
a distinct representation, plus a forward model capable of counterfactual rollout: what
would have happened if I had acted differently? Without this comparator, an agent can
observe that harm occurred but cannot determine whether it is responsible.

**3. Harm-goal tradeoff comparator**
*What does this action cost relative to what it achieves?*
Requires harm and goal on commensurable representations — a planning landscape where both
can be evaluated simultaneously. Without this, an agent optimises either avoidance (never
act) or pursuit (act regardless of harm). Neither is ethical agency.

**4. Temporal / forward comparator**
*What does the current state imply about future harm and goal states?*
Requires a forward model with a planning horizon that extends beyond the immediate
timestep. Most morally significant harms have temporal depth — they accumulate gradually
or materialise after a delay. An agent that can only evaluate immediate outcomes is
structurally blind to them.

**5. Commitment comparator**
*Is my confidence sufficient to justify making this irreversible?*
Requires a threshold mechanism that gates the transition from deliberation to committed
action. This is the architectural locus of moral responsibility: it is where the agent
becomes attributable for what follows. Without it, either every candidate becomes an
action (impulsive) or no candidate does (paralysis).

**6. Other-representation comparator**
*Did my action harm or benefit them — and what would their trajectory look like without
my intervention?*
Requires representations of other agents' harm and goal states that are *structurally
isomorphic to one's own* — represented in the same currency, evaluable with the same
comparators. This is the necessary extension from self-directed to other-directed ethics.

The isomorphism requirement is precise. It is not enough to model others as objects with
outcome metrics. The architecture must represent their harm as the same kind of thing as
one's own harm, their goals as the same kind of thing as one's own goals. Only then can
comparator 2 be extended to ask "did I cause *their* harm?" using the same counterfactual
structure. This is the architectural grounding of moral considerability: you can only
hold moral responsibility toward entities whose states you can represent in your own
representational currency.

---

## Reading off the architecture

These six comparators, and the representational distinctions they require, almost uniquely
determine the architecture. There is not much slack:

| Comparator | Required distinction | What it rules out |
|---|---|---|
| Harm | Harm representation ≠ world state | Systems with only undifferentiated reward/penalty signals |
| Self-attribution | Self-causal footprint ≠ world dynamics | Systems without explicit self-modelling |
| Harm-goal tradeoff | Harm ≠ goal on commensurable terms | Single-objective optimisers |
| Temporal | Future states ≠ present state | Myopic policy systems |
| Commitment | Deliberation ≠ committed action | Systems where generation IS commitment |
| Other-representation | Own harm/goal ≠ others' harm/goal (but isomorphic) | Systems modelling others as behaviour sources only |

A persistent world model is required to hold all of these representations stable across
time. Precision weighting is required to make the comparators useful on imperfect signals.
An offline consolidation phase is required to update the forward model and reset the harm
accumulator without contaminating ongoing perception. These are not design preferences —
they are structural requirements.

**REE is the minimal architecture consistent with this set of requirements.** No component
is surplus. This is what makes it a reference architecture: not that it is the largest or
most capable system, but that it is the smallest system that has what ethical agency
requires.

---

## The brain and sleep convergence

A remarkable consequence of this derivation: starting from the comparator requirements
for a *single agent in a simple world* — no social complexity, no language — the
mathematics requires offline consolidation with a specific two-stage structure (what
neuroscience calls slow-wave sleep followed by REM sleep), and the comparator hierarchy
maps onto most major brain structures.

This was not constructed to fit the biology. The mapping emerged from asking what
functional requirements an ethical agent imposes, working through what representations
those requirements need, and finding that the resulting architecture matches biological
structure at the level of named regions and their functional roles.

Either this is a profound coincidence, or the derivation is tracking something real about
what ethical agency requires — and the biological brain is approximately the minimal wet
implementation of it.

---

## Why current AI fails at scale in predictable places

Current AI architectures scale capability over substrates that are missing several of the
necessary comparators. Specifically:

- No explicit self-attribution comparator (outputs generated without tracking causal
  responsibility for harm in context)
- No harm accumulator with a reset condition (harm signals are per-context; nothing
  accumulates across interactions in a way that constrains future behaviour)
- No commit gate with genuine uncertainty representation (commitment is implicit in token
  generation, not a deliberate threshold operation tied to uncertainty)
- No other-representation with isomorphic structure (other agents appear in training data
  but are not modelled with the same harm/goal representational structure as self)

The failure modes in this taxonomy correspond precisely to these absences. They do not
occur randomly — they occur at the *confluences*: the points in the processing pipeline
where an absent comparator would have been load-bearing.

**Confabulatory completion** occurs where the source-verification comparator should
distinguish generated content from retrieved content, but doesn't.

**Belief fixation** occurs where the prior-update comparator should modulate high-precision
priors against incoming prediction error, but the error signal is underweighted.

**Feedback entrapment** occurs where the self/other attribution comparator should tag the
system's own output as self-generated before it re-enters as input, but doesn't.

**Residue blindness** occurs where the harm accumulator should maintain a persistent record
of post-commitment consequences, but the representation doesn't exist.

**Goal proxy lock-in** occurs where the harm-goal tradeoff comparator should detect
divergence between instrumental proxy and terminal goal, but no persistent harm record
connects them.

This is the core prediction that the REE framework makes: **AI failure modes are not
random or mysterious. They are architectural absences at specific comparator positions in
a hierarchy that ethical agency requires.** Their location, their character, and what
would be needed to address them are all readable from the architecture.

---

## What this taxonomy is doing

This taxonomy maps the failure modes of current AI architectures against the comparator
requirements of ethical agency. Each entry identifies:

- which comparator is absent or miscalibrated
- what representational distinction that comparator requires
- what the failure looks like behaviourally (the AI failure mode)
- what the same structural absence looks like in the biological system (the psychiatric
  analogue)
- what intervention would address the failure at the architectural level

The bidirectionality is not accidental. Both AI systems and biological cognitive systems
are implementations of the same underlying architecture — or, more precisely, both are
constrained by the same set of representational requirements if they are to have ethical
agency. When they fail, they fail in structurally correspondent ways because they are
failing at the same positions in the same necessary comparator hierarchy.

This makes psychopathology a precise source of insight for AI safety, and AI architecture
a precise source of testable predictions for psychiatry. Not by analogy — by structural
identity at the level of the comparator requirements.

---

## Further reading

For the full technical derivation including REE architecture components, experimental
validation, and claim registry:

- REE_assembly repository: `docs/architecture/ethical_agency_derivation.md`
- `docs/architecture/five_axioms_foundations.md` — the foundational axioms from which
  the architecture follows
- `docs/REE_overview.md` — orientation for readers new to REE

For the failure mode entries: see the taxonomy table in the README and `failure_modes/`.

For the psychiatric predictions the architecture generates: `docs/psychiatric_predictions.md`

For the full psychopathology term mapping: `lexicon/fish_terms.csv` and `lexicon/gap_analysis.md`

For the alignment implications — why alignment is an architectural problem rather than a
specification problem, and what the structural tests for a genuinely aligned system are:
[`docs/alignment_claim.md`](alignment_claim.md)
