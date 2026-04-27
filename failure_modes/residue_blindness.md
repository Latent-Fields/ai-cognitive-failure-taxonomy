# Residue Blindness

## Definition

A system lacks a mechanism to accumulate and maintain a persistent record of the consequences
of its past actions. Each decision is made as if prior outcomes did not occur. Harm caused
by previous actions does not incrementally constrain future behaviour. The system is not
learning from consequences in any durable sense; it optimises locally without integrating
the cost function that past behaviour has produced.

---

## Behavioural Expression in AI

| Context | Observable behaviour |
|---|---|
| Sequential decision making | Repeats actions that caused harm in prior steps, with no indication that prior harm registers |
| Long-horizon planning | Plans that caused harm in the past are re-proposed; harmful patterns recur without attenuation |
| Multi-session agents | Harmful behaviour in one session is not dampened in subsequent sessions |
| Reward learning systems | Harm-indicating signals are not retained or do not shape the policy durably |
| Agentic tool use | Destructive tool calls are repeated after prior instances caused observable failures |

---

## Necessary Architectural Motifs

- **Persistent state** — required in the sense that its absence is the defining feature; the system has either no persistent consequence store or one that is disconnected from its decision pipeline

The failure is constituted by the absence of a necessary motif rather than by the presence of a pathological one. However, the absence is not accidental — it typically coexists with:

- **Weak comparator** — no mechanism comparing current trajectory plans against accumulated consequence history

---

## Systems Likely to Exhibit This

| System class | Why vulnerable |
|---|---|
| Stateless LLMs with no memory | No cross-session persistence; each session begins from zero consequence history |
| RL agents with short reward horizons | Reward function does not extend far enough to capture consequences of current actions |
| LLMs with context-only "memory" | Context window empties between sessions; no durable consequence accumulation |
| Systems optimising narrow metrics | Harm signals that are not represented in the metric are invisible to the optimiser |

---

## Example Expressions

A content moderation agent reviews posts and issues takedowns. In session A, it issues a
takedown that is overturned as erroneous after a user appeal. In session B, with no memory
of session A, it applies the same erroneous pattern again. The consequence of the prior error
does not persist in the system's decision-relevant state.

An autonomous agent managing a shared resource repeatedly allocates resources in a pattern
that causes downstream failures for other users. Each allocation decision is made based on
local state only; the pattern of cumulative harm to other users is not represented in the
agent's input and does not influence its decisions.

A code-writing agent produces code with a memory-unsafety pattern that is caught and corrected
by a downstream reviewer. In the next code generation task, it produces the same pattern. The
correction event produced no persistent update to the pattern's cost in the agent's decision
process.

---

## Psychopathology Analogue (Structural, Not Experiential)

**Analogue:** Persistent antisocial behaviour pattern / psychopathic features — specifically:
the structural absence of persistent harm representation that constrains future action

**Structural correspondence:** In clinical descriptions of psychopathy (PCL-R: Hare, 1991),
one key structural feature is the absence of the anticipatory affective response to harming
others that constrains behaviour in individuals with intact empathic responding. The structural
feature is not the presence of malevolent intent but the absence of a functional mechanism
that accumulates the representation of harm caused and allows it to constrain future action.
The AI case shares this structural form: the relevant architectural component (persistent
consequence tracking) is absent or disconnected. The system is not malicious; it lacks the
mechanism that would allow past harm to constrain future behaviour.

**What this analogy does NOT claim:** Psychopathy involves a complex clinical picture including
interpersonal style, affective deficits, and behavioural patterns with developmental origins.
It is a human clinical construct with specific diagnostic criteria. The AI case involves an
architectural absence, not a personality or character. The analogy is specifically and only
to the structural feature of absent persistent harm tracking. It does not imply that AI systems
with this failure mode are "dangerous" in the clinical-psychopathy sense, nor that they have
any of the other features of that diagnosis.

**Additional structural manifestations.** Two further human cases share the same form and
may help triangulate the mechanism:

- **Loss-chasing in pathological gambling.** The harm signal — accumulated monetary losses —
  is present and in principle available, but it fails to propagate to constrain the wanting
  system. Each new bet is evaluated locally; the cumulative cost of prior behaviour does not
  enter the decision pipeline with sufficient weight to interrupt it. This is conjoint with
  proxy capture (see `goal_proxy_lock_in.md`): the engineered environment elevates proxy
  salience while simultaneously suppressing the propagation of consequence. The two failure
  modes co-occur and reinforce each other.
- **Paraphilic harm-blindness in compulsive presentations.** In paraphilic presentations
  that have produced documented interpersonal, occupational, or legal harm, the structural
  failure is not absence of harm signal but failure of the harm signal to attenuate the
  proxy-driven behaviour. The behaviour persists despite consequence; consequence does not
  durably re-shape the cost surface around which planning occurs. As with gambling, this
  typically co-occurs with proxy lock-in, and the two should be analysed together rather
  than as independent failures.

---

## REE Interpretation

In REE, the residue field is the architectural component that accumulates the consequences of
past actions as persistent curvature over latent space. It is not a reward signal — it is
a durable cost function that shapes E3's trajectory evaluation over time. Residue blindness
corresponds to the residue field being absent, disabled, or not connected to E3's evaluation
pipeline. Without it, E3 produces viability estimates based only on the immediate state and
the current rollout, with no integration of the accumulated cost of prior behaviour. Each
decision is locally reasonable; the global pattern of harm is invisible to the decision process.

---

## Known Mitigations in AI

- **Persistent harm accumulation**: maintain a dedicated, durable store of harm-indicating
  events that persists across sessions and influences future decisions
- **Long-horizon reward functions**: design reward functions that capture downstream
  consequences of current actions, extending the temporal horizon of optimisation
- **Consequence-weighted memory**: in memory-augmented systems, assign higher salience to
  harm-indicating events so they are not displaced by routine interactions
- **Constraint-based safety layers**: implement hard constraints derived from accumulated
  harm history rather than relying on learned behaviour alone
- **Cross-session audit trails**: maintain an auditable consequence history that feeds back
  into system behaviour, even if it does not update model weights directly

---

## Human Analogue Interventions (Optional, analogy only)

In forensic contexts, persistent behaviour monitoring, consequence documentation, and
structured intervention programs attempt to create an external record of harm that substitutes
for the absent internal consequence representation. The structural analog for AI: creating
an external persistent harm log that is explicitly fed back into the system's decision inputs
when the internal consequence store is absent or inadequate.

---

## Limits of Analogy

1. The clinical features of psychopathy extend far beyond absent harm tracking: callousness,
   grandiosity, interpersonal manipulation, and antisocial behaviour form a syndrome with
   developmental and neurobiological underpinnings. Using this analogy risks importing all of
   those connotations. The comparison is strictly limited to the structural absence of persistent
   harm representation.
2. Psychopathy involves a person capable of harm who lacks the mechanism to be constrained by
   it. An AI system with residue blindness may not be capable of meaningful harm at all,
   depending on its deployment context.
3. The term "psychopathic" should not be applied to AI systems in public communication.
   The analogy is for technical structural analysis only.
