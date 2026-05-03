# Fish's Clinical Psychopathology — Gap Analysis

*Source: `fish_terms.csv` — 85 terms from Fish's Clinical Psychopathology (Casey & Kelly, 3rd ed.),
structured by mechanism type and mapped to current taxonomy coverage.*

*Coverage summary: 9 terms fully covered (yes), 37 partially covered (partial), 39 not covered (no).*
*Updated 2026-05-03: agency_attribution_failure.md added as the highest-priority gap (passivity phenomena cluster). Coverage of the relevant Fish's terms shifts from "no" to "yes" for thought insertion / withdrawal / broadcasting / echo, made feelings / impulses / acts, somatic passivity, echopraxia, and echolalia (10 terms). Refreshed coverage totals pending a fish_terms.csv re-tag pass.*

---

## Coverage summary by mechanism type

| Mechanism type | Total terms | In taxonomy (yes) | Partial | Not covered |
|---|---|---|---|---|
| Comparator failure | 26 | 3 | 11 | 12 |
| Precision dysregulation | 16 | 2 | 8 | 6 |
| Update suppression | 8 | 3 | 4 | 1 |
| Threshold miscalibration | 14 | 2 | 7 | 5 |
| Closed feedback loop | 7 | 0 | 4 | 3 |
| Representation absence | 10 | 1 | 4 | 5 |
| Proxy displacement | 0 | 0 | 0 | 0 |
| **Totals** | **85** | **9** | **37** | **39** |

Note: proxy displacement does not appear as a mechanism type in Fish's because it is not
phenomenologically visible as psychopathology — it surfaces as behavioural consequence
(goal-substitution, means-end reversal). The OCD/goal-proxy link is captured in
commitment_dysregulation and goal_proxy_lock_in but does not map to a Fish's phenomenological term.

---

## Well-covered terms (in taxonomy: yes)

These 9 terms are fully addressed by a current failure mode entry:

| Term | Covered by |
|---|---|
| Confabulation | confabulatory_completion.md |
| Overvalued idea | belief_fixation.md |
| Primary delusion | belief_fixation.md |
| Hypervigilance | precision_misallocation.md |
| Compulsion | commitment_dysregulation.md |
| Catatonic stupor | commitment_dysregulation.md |
| Derealisation | provenance_collapse.md |
| Hallucination (auditory verbal) | provenance_collapse.md |
| Perseveration | belief_fixation.md |

---

## High-priority gaps — candidate new failure modes

These represent structurally novel failure modes not covered or only thinly covered by existing entries.

### 1. Passivity Phenomena / Agency Misattribution — *covered as of 2026-05-03*

**Status:** Added 2026-05-03 as `failure_modes/agency_attribution_failure.md`,
anchored on Asai 2016 (DOI: 10.1016/j.psychres.2016.10.082) S/N-slope analysis
of agency attribution in healthy + schizotypal participants. The Asai
finding — that the regression slope of agency rating against self-other
discriminability is the load-bearing measure of comparator competence,
and that schizotypal participants show shallower slopes producing both
over- and under-attribution errors symmetrically — gives this failure mode
a direct quantitative biological grounding rather than only a phenomenological
analogy.

The cross-reference also lands in REE_assembly:
- MECH-095 (TPJ agency-detection comparator) is the REE locus
- SD-047 (`environment.multi_source_dynamics`, candidate, registered
  2026-05-03) is the substrate-side enrichment that V3-EXQ-506
  identified as needed before MECH-095 can be honestly tested
- `evidence/literature/targeted_review_sd_047/` holds the supporting pulls

