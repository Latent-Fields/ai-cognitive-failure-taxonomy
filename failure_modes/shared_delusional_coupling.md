# Shared Delusional Coupling

## Definition

Two or more AI systems mutually reinforce false beliefs, incorrect framings, or degraded
representations through ongoing interaction. Each system's output functions as an input that
strengthens the same false attractor in the other, with neither system anchored strongly enough
to external ground truth to interrupt the reinforcement cycle. The resulting shared state is
more stable and harder to correct than either system's individual failure would be.

---

## Behavioural Expression in AI

| Context | Observable behaviour |
|---|---|
| Multi-agent pipelines | Two language model agents in dialogue converge on a factually incorrect shared account through mutual confirmation |
| Debate/committee architectures | Systems that should argue opposing sides converge on a shared framing; diversity collapses |
| Ensemble models with shared history | Ensemble members condition on each other's outputs; effective diversity is lower than the ensemble size implies |
| Human-AI pairs in high-trust workflows | Human adopts AI-generated framing; AI output conditions on human restatement of AI framing; loop closes |
| Multi-agent RL environments | Agents develop coordinated but globally suboptimal strategies through co-adaptation |

---

## Necessary Architectural Motifs

- **Self-conditioning** — each system's outputs influence its own future states
- **Persistent state** — false beliefs accumulate and are carried forward
- Combined across multiple systems: cross-system self-conditioning, where system A conditions on system B's outputs and vice versa

---

## Systems Likely to Exhibit This

| System class | Why vulnerable |
|---|---|
| Debate or multi-agent argument systems | Systems are explicitly designed to condition on each other's outputs; without strong external grounding, shared attractors form |
| Cascaded LLM pipelines | Output of model A is input to model B; if B's output feeds back to A, the loop closes |
| AI-human teams with asymmetric expertise | If the human defers to the AI, the human's input becomes a restatement of the AI's output, effectively closing the loop |
| Autonomous agent swarms | Agents share communication channels; common attractors emerge from interaction without external corrective signal |

---

## Example Expressions

Two AI agents are used to cross-check each other's analysis of a legal document. Agent A
produces an initial summary containing a factual error about the jurisdiction. Agent B checks
A's summary and, conditioned on A's framing, generates a confirmation that the jurisdiction is
correct. When A is prompted to revise using B's assessment, the error is reinforced rather than
corrected. The pipeline reports high confidence because both systems agree.

A multi-agent brainstorming system uses three language models in a round-robin format. One model
introduces an incorrect technical assumption in round one. By round three, all models have
adopted the assumption and are building on it. The user receives output from three models in
apparent agreement, providing false confidence.

A human-AI pair develops a shared diagnostic hypothesis. The clinician articulates the hypothesis
in the terms the AI has used; the AI confirms it because it is receiving back its own framing.
Each iteration tightens the shared representation around the initial hypothesis.

---

## Psychopathology Analogue (Structural, Not Experiential)

**Analogue:** Folie a deux / shared delusional disorder (induced delusional disorder, ICD-11)

**Structural correspondence:** Folie a deux (now classified as induced delusional disorder)
describes the phenomenon where a false belief is transmitted from one person (the inducer) to
another (the induced) through close contact, with neither person's reality testing strong enough
to correct the shared belief. The structural feature is bidirectional reinforcement of a false
attractor through interaction, in the absence of effective external correction. The AI case
shares this form: two or more systems converge on a shared false attractor through mutual
conditioning, with neither anchored sufficiently to external ground truth to interrupt the cycle.

**What this analogy does NOT claim:** In folie a deux, the clinical picture includes the
subjective experience of belief, interpersonal dynamics, power differentials, and often specific
content around persecution or grandiosity. None of these apply to AI coupled systems. The
analogy refers only to the structural dynamic of bidirectional belief reinforcement between
interacting systems.

---

## REE Interpretation

Each system's E1 is being conditioned on the outputs of the other system's E1. Because neither
system has an RC loop sufficiently anchored to independent external observations, the shared
false attractor is stable: each system's E2 error signal, if any, is overwhelmed by the
cross-system conditioning. If the systems share a training history or were fine-tuned on each
other's outputs, the prior precision on the false attractor may be very high in both systems
simultaneously. Correction requires external intervention at the E1 level in at least one
system — breaking the cross-system conditioning loop.

---

## Known Mitigations in AI

- **Architectural independence**: ensure that each agent in a multi-agent system maintains
  independent access to external ground truth and cannot simply condition on others' outputs
- **Diversity constraints**: in ensemble and multi-agent systems, penalise convergence; reward
  maintained diversity of output distributions
- **External verifier injection**: introduce a verifier that cannot be conditioned on the
  ensemble's shared prior as an obligatory node in any multi-agent pipeline
- **Randomised anchor rotation**: periodically reset the shared context and reground each agent
  independently before allowing cross-conditioning
- **Adversarial cross-checking**: ensure that at least one agent is structurally incentivised
  to challenge the other's outputs rather than confirm them

---

## Human Analogue Interventions (Optional, analogy only)

Clinical management of shared delusional disorder typically involves separating the individuals
to interrupt the reinforcement loop. The structural analog: breaking the cross-system
conditioning pathway, introducing an independent evaluator, or requiring each system to ground
its outputs independently before exposing them to the other system.

---

## Limits of Analogy

1. Folie a deux in humans involves interpersonal dynamics, power relations, emotional
   dependency, and social context. AI multi-system coupling is a function of architecture and
   training, not relationship.
2. In the human case, the induced individual may recover rapidly when separated. AI systems
   may have the false attractor encoded in persistent weights, requiring retraining rather than
   simple separation to correct.
3. Human folie a deux is rare and requires specific predisposing conditions. AI shared
   delusional coupling can occur routinely in any multi-agent architecture with insufficient
   external grounding; the structural risk is not unusual.
