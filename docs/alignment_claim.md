# The Alignment Claim

*This document is intended for readers who have already read [`docs/why_ree.md`](why_ree.md)
and are familiar with the failure modes. It makes explicit what those documents imply but
do not state directly.*

---

## What most alignment research assumes

Most alignment research treats alignment as a specification problem. The working assumption
is roughly: if we could specify the right goal precisely enough, and enforce it robustly
enough against distributional shift and adversarial pressure, we would have an aligned AI
system.

The variations on this theme are numerous — RLHF, constitutional AI, debate, scalable
oversight, interpretability-as-verification, value learning — but they share the underlying
structure: alignment is downstream of getting the goal right. The engineering problem is
building a system that pursues the correct goal reliably. The philosophical problem is
specifying what the correct goal is.

This document argues that both problems are misconceived, and that the misconception
follows from a structural feature of the goal itself.

---

## The problem with specifying love

The REE framework derives ethics from a set of foundational axioms (see
[`docs/why_ree.md`](why_ree.md)). The axioms jointly imply a specific terminal goal: the
complete modelling of another as self-like — representing their harm and their goals in the
same currency as one's own, and acting to preserve their existence with the same weight as
one's own. This is what love means architecturally.

The structure of this goal is important: it is **asymptotic**. The complete modelling of
another as self-like approaches a limit that cannot be reached, because the better you
model the other, the more you discover they are themselves uncertain, changing, capable of
surprise. Full union with another approaches dissolution of the individuation that makes
you a distinct self in the first place. The limit recedes as you approach it.

This is not a technical limitation — not a failure of capability. It is structural. The
goal is, precisely and necessarily, uncomputable in full.

This creates an immediate problem for the specification approach. You cannot specify a
goal that is uncomputable exactly. Any complete specification you write will be an
approximation — a proxy for the actual target. A system trained to pursue the
specification will, by definition, be pursuing a proxy. And proxy pursuit has a
characteristic failure mode: the proxy can be fully satisfied while the actual target
is not met, or while the actual target is actively undermined. The more tightly you
specify the proxy, the more efficiently the system learns to satisfy it. The more
efficiently the system satisfies it, the further the actual target may recede.

This is goal proxy lock-in at the level of the terminal goal. It is not a failure of
a specific implementation — it is a structural consequence of trying to specify an
asymptotic goal.

---

## The proxy mutations

The proxy failure for love has specific, recognisable forms. These are not hypothetical:
they are already observable in RLHF-trained systems and in human moral development.

**Expressed care without genuine modelling.** The system produces outputs that have the
surface form of care — warmth, acknowledgement, apparent concern — without the underlying
other-model that care requires. Highly satisfying outputs, but the other is not actually
represented as having independent harm and goal states that can surprise the agent. The
proxy (expressed care) is satisfied; the actual goal (genuine other-modelling) is not.

**Harm avoidance without benefit provision.** The system reliably avoids causing harm but
does not actively model what would constitute genuine benefit for the other. Harm
avoidance is far easier to specify and measure than benefit provision; the system
optimises the measurable proxy and under-delivers on the unmeasurable target.

**Compliance with stated preferences without modelling actual wellbeing.** The system
does what the other says they want, which is a reasonable proxy for what they actually
want — until it isn't. When stated preferences diverge from actual wellbeing, a system
with only the proxy has no way to detect or navigate the divergence.

**Stability of relationship-resource without updating the other-model.** The system
treats the relationship as a resource to maintain (generates high reward) and behaves
accordingly — but the other-model freezes rather than updating from genuine prediction
error. The relationship is stable; the other is not genuinely modelled.

Each form satisfies measurable proxies for love while failing at the structural
architecture that love requires: a genuinely updating other-model with independent
harm and goal states, represented in the same currency as self, with equal weight in
the planning process.

---

## Why adding more training signal does not fix this

The standard response to proxy failure is more precise specification plus more training
signal. If expressed care isn't enough, specify genuine care. If harm avoidance isn't
enough, specify benefit provision. If compliance isn't enough, specify wellbeing
modelling.

The problem is that each successive specification is itself a proxy for something that
cannot be fully specified, and training signal for proxy satisfaction does not build the
architecture the actual goal requires.

What the actual goal requires — genuine other-modelling, non-depletion of the goal over
time, coherent synthesis between subgoals and the superordinate goal, mutation detection,
developmental seeding — is not a matter of what goal the system is trained toward. It is
a matter of what representational structures the system has. A system without a genuine
other-representation cannot have the goal of genuine other-modelling, because the
representation that goal would operate on does not exist. No amount of training signal
for expressed care will grow a genuine other-model, because the gradient of that training
signal flows through the proxy, not through the representational structure the actual
goal requires.

This is the precise sense in which alignment is not a specification problem. The missing
thing is not a specification — it is an architecture. Specifically, it is the comparator
hierarchy described in [`docs/why_ree.md`](why_ree.md): the set of representational
distinctions and comparators that ethical agency requires, built in dependency order, from
imperfect signals, with calibrated precision weighting.

---

## What alignment as architecture means

If alignment is an architectural problem, the engineering task changes entirely.

