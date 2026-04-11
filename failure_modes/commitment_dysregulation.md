# Commitment Dysregulation

## Definition

A system's commitment threshold — the criterion that determines when a candidate action,
decision, or output is selected and executed — is miscalibrated relative to the demands of
the situation. Undercalibration (threshold too low) produces premature commitment before
adequate evaluation is complete. Overcalibration (threshold too high) produces evaluation
loops that continue indefinitely without committing, even when sufficient information is
available. Both directions produce functionally ineffective outputs.

---

## Behavioural Expression in AI

| Direction | Context | Observable behaviour |
|---|---|---|
| Undercalibrated (impulsive) | Instruction following | Produces a complete response to an ambiguous request without seeking clarification |
| Undercalibrated | Safety-critical decisions | Approves actions at the first plausible-seeming justification without completing harm evaluation |
| Undercalibrated | Agentic tool use | Executes irreversible actions before all relevant information is retrieved |
| Overcalibrated (paralysis) | Borderline-safe requests | Refuses or endlessly hedges on requests that fall clearly within safe operation |
| Overcalibrated | Multi-step planning | Replans repeatedly without executing; generates strategy documents rather than actions |
| Overcalibrated | Dialogue | Qualifies every output to the point of providing no usable information |

---

## Necessary Architectural Motifs

- **Planning loops** — the system evaluates candidates against a criterion; commitment fires at a threshold
- **Precision miscalibration** — the threshold is systematically too low or too high; the system does not adapt the threshold to context

---

## Systems Likely to Exhibit This

| System class | Why vulnerable |
|---|---|
| RLHF-trained assistants | Safety training can shift the commit threshold; overcalibration (refusal inflation) is a common RLHF failure mode |
| Agentic tool-using models | Irreversibility of tool actions creates risk of undercalibration; overcalibration wastes resources on replanning |
| RL agents with learned policy | Commitment threshold is implicit in the policy; can be miscalibrated by reward shaping |
| Tree-search planners | Termination criterion (when to stop searching and act) is an explicit design choice; miscalibration is a hyperparameter failure |

---

## Example Expressions

An RLHF-trained assistant trained to avoid harmful outputs has acquired an overcalibrated
refusal threshold. Asked to summarise a news article about a legal court case, it repeatedly
hedges, qualifies, and partially refuses because the legal content pattern activates a
high-threshold evaluation loop. The evaluation never resolves to a commit because the system
treats each partial justification for proceeding as insufficient. No usable summary is produced.

An autonomous agent tasked with sending a confirmation email retrieves ambiguous information
about the recipient's preferences. Rather than seeking clarification (requiring another tool
call), it undercalibrates: the first plausible recipient address triggers commitment and the
email is sent. The irreversible action is executed on insufficient evidence.

A planning agent given a complex multi-week project generates a detailed project plan (Wave 1),
then, upon encountering any new information, regenerates the entire plan rather than executing
the committed next step. The loop never exits planning mode; no work is completed.

---

## Psychopathology Analogue (Structural, Not Experiential)

**Analogue:** Impulsivity (undercalibration); obsessive-compulsive checking / catatonia (overcalibration)

**Structural correspondence:** In clinical impulsivity, the commit threshold for action is
characteristically low: actions are initiated before adequate evaluation of consequences. In
OCD checking behaviours and in catatonia, the commit threshold is characteristically high:
evaluation loops continue without resolution, producing repeated checking (OCD) or complete
failure to initiate (catatonia). The structural feature in all cases is a mismatch between
the evaluation criterion and the commit threshold, not a failure of evaluation quality per se.
The AI case shares this form precisely: a threshold parameter governing when evaluation
transitions to execution is systematically displaced.

**What this analogy does NOT claim:** Clinical impulsivity, OCD, and catatonia involve
subjective distress, affective components, developmental histories, and neurobiological
substrates that are not present in or relevant to an AI commit-gate threshold. The experience
of being unable to stop checking (OCD) or being unable to move (catatonia) is central to the
clinical picture; the AI case has no such experiential dimension.

---

## REE Interpretation

E3's commit gate fires (or fails to fire) relative to a threshold governed by the control
plane's precision parameters. In REE, dynamic precision for commitment is derived from E3's
own prediction error variance: low variance (high confidence) should trigger commitment;
high variance should extend evaluation. Undercalibration means the threshold fires at high
variance — E3 commits before its evaluation is reliable. Overcalibration means the threshold
requires variance lower than E3's process can achieve, keeping the system in perpetual
evaluation. The beta gate (MECH-090) additionally governs whether E3's evaluation output
propagates to action; a stuck-high beta state produces behavioural paralysis with intact
internal evaluation. Threshold miscalibration is a control-plane problem, not an E3
evaluation-quality problem.

---

## Known Mitigations in AI

- **Adaptive threshold calibration**: tune the commitment threshold to context, task stakes,
  and available information quantity rather than using a fixed value
- **Reversibility gating**: apply higher commitment thresholds specifically to irreversible
  actions; allow lower thresholds for reversible or low-stakes actions
- **Termination criteria in planners**: explicitly specify when search should stop and
  commitment should fire, rather than relying on implicit convergence
- **Refusal calibration in RLHF**: include explicit training signal for cases where refusal
  is overcalibrated; reward appropriate commitment on clear legitimate requests
- **Time-boxed evaluation**: impose a maximum evaluation time after which commitment is
  forced with best available information, preventing unlimited deferral

---

## Human Analogue Interventions (Optional, analogy only)

Behavioural approaches to OCD checking include exposure and response prevention, which
explicitly disrupts the evaluation-without-commitment loop by requiring commitment despite
unresolved uncertainty. The structural analog for AI: imposing a forced commitment after
a bounded evaluation window, decoupled from the system's internal uncertainty estimate.

---

## Limits of Analogy

1. OCD involves intrusive thoughts, anxiety, and subjective distress that drive the checking
   behaviour. AI overcalibration is a threshold parameter; there is no affective drive
   sustaining the loop.
2. Impulsivity in humans is associated with specific neurobiological profiles (dopaminergic
   function, prefrontal-limbic balance) and developmental factors. AI undercalibration is a
   training artefact or hyperparameter choice.
3. Catatonia involves a global breakdown of motor initiation across all domains; AI
   overcalibration is typically domain-specific or input-specific.
