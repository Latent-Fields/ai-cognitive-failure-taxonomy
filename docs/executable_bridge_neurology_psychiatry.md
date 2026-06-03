# Computer science as the executable bridge between neurology and psychiatry

*Conceptual note. Added 2026-06-03. Grounded in recent REE-v3 / REE_assembly failure-mode
analysis. Companion to [`framework_overview.md`](framework_overview.md),
[`why_ree.md`](why_ree.md), and [`ree_mapping.md`](ree_mapping.md).*

---

## Core thesis

Neurology and psychiatry describe the same organ from two ends and rarely meet in the
middle.

- **Neurology names substrates.** Basal ganglia, hippocampus, orbitofrontal and
  ventromedial prefrontal cortex, thalamocortical loops, dopaminergic vigor systems,
  hippocampal contextual representation. These are *parts and their wiring*.
- **Psychiatry names observed failure modes.** Catatonia, abulia, akinetic mutism,
  negative symptoms, perseveration, salience collapse, dissociation, impulsivity,
  mania, compulsion. These are *patterns of breakdown in the whole*.

The gap between them is an inference gap. Knowing a substrate does not tell you which
clinical syndromes it makes *possible*; knowing a syndrome does not tell you which
architecture had to exist for it to occur.

**Computer science can sit in that gap as an executable bridge.** If you build a control
architecture out of components that are deliberate analogues of neural substrates, and
you run it, then its *failure modes are observable, reproducible, and dissectible*. You
can then ask the bridging question precisely:

> What kind of architecture would have to exist for this clinical pattern to become a
> *possible* failure mode?

An executable system answers that question by exhibiting the pattern — or refusing to. A
syndrome you can only describe in humans becomes a syndrome you can instantiate, perturb,
and trace to a specific loop. That is the bridge: not metaphor, but a runnable
intermediate representation in which "substrate" and "syndrome" are the same object seen
at different timescales.

This is the same bidirectional commitment the taxonomy makes elsewhere (psychiatry → AI
for descriptive precision; AI → psychiatry for generative prediction), stated at the
level of the *neurology–psychiatry* gap rather than the AI-behaviour gap. This note is
written so it is legible to someone arriving from the AI cognitive-failure side: you do
not need REE internals. REE-v3 is simply the first system available that fails in a
clinically legible way, and it is used here as a worked example.

---

## Why the recent REE-v3 failures are clinically meaningful

REE-v3 is an experimental cognitive-motivational architecture: a world model, a
harm/benefit evaluator, a goal-representation pipeline, exploration ("curiosity") and
vigor drives, and a basal-ganglia-like selection-and-commitment loop that is supposed to
convert evaluated options into committed action.

Over recent weeks its experiments stopped failing in scattered, idiosyncratic ways and
began **converging on one failure shape**. Crucially, the governance process that
adjudicates these runs has *not* classified them as the architecture being wrong
(falsifications). It classifies them as `non_contributory`, `substrate_ceiling`, or
`measurement_test_design_defect` — *the claim was never given conditions under which it
could express itself* (2026-06-03 governance cycle, REE_assembly `master` commit
`0de956c449`, which applied six such autopsies and flagged two more for deep review).

That distinction is the point. A system that is *wrong* is not clinically interesting. A
system that is **internally active but cannot convert that activity into behaviour** is
clinically interesting, because that is precisely the form a large family of human
syndromes takes. The recent failures are meaningful because they are *specific*: each
localises to a different stage of the action-production pathway, and together they
describe a system that is assembled but underpowered at the point where representation
must become action.

---

## The "catatonic-like" action-release failure pattern

The metaphor that currently fits is **not** "unconscious," "dead," or "broken." The
internal machinery runs. Candidate trajectories are generated, harm and benefit are
evaluated, salience signals fire, drives are present and measurable. What fails is the
*final conversion* — turning a salient, evaluated option into a committed, executed
action.

That picture — internally active, representations and drives present, but unable to
release action — is the shape of **catatonia / abulia / akinetic mutism**. Not as a
diagnosis, but as a *control-architecture signature*: the loop that should select among
options and commit to one is underpowered, so the system idles in a high-entropy,
low-commitment state with its evaluative and motivational subsystems intact behind the
stall.

Three independent recent results triangulate this signature.

### 1. Goal representation forms under force, but starves ecologically

