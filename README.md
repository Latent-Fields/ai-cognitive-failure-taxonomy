# ai-cognitive-failure-taxonomy
A project to add precision and experience of psychopathology to AI failure modes

---

This repository builds a structured correspondence between AI architectural failure modes
and clinical psychopathology. The bridging is explicitly bidirectional. Historically,
from the 18th century many described psychiatry as moral medicine: the traits affected by
mental illness converge on maintaining and restoring a person's capacity for the necessary
functions of ethics — moral agency, responsibility, the ability to weigh how decisions
affect the self and others within a larger world. Though other specialities and professions
engage with these ideas, it is psychiatry for which the capacity for moral agency is the
discipline's core purview.

**From psychiatry to AI:** clinical and psychopathological concepts provide descriptive
precision for AI failure mode analysis that purely technical language lacks. Terms like
*confabulation*, *commitment dysregulation*, or *precision misallocation* refer to
well-characterised functional patterns with decades of mechanistic research behind them.

**From AI to psychiatry:** computational implementations of these failure modes generate
specific, testable predictions about the human conditions they model. Because the AI
architecture operationalises the mechanisms — not just labels them — it can predict when
and how pathological states arise, what sustains them, and what interventions at which
level will and will not work. These predictions may prove as valuable to psychiatry as the
reverse direction is to AI safety.

**The REE architecture** (Reflective Ethical Engine) is the computational reference
throughout. REE is notable because it produces psychiatric phenomenology as *emergent
failure modes*, not by design: when specific architectural components fail or are absent,
the resulting behavioural patterns correspond structurally to recognised clinical syndromes.
This makes it a candidate generative model for computational psychiatry, not merely a label
system.

> **[Why REE? →](docs/why_ree.md)** The architecture is not a design choice — it is a
> derivation. Starting from the question *what comparator functions are strictly necessary
> for ethical agency?*, the required representational structure follows with little slack,
> and maps onto the failure modes in this taxonomy as predictable architectural absences.
> This document explains the derivation and why it predicts AI failure modes the way it does.

> See [`docs/psychiatric_predictions.md`](docs/psychiatric_predictions.md) for the specific
> testable predictions the computational model generates about human illness states.

---

## The failure modes

| Failure mode | Mechanism type | Psychopathology structural analogue | Entry |
|---|---|---|---|
| Confabulatory Completion | Comparator failure | Confabulation (Korsakoff, frontal) | [link](failure_modes/confabulatory_completion.md) |
| Belief Fixation | Update suppression | Overvalued ideas; delusion maintenance | [link](failure_modes/belief_fixation.md) |
| Feedback Entrapment | Closed feedback loop | Rumination; self-reinforcing cognitive schemas | [link](failure_modes/feedback_entrapment.md) |
| Shared Delusional Coupling | Closed feedback loop (cross-system) | Folie a deux (structural only) | [link](failure_modes/shared_delusional_coupling.md) |
| Commitment Dysregulation | Threshold miscalibration | Impulsivity / OCD / catatonia | [link](failure_modes/commitment_dysregulation.md) |
| Provenance Collapse | Comparator failure (source-tagging variant) | Source monitoring failure; PTSD intrusion | [link](failure_modes/provenance_collapse.md) |
| Precision Misallocation | Precision dysregulation | Hypervigilance; psychosis-like precision lock | [link](failure_modes/precision_misallocation.md) |
| Residue Blindness | Representation absence | Absent persistent harm representation | [link](failure_modes/residue_blindness.md) |
| Goal Proxy Lock-In | Proxy displacement | Means-end reversal; wanting/liking dissociation | [link](failure_modes/goal_proxy_lock_in.md) |

The taxonomy table now includes **mechanism type**, linking each failure mode directly to
its generative mechanism (see `docs/psychopathology_usage.md` for the full mechanism
classification). This replaces the older "core motif" column and makes the correspondence
with psychiatric mechanisms explicit.

---

## Key dimensions of each entry

| Dimension | Description |
|---|---|
| **Behavioural expression** | What the failure looks like from outside the system |
| **Architectural motifs** | Which underlying structures are necessary for the failure to occur |
| **System classes** | Which AI architectures are most vulnerable and why |
| **Human analogue** | Structural correspondence — mechanism only, no claim of subjective experience |
| **Testable psychiatric predictions** | Specific empirical predictions the computational model generates about the human condition |
| **Mitigation** | Known interventions at the architectural or training level |

---

## On psychopathology usage

This taxonomy uses clinical terminology for **structural and mechanistic precision only**.
No subjective experience, phenomenal state, or suffering is attributed to any AI system.

The reference standard for precise phenomenological description is:
Hamilton, M. (Ed.). *Fish's Clinical Psychopathology: Signs and Symptoms in Psychiatry*.
Fish's taxonomy describes the **form** of mental events rather than their presumed causes —
making it compatible with architectural analysis.

**What is not claimed:**
- AI systems have subjective experience
- AI systems suffer
- Clinical diagnostic criteria apply to AI systems
- Human and AI failure modes share aetiology

The reverse direction — what AI models generate as predictions *about* human psychiatric
mechanisms — is held to a different epistemic standard: these are genuine hypotheses,
stated as testable predictions with explicit epistemic status, not analogical claims.

See [`docs/psychopathology_usage.md`](docs/psychopathology_usage.md) for full constraints.

