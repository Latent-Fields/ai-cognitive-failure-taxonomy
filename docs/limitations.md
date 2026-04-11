# Limitations

## 1. AI systems are not conscious

No entry in this taxonomy implies that AI systems have conscious experience, subjective
states, or phenomenology. The psychopathology analogues are structural tools. When we say
an AI system exhibits "confabulation-like" behaviour, we mean its output has the functional
form of confabulation — gap-filling without provenance tracking — not that it experiences
anything analogous to what a confabulating patient experiences.

This distinction is not merely a disclaimer. It matters for analysis: the human experience
of confabulation includes a subjective sense of coherent memory and often preserved affect.
None of that is present in, or relevant to, the AI case. Importing those features into the
analysis would be an error.

---

## 2. The analogy is one-directional

Structural similarity does not imply mechanistic identity. That a failure mode in an AI
system resembles confabulation does not mean the system uses the same mechanism as a
confabulating patient, responds to the same interventions, or will deteriorate in the
same way. The analogy identifies a shared functional form and suggests a research direction.
It does not license inference in the other direction.

---

## 3. These are functional descriptions, not diagnoses

This taxonomy does not diagnose AI systems. It characterises failure patterns. The distinction
matters because:

- Diagnoses imply aetiology, prognosis, and treatment. These entries do not.
- Diagnoses are categorical; these failure modes exist on continua and co-occur.
- A clinical diagnosis requires assessment of a specific individual in context. These entries
  describe classes of systems under classes of conditions.

---

## 4. Psychopathology terminology carries clinical load

Terms like "delusion," "paranoia," or "psychosis" carry clinical, social, and moral weight
in their primary context. Using them in an AI context risks:

- Trivialising the conditions they describe in human patients
- Importing unfounded claims about AI experience or suffering
- Creating confusion between AI system failures and human illness

This taxonomy attempts to minimise these risks by using structural qualifiers consistently
("confabulation-like," "structural analog of"), by isolating the specific functional feature
being compared, and by including explicit `Limits of Analogy` sections. These measures do
not eliminate the risk entirely.

---

## 5. Scope boundaries

This taxonomy does not cover:

- **Hardware and infrastructure failures**: power loss, memory corruption, network partition
- **Data quality failures**: the taxonomy describes architectural failure modes, not the
  consequences of bad training data per se (though bad data can trigger some modes)
- **Adversarial attacks**: prompt injection, jailbreaking, and poisoning attacks may trigger
  failure modes described here, but the taxonomy does not cover attack methodology
- **Calibration failures in narrow systems**: a classifier that outputs wrong probabilities
  but has no persistent state or planning loop is outside scope
- **Value misalignment as a general category**: this taxonomy covers specific architectural
  mechanisms; it does not attempt to address the full scope of alignment failure

---

## 6. The taxonomy is incomplete

Nine failure modes are not all possible failure modes. The entries here were selected because
they have clear architectural explanations and useful clinical correspondences. There are
certainly failure patterns not yet characterised. The schema in `schema/failure_mode_template.md`
is designed to be extensible.

---

## 7. Mitigations are not guarantees

The `Known Mitigations` sections describe interventions that reduce susceptibility. None of
them eliminates a failure mode. Systems with all listed mitigations in place can still exhibit
the failure under sufficient distributional shift, adversarial conditions, or sufficiently
long deployment horizons.