The goal pipeline is **not** simply unwired. Under forced supra-threshold input it forms
a goal representation (a substrate contract test produces a non-zero goal latent, and one
seed of the diagnostic run reaches `z_goal_norm_peak ≈ 0.19`). But run ecologically, the
goal latent stays at its zero initialisation on **all** measured cells. The reason is
upstream: the agent does not reliably reach survival/foraging competence (2 of 3 seeds
never develop a competent policy even on the easy curriculum stage — episode lengths of
~18–24 steps against a survival gate of 75), so it never accrues enough reward-contact /
benefit input to *form* the goal.

This is not a missing wire. It looks like **goal representation requiring a developmental
reward-contact history** — the computational echo of vmPFC/OFC incentive representations
that consolidate from the animal actually contacting and consuming rewards (Berridge's
wanting/liking distinction; here a `benefit_exposure` signal is the consummatory-contact
analog that feeds goal formation). An agent that cannot survive/forage never earns the
history that builds a goal. This is distinct from
[`goal_proxy_lock_in`](../failure_modes/goal_proxy_lock_in.md): there the goal is
*present and wrong*; here it is *absent because the contact history that would form it
never accrued*.

*Evidence: `failure_autopsy_V3-EXQ-603e-626a-622_2026-06-03` (REE_assembly).*

### 2. Modulatory drives exist but lack selection authority

Curiosity and vigor are present and gated correctly — and **do not change the chosen
action**.

- The curiosity substrate (MECH-314): its candidate-pool is confirmed action-divergent
  (the upstream collapse was fixed), yet the curiosity bias contributes **exactly 0.0**
  to selection *in every arm, including the fully-enabled one*, and the selected-action
  entropy is byte-identical (0.714553) across all five ablation arms.
- The vigor substrate (MECH-320 / ARC-068): its gate fires (`v_t = 0.05`), and yet action
  density is **byte-identical** between vigor-ON and vigor-OFF arms (0.865).

The pattern is "signal exists, behaviour unchanged." The modulatory channels are wired and
active but have **no selection authority** at the action-selection arbitrator — they are
swamped by the dominant primary (harm/goal) score term and never move the argmax. In a
brain, exploration and tonic-dopamine vigor are *selection-competitive* channels that can
override the exploit policy and set global response rate; a modulator that fires but
cannot change behaviour resembles an exploration/vigor signal **disconnected from the
basal-ganglia selection gate**.

*Evidence: `failure_autopsy_604a-624a-630_2026-06-03` (REE_assembly).*

> **Candidate new failure mode.** This "modulator fires, argmax unchanged" pattern is not
> commitment-threshold miscalibration (it is upstream of the threshold) and not goal
> proxy lock-in. It is a distinct shape — *modulatory signal without selection authority*
> — and is a candidate entry for `failure_modes/` under the repo's
> [contribution protocol](../README.md) (schema + `Limits of Analogy` + testable
> predictions). It is logged here rather than authored as a full entry to keep this note
> conceptual.

### 3. Commitment never naturally forms

The maintenance-time commitment-release mechanism (MECH-342) could not be tested at all,
because **the agent never naturally committed**. Its candidate scores are nearly tied —
mean decision margin `0.00074`, roughly **70× below** the commitment-admission floor
(`0.05`), and *identical* in healthy and degraded conditions. With undifferentiated option
values the commitment gate never admits the latch (`n_commit_entries = 0`,
`beta_elevated_occupancy = 0.0` throughout).

This is an **action-release / decisional-initiation failure**, not an absence of internal
processing. It maps onto the decision-confidence / value-margin signal that gates
commitment *onset* (LIP/PFC ramping to a decision bound): a persistently flat margin is an
agent whose options are never distinct enough for a committable decision to form. The
internal evaluator is running; the bound is never reached. In the taxonomy's terms this is
the **overcalibrated / paralysis** pole of
[`commitment_dysregulation`](../failure_modes/commitment_dysregulation.md) reached *not*
by a too-high threshold but by a too-flat value landscape — a mechanistically distinct
route to the same "evaluates without committing" surface behaviour.

*Evidence: `failure_autopsy_V3-EXQ-629_2026-06-03` (REE_assembly).*

> A related "wired but inert" instance from the diversity side: the
> crystallization-necessity retest (V3-EXQ-610c) found its crystallization step to be a
> behavioural no-op because the policy is never trained
> (`failure_autopsy_V3-EXQ-610c_2026-06-03`). Same family, harness-level proximate cause.