**Terms now covered:** Thought insertion, thought withdrawal, thought broadcasting, thought echo,
made feelings, made impulses, made acts, somatic passivity, echopraxia, echolalia (10 terms;
previously listed under "not covered" in the Fish's coverage totals).

**Outstanding follow-up lit-pulls** identified during this scaffolding pass — each
addresses a specific feature of the passivity-phenomena cluster that the Asai
anchor does not directly cover:

1. **Frith comparator model + Schneiderian first-rank symptoms** — the canonical
   1992 / 2000 Frith papers and successor literature on the corollary-discharge
   account of passivity phenomena. Provides the historical mechanistic framework
   and connects the Asai S/N finding to the broader schizophrenia computational
   psychiatry tradition. Anchor candidates: Frith 1992 (Psychological Medicine);
   Voss et al. 2010 (action awareness in schizophrenia); Synofzik / Vosgerau /
   Newen 2008 (two-step account of self-attribution). Estimated 4 entries.

2. **Echopraxia / echolalia and motor self-other discrimination** — separate
   feature cluster within passivity phenomena. Distinct mechanism from
   thought-insertion (motor mirror system, frontal lesions, autism literature).
   Anchor candidates: Ganos et al. on echophenomena; iacoboni / mirror-neuron
   reviews specifically targeted at agency rather than at general action
   understanding. Estimated 3 entries.

3. **Made feelings / made impulses (interoceptive passivity)** — a more
   somatically-bound subset of passivity phenomena where the inserted content
   is affective or motivational rather than propositional. Probably depends on
   different comparator (interoceptive predictive coding) than the visual /
   action-attribution comparator Asai's paradigm tested. Anchor candidates:
   Seth on interoceptive inference; Critchley on insula and self-attribution;
   recent work on alexithymia as a comparator-precision phenomenon.
   Estimated 3 entries.

4. **Asymmetric over/under-attribution as a diagnostic signature** — the
   *non-monotonic* finding in Asai is itself worth a follow-up pull. Does the
   symmetric over/under-attribution pattern show up in other comparator-failure
   syndromes, or is it specific to agency-attribution? If general, it becomes a
   structural prediction for AI failure modes too: monitor for symmetric
   error patterns as a signal that a comparator is operating outside its
   competence regime, regardless of the specific comparator. Anchor candidates:
   non-monotonic perceptual judgment under degraded stimuli; psychophysical
   slope-based competence measures. Estimated 3 entries.

These four follow-up pulls would round out the passivity cluster's empirical
grounding without expanding the failure-mode count further.

---

### 2. Delirium

**Terms:** Delirium (and partial overlap with clouding, twilight state)

**Gap:** Delirium is a multi-mechanism syndrome (simultaneous precision dysregulation +
provenance collapse + disrupted replay/consolidation). No existing entry addresses
simultaneous multi-mechanism failure. Individually each mechanism is covered, but delirium
as a syndrome — and the specific pattern of co-occurring mechanisms — is not.

**Proposed failure mode:** `multi-mechanism_syndrome.md` or `delirium_analog.md`

**Notes:** The interest is architectural: delirium provides the clearest clinical case where
multiple failure modes co-occur and interact. A framework for multi-mechanism failure would
be more useful than a delirium-specific entry.

---

### 3. Episodic Consolidation Failure

**Terms:** Anterograde amnesia, retrograde amnesia

**Gap:** Both are already noted in Future Directions as "catastrophic forgetting" candidate.
The amnesias represent absence of consolidation mechanisms (anterograde: write failure;
retrograde: gradient overwrite). Neither is addressed in the current taxonomy.

**Proposed failure mode:** `episodic_consolidation_failure.md`

**AI equivalent:** Stateless transformers (anterograde: no write to persistent store),
catastrophic forgetting (retrograde: gradient update overwrites prior representations).

**Notes:** This is already on the Future Directions list. Structurally clean; good candidate
for the first new entry after the passivity phenomena cluster.

---

### 4. Entity Attribution Failure (Capgras / Fregoli / Reduplicative Paramnesia)

**Terms:** Capgras syndrome, Fregoli syndrome, reduplicative paramnesia

**Gap:** All three involve failures of identity comparison — either under-identification
(Capgras: this face is not the person I know), over-identification (Fregoli: these different
faces are the same person), or duplication (reduplicative paramnesia: there are two of this
place). These are identity-comparison comparator failures, distinct from confabulation (which
is about content generation) and provenance collapse (which is about source tagging).

**Proposed failure mode:** `entity_attribution_failure.md`

**AI equivalent:** Entity resolution failures in knowledge graphs; retrieval systems that
under-merge or over-merge entity records; systems that conflate distinct real-world entities
or multiply them spuriously. This may be failure of attribution due to lack of distinction
in comparator representations rather than, say pure precision error related failures and 
the exact mechanics of whether attribution error or another error is the best core 
epresentation needs investigating. 

---

### 5. Insight Failure / Anosognosia

**Terms:** Lack of insight (anosognosia), partial insight

**Gap:** Self-monitoring failure in which the system does not register its own illness/error
state. The RC loop fails to update the self-model with evidence of pathological output.
No current entry addresses self-model error blindness specifically.

**Proposed failure mode:** `self-monitoring_failure.md`

**AI equivalent:** Systems that generate incorrect outputs but do not flag inconsistency
in self-monitoring; calibration failure where system confidence does not track accuracy;
RLHF-trained systems that answer confidently without uncertainty representation.

**Notes:** Important for AI safety (self-correction depends on self-monitoring). The
residue blindness entry covers absence of consequence tracking, not self-model accuracy.
These are distinct mechanisms.

---

### 6. Nihilistic Delusion / Cotard Syndrome

**Terms:** Nihilistic delusion / Cotard

**Gap:** Cotard represents maximal maintenance loop collapse plus self/world representation
failure. The self and world are represented as absent or destroyed. This is distinct from
residue blindness (absent harm tracking) and from depressed mood (negative valence): it
is absence of self/world representation in the viability map. 

**Proposed failure mode:** Extend maintenance loop documentation; possibly add to
`docs/psychiatric_predictions.md` as additional P-series prediction.

---

## Partial coverage — improvements to existing entries

These terms are covered mechanistically but would benefit from explicit mention or
additional sub-section in their existing entries.

| Term | Current entry | Recommended addition |
|---|---|---|
| Secondary delusion | belief_fixation.md | Add note: secondary delusion = feedback entrapment producing delusion; primary/secondary distinction maps onto two different mechanism types |
| Deja vu / jamais vu | confabulatory_completion.md? | Add as familiarity-signal dissociations; inverse comparator failures vs confabulation |
| Delusional percept | precision_misallocation.md | Add as specific clinical form of aberrant salience; cite Kapur 2003 |
| Delusional atmosphere | precision_misallocation.md | Add as pre-delusional diffuse precision elevation; prodromal state |
| Thought blocking | commitment_dysregulation.md | Add as paralysis applied to thinking stream |
| Flight of ideas | commitment_dysregulation.md | Add as impulsivity applied to thinking stream |
| Obsession | feedback_entrapment.md | Add as obsessional rumination loop with ego-dystonic quality |
| Phobia | precision_misallocation.md | Add connection to fear-avoidance / pain_architecture.md |
| Depersonalisation | provenance_collapse.md | Add as self-model/self-experience mismatch — distinct from real/synthetic; may need its own subsection |
| La belle indifference | pain_architecture.md | Add as clinical form of z_harm_s / z_harm_a dissociation type |
| Pseudohallucination | provenance_collapse.md | Add as partial hypothesis-tag failure (the concepr of a hypothesis tag this may itself be considered a belief); beleif related errors may be graded rather than binary and subject to the different mechanisms failure of beleif |
| Anhedonia | docs/psychiatric_predictions.md | Expand P-002 to address wanting/liking dissociation; link to goal_proxy_lock_in.md |
| Cryptomnesia | provenance_collapse.md | Add as specific form: retrieved-as-generated (compare to generated-as-retrieved) |
| Ideas of reference | precision_misallocation.md | Add as sub-delusional aberrant salience; cite as prodromal marker; susceptibility of humans to communication attribution to errors may have important reasons |

---

## Mechanism type coverage: gaps and proposals

The 7-type classification in `docs/psychopathology_usage.md` has one identified gap:

### Proposed 8th type: Agency misattribution

| Property | Value |
|---|---|
| **Name** | Agency misattribution |
| **Definition** | The mechanism for attributing self/other authorship of mental events is absent or inverted; internally generated states (thoughts, feelings, actions) are attributed to external agents |
| **Human substrate (structural)** | Efference copy mismatch: motor system forwards corollary discharge to predict sensory consequence of own action; when efference copy is absent or misrouted, own actions are perceived as externally caused. Lateral prefrontal self-tagging circuitry. Inferior frontal gyrus source monitoring |
| **AI structural equivalent** | System produces output but self-authorship marker is absent from or incorrect in the self-model; own outputs re-enter as external inputs; no self-tagging gate on generated content |
| **Covered by** | Not yet in taxonomy |
| **Relationship to comparator failure** | Subtype: the comparator specifically being absent is the self/other attribution comparator, not the real/synthetic comparator (provenance collapse) |

---

## New terms from Fish's not yet in mechanism taxonomy

Several Fish's phenomenological terms do not cleanly map to any existing mechanism type.
These may require new mechanism entries or mechanism extensions:

| Term | Gap |
|---|---|
| Alexithymia | Representation present but not connected to reporting pathway — neither representation absence (generated) nor precision dysregulation (attenuated). Possible new type: representation inaccessibility |
| Overinclusive thinking | Conceptual boundary precision failure — not salience misallocation but category-membership threshold too low |
| Concrete thinking | Absence of representational tier — not a failure mechanism but a structural absence of abstraction layer |
| Incongruent affect | Cross-channel coherence failure — RC loop does not check consistency between affective and cognitive output channels |

---

## Proxy displacement — notable absence from Fish's

Fish's does not contain phenomenological terms corresponding to proxy displacement
(goal_proxy_lock_in). This is architecturally expected:

Proxy displacement produces behavioural consequences (persisting in goal-substituted behaviour)
that do not have a distinctive phenomenological form visible to the person experiencing them.
The person does not experience "I am pursuing a proxy for my real goal" — they experience
normal goal-directed behaviour toward what has become their effective goal. The failure is
visible in behaviour over time (OAI: means-end reversal; Berridge wanting without liking),
not as an experienced mental event. Fish's catalogues form-of-experience, so proxy displacement
is structurally outside its scope, though may capture some of the effects of this in addiction
phenomenology with narrowing of repertoire potentially being a downstream effect of this.

This is a case where the AI architectural concept has no psychopathological phenomenological
form — but does have recognisable behavioural and neurobiological correlates (cortico-striatal
shift, Berridge dissociation) that are well-described outside Fish's.

---

## Summary: prioritised action list

1. **Add 8th mechanism type** (agency misattribution) to `docs/psychopathology_usage.md`
2. **New failure mode entry:** `agency_attribution_failure.md` — passivity phenomena cluster
3. **New failure mode entry:** `episodic_consolidation_failure.md` — anterograde/retrograde amnesia
4. **New failure mode entry:** `entity_attribution_failure.md` — Capgras/Fregoli/reduplicative paramnesia
5. **New failure mode entry:** `self_monitoring_failure.md` — anosognosia/insight failure
6. **Extend existing entries** per the partial coverage table above (secondary delusion, obsession, delusional percept, phobia, depersonalisation, pseudohallucination)
7. **Add Cotard/nihilistic delusion** as a P-series prediction or extended maintenance loop note
8. **Update README table** with new entries when added
