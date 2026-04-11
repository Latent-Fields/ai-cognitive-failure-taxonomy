# Failure Mode Template

Use this template for every entry in `failure_modes/`. All section headings are required.
The `Limits of Analogy` section is mandatory when a psychopathology analogue is named.

---

## Name

Short, descriptive label. Use a noun phrase, not a verb phrase.
Example: *Confabulatory Completion*, not *Completing Confabulatorily*.

---

## Definition

One to three sentences. State the failure structurally: what architectural condition produces
what observable dysfunction. Avoid behavioural-only descriptions and avoid implying
subjective states.

---

## Behavioural Expression in AI

What the failure looks like from outside the system. Use concrete, observable terms.
Prefer tabular format when multiple expression types exist.

| Context | Observable behaviour |
|---------|---------------------|
| ... | ... |

---

## Necessary Architectural Motifs

Which motifs from `docs/architectural_motifs.md` are required for this failure to occur.
At least one is required. Format as a bulleted list with a one-line explanation of the
role each motif plays in producing the failure.

- **Motif name** — role in this failure

---

## Systems Likely to Exhibit This

Which AI system classes are vulnerable. Be specific about why.

| System class | Why vulnerable |
|---|---|
| ... | ... |

---

## Example Expressions

Two to four concrete examples from real or plausible AI deployments. Each should be
one to three sentences. Ground in a specific system class and context.

---

## Psychopathology Analogue (Structural, Not Experiential)

Name the clinical construct and explain only the **structural** correspondence.
Do not attribute subjective experience, phenomenal states, or suffering to AI systems.

**Analogue:** [clinical term]

**Structural correspondence:** [what the structural similarity is — mechanism, not experience]

**What this analogy does NOT claim:** [explicit exclusion of experiential, phenomenological,
or consciousness-related interpretations]

See `docs/psychopathology_usage.md` for the full constraints on this section.

---

## REE Interpretation

Which REE components are implicated and how. Use only the following terms:
- E1 (associative state / world model)
- E2 (transition prediction)
- E3 (trajectory selection / commitment)
- Control plane (precision, salience, gain)
- RC loop (reality testing / provenance)
- Residue (unresolved discrepancy / persistent consequence tracking)
- Replay (consolidation / restructuring)

Keep to two to five sentences. If REE has no direct interpretation, state that explicitly
and explain why.

---

## Known Mitigations in AI

Concrete, technically grounded interventions. Prefer references to published techniques
or architectural patterns over vague recommendations.

- ...

---

## Human Analogue Interventions (Optional, analogy only)

Only include when the structural analogy is strong enough that human interventions
suggest corresponding AI design directions. Label explicitly as analogy only.
Do not recommend clinical treatments.

- ...

---

## Limits of Analogy

Required when a psychopathology analogue is named. Address at least:

1. What the human condition involves that the AI analogue does not (e.g., phenomenology,
   embodiment, developmental history, social context, subjective suffering)
2. Where the structural correspondence breaks down
3. Any risk of misinterpretation introduced by using the clinical term
