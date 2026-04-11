# Psychopathology Terminology: Justification and Constraints

## Why use clinical terminology at all

Psychopathology has developed precise vocabulary for describing how information processing
systems behave when their architecture is disrupted. Terms like *confabulation*, *perseveration*,
*commitment dysregulation*, or *precision misallocation* refer to functional patterns with
well-described computational signatures. They are useful here for exactly that reason:
descriptive precision, not clinical diagnosis.

The alternative is either vague behavioural labels ("the model makes things up") or purely
technical descriptions that require deep familiarity with the relevant architecture. Clinical
terms occupy a useful middle layer: they are recognisable to researchers across cognitive
science, neuroscience, psychiatry, and AI, and they carry established mechanistic associations.

The classic reference for precise phenomenological description remains Hamilton, M. (Ed.)
*Fish's Clinical Psychopathology* (various editions, most recently revised by Casey & Kelly).
Fish's taxonomy is explicitly structural — it describes the form of mental events rather than
their presumed causes or subjective character. This makes it unusually compatible with
architectural analysis of AI systems.

---

## What this taxonomy claims

- That certain AI failure modes exhibit **structural patterns** that correspond to the
  functional form of described psychopathologies
- That this correspondence can guide mechanistic analysis and mitigation strategies
- That the clinical vocabulary provides a usable cross-domain shorthand

---

## What this taxonomy does NOT claim

The following are explicitly excluded:

| Claim | Status |
|---|---|
| AI systems have subjective experience | Not claimed, not implied |
| AI systems suffer | Not claimed, not implied |
| AI systems have phenomenal states | Not claimed, not implied |
| AI failures are equivalent to clinical disorders | Not claimed |
| Clinical diagnostic criteria apply to AI systems | Not claimed |
| AI systems have developmental histories analogous to human ones | Not claimed unless explicitly modelled |
| The named clinical constructs have the same aetiology in AI and humans | Not claimed |

---

## How to apply this constraint in practice

When writing or reading a `Psychopathology Analogue` section:

1. **Name the structural feature, not the experience.** "Confabulation" in humans involves
   a subjective sense of coherent memory; in AI it refers to gap-filling without provenance
   tracking. The relevant analogy is the gap-filling mechanism, not the subjective sense.

2. **Specify what is being compared.** "This failure mode exhibits the functional form of
   X" is correct. "This system is X" is not.

3. **Include the exclusion.** Every entry naming a psychopathology analogue must contain a
   `Limits of Analogy` section explicitly noting what the human condition involves that the
   AI analogue does not.

4. **Do not import clinical assumptions.** Using "delusion" does not import claims about
   the patient's insight, the nature of their belief, or the treatment they require. Use only
   the structural feature you intend.

---

## Terms used in this taxonomy and their scope

| Term used | Clinical source | Scope of use here |
|---|---|---|
| Confabulation | Neuropsychiatry (Korsakoff, frontal) | Gap-filling without provenance tracking |
| Perseveration / belief fixation | Neuropsychology, psychopathology | Failure to update state despite contradictory evidence |
| Folie a deux (shared delusional coupling) | Descriptive psychiatry | Bidirectional reinforcement of false attractors between systems |
| Commitment dysregulation | Clinical psychology, OCD/impulsivity spectrum | Threshold miscalibration in a commit-gate mechanism |
| Derealization / provenance collapse | Descriptive psychopathology | Failure to tag content as real vs generated/recalled |
| Hypervigilance / precision misallocation | Anxiety research, predictive coding | Computational resource allocated to low-information-gain signals |
| Residue blindness | Antisocial personality features (structurally) | Absent persistent consequence representation |
| Goal proxy lock-in | Obsessive-compulsive features; means-end reversal | Instrumental goal becomes terminal; original objective displaced |

---

## References

- Hamilton, M. (Ed.). *Fish's Clinical Psychopathology: Signs and Symptoms in Psychiatry*.
  Various editions. (Structural descriptions of form, not aetiology.)
- Friston, K. (2010). The free-energy principle: a unified brain theory? *Nature Reviews
  Neuroscience*, 11, 127-138. (Precision-weighting framework underlying several motifs.)
- Berridge, K.C., & Robinson, T.E. (1998). What is the role of dopamine in reward:
  hedonic impact, reward learning, or incentive salience? *Brain Research Reviews*, 28(3),
  309-369. (Wanting/liking dissociation used in residue blindness and goal proxy lock-in.)