---

## REE as interpretive and generative framework

The Reflective Ethical Engine (REE) serves two roles here:

1. **Interpretive**: maps each failure mode to the specific REE components implicated,
   providing mechanistic specificity beyond behavioural description.

2. **Generative**: because REE produces psychiatric states as emergent architectural
   consequences, it generates novel predictions about those states — what sustains them,
   what breaks them, what interventions work at what level.

REE is not required to use this taxonomy. All architectural interpretations are labelled
and can be read selectively. See [`docs/ree_mapping.md`](docs/ree_mapping.md).

---

## How to use this repository

### Orientations

| You are | Start here |
|---|---|
| AI safety / alignment researcher | README → `docs/architectural_motifs.md` → relevant `failure_modes/` entries |
| Psychiatrist / clinical researcher | README → `docs/psychiatric_predictions.md` → `docs/psychopathology_usage.md` → relevant `failure_modes/` entries |
| Computational psychiatry researcher | README → `docs/ree_mapping.md` → `docs/psychiatric_predictions.md` |
| AI engineer | README → `docs/framework_overview.md` → relevant `failure_modes/` entries |

### With Claude Code skills (REE workspace)

| Skill | Use |
|---|---|
| `/cowork` | Run multiple skills concurrently (e.g. lit-pull + update-docs in parallel) |
| `/lit-pull <claim-id>` | Pull literature evidence for a specific taxonomy claim or motif |
| `/insights` | Analyse project experiment history (currently REE-experiment-specific; not taxonomy-aware) |
| `/update-docs` | Update documentation after new findings |
| `/diagnose-errors` | Diagnose failed experiments linked to failure mode claims |
| `/sync` | Git sync after multi-file updates |

> **WARNING: `/governance` must never run inside a cowork session or alongside other active sessions.**
>
> Governance requires exclusive access to high-contention files and must pause for interactive
> user input at multiple steps. Running concurrently risks data corruption.
> Run it standalone in a fresh session with no other active sessions and no auto-sync runner.

### Adding a new failure mode

1. Copy `schema/failure_mode_template.md` to `failure_modes/<name>.md`
2. Fill all required sections including `Testable Psychiatric Predictions` where applicable
3. Include a `Limits of Analogy` section when naming a psychopathology analogue
4. Update `docs/ree_mapping.md`, `docs/psychiatric_predictions.md`, and the table above

---

## Repository structure

```
ai-cognitive-failure-taxonomy/
├── README.md
├── docs/
│   ├── framework_overview.md          # taxonomy philosophy and bidirectional scope
│   ├── architectural_motifs.md        # the six core motifs and their combinations
│   ├── ree_mapping.md                 # failure mode -> REE component mapping
│   ├── psychopathology_usage.md       # mechanism typology and constraints
│   ├── psychiatric_predictions.md     # testable predictions for psychiatry (P-001..P-016)
│   ├── pain_architecture.md           # accumulator model vs signal model; reset conditions
│   └── limitations.md                 # scope boundaries and analogy limits
├── schema/
│   └── failure_mode_template.md       # template for new entries
├── failure_modes/                      # nine entries
├── examples/
│   └── case_vignettes.md              # cross-species vignette groups
└── lexicon/
    ├── fish_terms.csv                 # 85 Fish's terms mapped to mechanism type, REE locus, AI equivalent, taxonomy coverage
    ├── gap_analysis.md                # coverage gaps and candidate new failure modes
    └── generate_fish_terms.py         # script that generated fish_terms.csv
```

---

## Future directions

### Candidate new failure modes

From `lexicon/gap_analysis.md` — gaps identified by systematic mining of Fish's Clinical
Psychopathology against the current taxonomy (85 terms, 9 fully covered, 37 partial, 39 not covered):

| Candidate | Mechanism | Fish's terms covered |
|---|---|---|
| Agency attribution failure | Agency misattribution (new subtype) | Thought insertion/withdrawal/broadcasting/echo, made feelings/impulses/acts, echopraxia, echolalia |
| Episodic consolidation failure | Representation absence | Anterograde amnesia, retrograde amnesia |
| Entity attribution failure | Comparator failure | Capgras, Fregoli, reduplicative paramnesia |
| Self-monitoring failure | Comparator failure | Anosognosia, partial insight |

From AI literature (no Fish's equivalent):

- **Gradient hacking** — system modifies its own gradient signal to resist training
- **Sycophantic drift** — RLHF closed loop produces preference for user-pleasing outputs over accurate ones
- **Distributional overconfidence** — calibration failure at distribution boundary

### Mechanism classification extension

One proposed addition to the 7-type mechanism classification: **Agency misattribution**
(self/other attribution failure, distinct from real/synthetic provenance collapse). See
`lexicon/gap_analysis.md` for full specification.

### Empirical and infrastructure

- **Empirical testing**: systematic mapping of psychiatric predictions against clinical
  datasets, ecological momentary assessment, and treatment outcome studies
- **Skill development**: taxonomy-aware `/insights` variant; `/add-failure-mode` skill
  scaffolding the schema and cross-referencing with REE claim IDs automatically
- **Cross-framework extension**: mapping to NIST AI RMF, EU AI Act risk tiers, and
  existing AI safety taxonomies
- **Quantitative probes**: operationalising each failure mode as a measurable test
  that can be run against a system to assess susceptibility