Put together: an evaluator that works, drives that fire, goals that *can* form — and a
basal-ganglia-like selection-and-commitment loop too weak to give any of it authority over
action. That is the catatonic-like / abulic signature.

---

## Mapping table: computational failure → clinical analogue → neurofunctional loop → REE evidence

| Computational failure | Clinical analogue | Likely neurofunctional loop | REE evidence / example |
|---|---|---|---|
| Goal latent forms under forced input but stays at zero-init ecologically; the agent never accrues reward-contact history | Avolition / anhedonic negative symptoms; impoverished incentive representation | vmPFC / OFC incentive representation + ventral-striatal / mesolimbic reward-contact loop (goal forms from consummatory history, not from wiring alone) | 603e/626a/622 goal-stream cluster: goal latent `= 0` on all 15 cells ecologically; forms (~0.19) only under forced benefit+drive; 2/3 seeds never foraging-competent. `non_contributory` / `substrate_ceiling`, `pending_retest_after_substrate` |
| Modulatory drive (exploration) fires but contributes 0 to the chosen action | Abulia / negative-symptom amotivation: drive present, behaviour flat | Frontopolar / ventral-striatal exploration channel → **basal-ganglia selection gate** (the override never reaches the arbitrator) | 604a: curiosity bias `0.0` in every arm incl. ALL_ON; selected-action entropy identical across all arms |
| Modulatory drive (vigor) gate fires but response rate is unchanged | Psychomotor retardation / akinesia with intact tonic motivation | Tonic-dopamine vigor → motor-gain coupling at the striato-pallidal gate (vigor scalar with no coupling to action rate) | 624a: `v_t = 0.05` fires, action density byte-identical ON vs OFF (0.865) |
| Option values undifferentiated → decision margin never reaches the commitment bound → no action released | Akinetic mutism / catatonic stupor; decisional-initiation failure with preserved cognition | BG action-release / commitment gate (STN–GPi–thalamus), pre-SMA/SMA initiation, dopaminergic readiness; decision-bound ramp (LIP/PFC) | 629: mean decision margin `0.00074` (~70× below admission floor), `n_commit_entries = 0`, beta latch never elevated |
| Critical-period crystallization step is a behavioural no-op (policy never trained) → no consolidated strategy to protect | Failure to consolidate a stable behavioural repertoire (developmental, not degenerative) | Critical-period plasticity closure (PNN/Lynx1; EWC analogue) acting on a policy that never underwent winner-take-all learning | 610c: crystallization frozen onto an untrained near-uniform policy; both arms ~0.7 of max entropy |

Every row is governance-classified as a *non-falsification*: the claim was never placed
under conditions where it could express itself. The clinical analogue is the failure's
*control-architecture signature*, not a diagnosis.

---

## Why this is not just metaphor

The analogy earns its keep because it **predicts where to look next**, and the prediction
is specific enough to be wrong.

- The catatonic-like reading says the deficit is at the **selection-and-commitment loop**,
  not at representation. That immediately predicts: enriching the evaluator, the world
  model, or the drives will *not* fix the behaviour, whereas giving the existing modulatory
  signals competitive authority at the selection arbitrator *will*. Clusters (1)–(3) were
  independently designed to test different mechanisms (goal, curiosity, vigor,
  commitment-release) and all failed at the *same* downstream stage — exactly the
  convergence the loop-localisation hypothesis predicts and a representation-deficit
  hypothesis does not.
- It predicts the *form* of the fix: a competitive arbitration layer at or after the
  evaluator (normalisation, relative scaling against the dominant score term, or a
  dedicated gating channel) rather than per-mechanism tuning. This is the same conclusion
  the architecture's own calibration work reached from a different direction ("diversity
  must act at or after the scoring stage").
- It distinguishes two failures that look identical from outside — *absence of a
  representation* vs *failure to release a present representation into action* — and
  assigns them to different loops with different repairs. Cluster (1) is the former (goal
  not yet formed); clusters (2)–(3) are the latter (formed/active but not authoritative). A
  pure "it's broken" account cannot make that cut.

The analogy is doing explanatory work: it compresses several independent autopsies into one
loop-level hypothesis and tells you which experiment discriminates it next. This is the
generative direction the taxonomy claims (see [`framework_overview.md`](framework_overview.md)),
exercised on live evidence.

---

## Cautions

