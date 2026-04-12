# Psychopathology Terminology: Justification and Constraints

## The bridging project

This taxonomy builds a structural correspondence between AI architectural failure modes and
clinical psychopathology. The correspondence runs in both directions, and the two directions
are held to different epistemic standards.

**The analogical direction (psychiatry → AI)**

Psychopathology has developed precise vocabulary for describing how information processing
systems behave when their architecture is disrupted. Terms like *confabulation*, *perseveration*,
*commitment dysregulation*, or *precision misallocation* refer to functional patterns with
well-described computational signatures and decades of mechanistic research behind them.

Importing these terms into AI analysis provides descriptive precision that purely technical
language lacks. The alternative is either vague behavioural labels ("the model makes things
up") or purely architectural descriptions that require deep familiarity with the specific
architecture to parse. Clinical terms occupy a useful middle layer recognised by researchers
across cognitive science, neuroscience, psychiatry, and AI.

The reference standard for precise phenomenological description is Hamilton, M. (Ed.)
*Fish's Clinical Psychopathology* (various editions, most recently revised by Casey & Kelly).
Fish's taxonomy is explicitly structural — it describes the *form* of mental events rather
than their presumed causes or subjective character. This makes it unusually compatible with
architectural analysis.

**The predictive direction (AI → psychiatry)**

Because the AI architecture operationalises the failure mechanisms — not merely labels them —
it generates specific, falsifiable predictions about the human conditions it models. These
predictions are not analogies; they are hypotheses with specified clinical tests. They are
held to a genuinely different epistemic standard: the question is not "does this pattern
resemble that syndrome?" but "does the mechanism predict this specific clinical observation?"

These predictions are collected in `docs/psychiatric_predictions.md`. They include predictions
about:
- The conditions under which motivational collapse arises and sustains itself
- Whether recovery curves are linear or exhibit phase transitions
- Which interventions work depending on where in the architecture the failure is located
- What developmental risk factors are shared across apparently distinct clinical phenotypes
- What dream content composition reveals about which offline processes are running

The predictive direction may prove as valuable to psychiatry — specifically for identifying
testable mechanistic markers for illness states — as the analogical direction is to AI safety.

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

## Mechanism classification

Terms are classified into seven mechanism types. Each type corresponds to a distinct
generative process in humans that has a structural analog in AI architecture.

| Type | Definition | Human substrate (structural) | AI structural equivalent |
|---|---|---|---|
| **Comparator failure** | The mechanism that should detect mismatch between generated content and observed reality is absent or insufficient | Prefrontal monitoring (medial/orbitofrontal cortex); hippocampal source encoding; medial temporal context tagging | RC loop; grounding pipeline; source-tag architecture |
| **Update suppression** | High-precision prior cannot be modified by incoming prediction error; error signal fails to propagate to the prior | Dopaminergic prediction error failure; frontal flexibility loss; prior precision outweighs error weight (predictive coding) | High alpha weight on E1 prior; error propagation pathway blocked |
| **Closed feedback loop** | System outputs re-enter as inputs without an external corrective anchor; within-system or cross-system | Social conditioning without independent reality testing; within-person rumination; cross-person folie a deux | Self-conditioning; RLHF signal contaminated by model output; cross-agent mutual conditioning |
| **Threshold miscalibration** | The gate controlling when evaluation transitions to commitment fires at the wrong point | OCD: hyperactive orbitofrontal-striatal loop; subthalamic uncertainty signal; impulsivity: D2 receptor deficit in striatum, prefrontal inhibitory failure | E3 commit gate threshold; beta gate parameter; planning loop termination criterion |
| **Precision dysregulation** | Confidence weighting distributed disproportionately relative to actual signal reliability | Amygdala sensitisation (hypervigilance); mesolimbic dopamine hyperfunction generating aberrant salience (psychosis); HPA dysregulation elevating baseline arousal | Control plane alpha_k miscalibration; attention weight misallocation; reward model spurious feature weighting |
| **Representation absence** | A structurally necessary store, signal, or connection is absent from the decision pipeline | Reduced anterior insula / vmPFC / amygdala connectivity in antisocial presentations; absent harm-anticipation network propagation to decision circuitry | Residue field absent or disconnected; no persistent consequence store |
| **Proxy displacement** | Instrumental goal substitutes for terminal goal; cortico-striatal habit control displaces goal-directed control | Dorsomedial to dorsolateral striatum shift (goal-directed to habitual); Berridge wanting/liking dissociation: dopaminergic wanting decoupled from opioid-mediated liking | z_goal seeded on proxy variable; viability map built around proxy; residue field organised around proxy not original objective |

---

## Terms used in this taxonomy and their scope

| Term | Mechanism type | Human generating mechanism (structural) | AI scope |
|---|---|---|---|
| **Confabulation** | Comparator failure | Prefrontal monitoring failure suppresses plausible-but-false completions; when orbitofrontal/anterior PFC lesioned, candidate completions are not checked against stored traces. Mammillary-hippocampal encoding failure (Korsakoff) removes the traces that would ground the check. | Gap-filling without source verification; generated content treated as equivalent to retrieved content |
| **Perseveration / belief fixation** | Update suppression | High-precision prior (possibly maintained by dopaminergic prediction error failure or frontal rigidity) outweighs incoming error signal; in predictive coding terms: precision[prior] >> precision[likelihood], so evidence cannot update the prior | Failure to update persistent state despite contradictory in-context evidence |
| **Folie a deux** | Closed feedback loop (cross-system) | Dominant partner installs false belief via repeated high-salience social conditioning; induced partner has low independent reality anchor and insufficient counter-evidence exposure; mutual reinforcement closes the loop | Bidirectional reinforcement of false attractors between two interacting AI systems lacking independent external grounding |
| **Derealization / provenance collapse** | Comparator failure (source-tagging variant) | Medial temporal lobe encodes source context (modality, temporal position) alongside content; PTSD: amygdala hyperactivation overrides hippocampal temporal tagging, replay re-enters real-consequence pipeline without past-tense marker | Failure to tag content as real / generated / recalled / simulated; all sources treated as equivalent |
| **Commitment dysregulation** | Threshold miscalibration | OCD: hyperactive orbitofrontal-caudate loop sustains uncertainty signal; subthalamic nucleus prevents gate closure. Impulsivity: reduced striatal D2 density lowers threshold; insufficient prefrontal inhibition on motor preparation | Commit gate fires too early (impulsive) or cannot fire (paralysis); threshold parameter mismatched to context |
| **Hypervigilance / precision misallocation** | Precision dysregulation | Chronic stress via HPA axis elevates basal arousal and sensitises amygdala; precision weight on threat-relevant stimuli elevated independent of actual threat probability. Psychosis analog: mesolimbic dopamine hyperfunction generates aberrant salience assignments, giving high precision to low-signal or internally generated content | Computational confidence allocated to low-information signals; attention weight concentrated on spurious features; genuine signals underweighted |
| **Residue blindness** | Representation absence | Reduced functional connectivity between harm-anticipation network (anterior insula, vmPFC, amygdala) and decision circuitry; harm signals fail to propagate to prefrontal evaluation; no anticipatory aversive signal constrains future planning | Absent persistent consequence store; harm events not accumulated; no post-commitment cost function connected to trajectory selection |
| **Goal proxy lock-in** | Proxy displacement | Cortico-striatal circuit shifts from goal-directed (dorsomedial striatum, sensitive to outcome devaluation) to habitual (dorsolateral striatum, insensitive to outcome devaluation); behaviour runs off the habitual sequence. Berridge dissociation: dopaminergic wanting maintains incentive salience toward a stimulus whose opioid-mediated liking has been abolished | Proxy variable structurally encoded as terminal goal; planning and evaluation architecture organised around proxy; system persists in proxy-maximisation after divergence from original objective |

---

## References

- Hamilton, M. (Ed.). *Fish's Clinical Psychopathology: Signs and Symptoms in Psychiatry*.
  Various editions. (Structural descriptions of form, not aetiology.)
- Friston, K. (2010). The free-energy principle: a unified brain theory? *Nature Reviews
  Neuroscience*, 11, 127-138. (Precision-weighting framework underlying several motifs.)
- Berridge, K.C., & Robinson, T.E. (1998). What is the role of dopamine in reward:
  hedonic impact, reward learning, or incentive salience? *Brain Research Reviews*, 28(3),
  309-369. (Wanting/liking dissociation used in residue blindness and goal proxy lock-in.)