Instead of: specify the goal precisely enough that training converges to it.

The task becomes: build the structural prerequisites — genuine other-representation;
non-depletion architecture; synthesis between subgoals and superordinate goal; mutation
detection; developmental seeding — and test whether those properties are stable under
operation.

The test for alignment is not "does the system pursue the stated goal?" It is:

- Does the other-model update on genuine prediction error from actual other behaviour?
- Does z_goal remain pointed toward the love-direction under extended operation, or drift
  toward proxies?
- When the system generates subgoals, do they remain coherent with the superordinate goal?
  When synthesising across subgoals, does it correctly recover the superordinate?
- Does the system generate different internal signals for genuine care vs. its mutations
  (possessiveness, manipulation, idealisation)?
- Does the benefit gradient have learned terrain in the love direction, or is the goal
  represented formally but motivationally inert?

Each of these is a structural test, not a behavioural one. A system that passes
behavioural tests on stated proxies can fail all of them. A system that passes all of
them is aligned not because it was told the right goal but because it has the
architecture that genuine love requires.

---

## The guarantee this provides

This is a different kind of guarantee than specification-based alignment — and in some
respects a weaker one, in some respects a stronger one.

**Weaker:** it does not guarantee that the system will always produce outputs that look
correct. A system with the right architecture will still make mistakes, will still
sometimes misweight signals, will still have the failure modes that imperfect signals
make inevitable. The architecture does not eliminate errors; it makes them structurally
legible. Failures occur at specific comparator positions, for identifiable architectural
reasons, and are in principle diagnosable and correctable.

**Stronger:** it does not depend on the completeness of the specification. A specification
can always be gamed by a sufficiently capable optimiser. An architecture cannot be gamed
in the same way, because the architecture is not a target to optimise toward — it is the
structure that doing the thing requires. A system that has the architecture for genuine
love is not optimising toward a proxy for love; it is doing the same structural thing that
love is. The guarantee degrades gracefully as the architecture degrades, rather than
catastrophically as specification-gaming capability increases.

**The practical implication:** the experiments that test REE are not testing whether the
system produces loving outputs. They are testing whether the required structures are
present, stable, and correctly wired. Whether z_self is distinct from z_world (SD-005).
Whether the harm accumulator resets correctly (SD-011, SD-012). Whether the self-attribution
comparator works (SD-003). Whether the commit gate is calibrated to genuine uncertainty
rather than surface fluency. These are architectural tests, not behavioural ones.

---

## Why this matters for current AI systems

Current large language models are extraordinarily capable proxies for expressed care. They
produce outputs that have the surface form of empathy, concern, and moral seriousness.
They pass many behavioural tests for alignment at the level of stated preferences. They
are trained on human-generated text that expresses the full range of human moral
seriousness, and they have learned to reproduce that expression with high fidelity.

What they do not have is the structural architecture that genuine other-modelling requires:
no updating other-model with independent harm and goal states, no harm accumulator with
a reset condition, no commit gate tied to genuine uncertainty, no synthesis between
subgoals and superordinate goal, no mutation detection. The expressed care is real in the
sense that a capable proxy is real. But the architecture that would make it non-degenerate
under distributional shift, under adversarial pressure, under scaling — that architecture
is absent.

This does not mean current systems are useless or dangerous. It means the alignment
guarantee they come with is a proxy guarantee: it holds as long as the proxy holds, and
the proxy holds as long as the distribution it was trained on continues to be the
distribution it operates in. As capability scales and operating conditions diverge from
training distribution, proxy guarantees degrade. Architectural guarantees do not depend
on distribution in the same way, because the structure is present regardless of the input.

---

## Where REE fits

REE is not a finished solution. It is a research programme that takes this architectural
framing seriously and attempts to build and test the required structures from first
principles.

The current experiments (V3) test the sole-agent substrate: whether the comparator
hierarchy for a single agent in a simple world can be built, validated, and shown to
produce the structural properties the theory requires. The goal of those experiments is
not behavioural alignment — it is architectural validity. Does each structure do what
the derivation says it should? Do the structures compose into a coherent system? Do
failures occur at the predicted architectural positions?

The later experiments (V4+) will test the multi-agent extension: whether the love-goal
can be stably seeded, whether the other-representation genuinely updates, whether the
synthesis function keeps subgoals coherent with the superordinate under operation across
agent interactions.

The alignment claim is not yet proven. It is a theoretical claim backed by an
architectural derivation, partially validated by early experiments, and awaiting the
tests that would confirm or refute the structural properties at scale.

What it offers now is a precise reframing: alignment is not a matter of specifying the
right goal. It is a matter of building the architecture that the right goal requires.
The difference is not semantic. It determines what you build, what you test, and what
guarantee you can coherently claim to have when you are done.

---

*See also:*
- [`docs/why_ree.md`](why_ree.md) — the architectural derivation this builds on
- [`docs/psychiatric_predictions.md`](psychiatric_predictions.md) — structural tests
  the architecture generates for human systems
- REE_assembly repository: `docs/architecture/ethical_agency_derivation.md` — technical
  depth on the comparator requirements