- **This is not a model of human catatonia.** REE-v3 is a small grid-world agent. The
  clinical terms are used as *control-architecture signatures*, not nosological claims about
  people. No claim is made about the neurobiology, treatment, or experience of any human
  syndrome. (See [`psychopathology_usage.md`](psychopathology_usage.md) and
  [`limitations.md`](limitations.md) for the standing constraints on structural
  correspondence.)
- **This is not proof REE will scale.** That the failures are legible says nothing about
  whether fixing them yields a capable agent. Legible failure and eventual capability are
  independent.
- **Clinical resonance must not substitute for experiment.** The fit between a failure and a
  syndrome is a hypothesis-generator, not evidence. Within REE this is enforced
  procedurally: a clinically-suggestive autopsy produces a *recommended* disposition and a
  next experiment; it never auto-applies, and the analogy never weights claim confidence. A
  satisfying metaphor that survives no falsifier is worth nothing.
- **Convergence can be an artifact.** Several mechanisms failing at the same stage could
  reflect one shared harness defect rather than one shared architectural truth. Each cluster
  must be checked for a common-cause confound before the loop-level reading is trusted (630
  is a worked example: it looked like the others but was caused by an environment confound
  and was routed out of the cluster).

---

## Next research questions

1. **How do psychiatric syndromes become computationally generative?** Can a syndrome be
   restated as a constraint on an architecture — "for *this* pattern to be a possible
   failure mode, the system must have property X" — strongly enough to generate predictions
   and candidate fixes?
2. **What distinguishes absence of representation from failure of action-release
   authority?** These present identically (no behaviour) but require opposite repairs. What
   observable signatures separate "the goal never formed" from "the goal formed but could
   not command action"?
3. **How can modulatory drives be given selection authority without producing monostrategy
   or noise?** The fix for clusters (2)–(3) is to let curiosity/vigor/goal signals move
   selection — but too much authority collapses behaviour to a single strategy or to
   randomness. What arbitration discipline gives authority *and* preserves diversity?
4. **Can artificial cognitive failure modes be classified using psychiatric phenomenology
   plus neurofunctional-loop hypotheses?** Is there a usable taxonomy of the form *(observed
   failure pattern) × (hypothesised loop)* that generalises across mind-like control
   architectures — i.e. the project this repository already is, extended with an explicit
   loop-hypothesis column?
5. **Could REE become a computational-psychopathology workbench before it becomes a full
   ethical AI?** The near-term scientific value may be as a system in which psychiatric
   failure modes can be instantiated and dissected — independent of whether it ever reaches
   its original goal.

---

## Working hypothesis

REE-v3's current dominant failure mode is not representational absence but **failure of the
basal-ganglia-like selection and commitment loop to give goal, salience, curiosity, and
vigor signals enough authority to become action.** The evaluative and motivational
subsystems are present and active; what is underpowered is the conversion of salience into
committed behaviour. This makes the project a useful test case for computational psychiatry:
psychiatric categories may describe not only human syndromes but **recurring failure modes
in mind-like control architectures** — patterns that any system bridging representation and
action can fall into, and which an executable model lets us name, localise, and perturb.

---

## Source autopsies (REE_assembly, `evidence/planning/`)

- `failure_autopsy_V3-EXQ-603e-626a-622_2026-06-03.{md,json}` — goal-stream / goal-latent-zero
  cluster; goal formation requires reward-contact history (foraging-competence prerequisite).
- `failure_autopsy_604a-624a-630_2026-06-03.{md,json}` — modulatory score-bias
  selection-authority cluster (curiosity 604a + vigor 624a); 630 is the env-confound member
  routed out.
- `failure_autopsy_V3-EXQ-629_2026-06-03.{md,json}` — MECH-342 `NO_NATURAL_COMMITMENT`; flat
  decision margin, commitment gate never admits.
- `failure_autopsy_V3-EXQ-610c_2026-06-03.{md,json}` — crystallization a behavioural no-op
  (related "wired but inert" instance).
- Governance disposition: REE_assembly `master` commit `0de956c449` (2026-06-03) — all of the
  above classified `non_contributory` / `substrate_ceiling` / `measurement_test_design_defect`,
  **not** falsifications.

See also [`ree_mapping.md`](ree_mapping.md) (failure mode → REE component) and
[`psychiatric_predictions.md`](psychiatric_predictions.md) (the falsifiable-prediction register
this note's clusters can feed into).
