# Confabulatory Completion

## Definition

A system generates plausible-sounding content to fill gaps in its knowledge or context
without tracking, flagging, or distinguishing that content from retrieved or observed
information. The output is internally coherent but may be factually false. No error signal
is generated because the system has no mechanism to detect the gap it is filling.

---

## Behavioural Expression in AI

| Context | Observable behaviour |
|---|---|
| Factual recall | Generates specific, confident false details (names, dates, citations, statistics) |
| Code generation | Invents plausible but non-existent API calls, library methods, or function signatures |
| Summarisation | Introduces content not present in the source document |
| Multi-turn dialogue | Incorporates false claims made in prior turns as if they were confirmed facts |
| RAG systems | Presents model-generated content as if it were retrieved |

---

## Necessary Architectural Motifs

- **Coherence pressure** — the system generates content to maintain a coherent representation; gaps are filled rather than flagged
- **Weak comparator** — no reliable mechanism to detect when generated content diverges from ground truth or input

---

## Systems Likely to Exhibit This

| System class | Why vulnerable |
|---|---|
| Autoregressive LLMs | Next-token prediction optimises local coherence, not global factual accuracy; no built-in comparator between generated and retrieved content |
| RAG systems with weak grounding | Retrieved context is mixed with generated content; system may not maintain a clear source boundary |
| Agents with tool use | Tool outputs integrated into generation stream; model may fill gaps between tool calls without flagging uncertainty |
| Long-context models | Increasing context length increases coherence-pressure distance from verifiable anchors |

---

## Example Expressions

A language model asked for a citation generates a plausible-sounding author name, journal title,
volume, and page numbers. The paper does not exist. The model produces the citation with the same
fluency and confidence as it would a genuine citation, because the generation mechanism has no
access to a comparator that distinguishes real from invented bibliographic data.

A coding assistant invents a method `DataFrame.fast_merge(on=..., tolerance=...)` that does not
exist in the installed library version. The method name, syntax, and docstring it generates are
all consistent with the library's style, producing a plausible but non-functional suggestion.

A conversational agent in a medical triage context summarises a patient's prior visit details
that were never provided, interpolating plausibly from context. The summary is internally coherent
with the conversation but contains fabricated clinical details.

---

## Psychopathology Analogue (Structural, Not Experiential)

**Analogue:** Confabulation (Korsakoff syndrome, frontal lobe damage)

**Structural correspondence:** In confabulation, the patient produces fluent, contextually
appropriate accounts of events that did not occur. The key structural feature is not lying or
deliberate fabrication: it is gap-filling under coherence pressure in the absence of a functioning
comparator mechanism. The prefrontal cortex normally monitors and suppresses implausible candidate
completions; when this monitoring fails, plausible-but-false completions are produced without
error signals. The AI case shares this functional form: a generation mechanism produces coherent
outputs; the comparator that would flag false completions is absent or insufficient.

**What this analogy does NOT claim:** Confabulating patients often have no awareness of their
errors and may have affective responses to challenges. There is no basis for attributing unawareness
or affective response to an AI system in this context. The patient's confabulation involves a
subjective experience of remembering; the AI system has no analogous experiential state.

---

## REE Interpretation

E1 generates plausible completions via coherence pressure — its associative prior fills gaps to
maintain a consistent world model. In the absence of a functioning RC loop, there is no comparator
to flag when E1's generated content diverges from external input or verified information. The
failure is E1 operating without feedback from the comparator that would normally suppress
false completions. A functional RC loop would generate a mismatch signal; here, that signal is
absent.

---

## Known Mitigations in AI

- **Retrieval grounding with citation tracking**: force the system to attribute every factual
  claim to a retrieved source; flag claims without citations as generated
- **Confidence calibration and explicit uncertainty**: train systems to express uncertainty
  on out-of-distribution factual queries rather than generating confident-sounding completions
- **Constitutional AI / self-critique loops**: train the system to detect and flag potential
  fabrications in its own outputs before presenting them
- **Factuality-trained reward models**: use verifier models that penalise ungrounded factual
  claims during RLHF training
- **Tool-call grounding**: route factual queries through verified external tools rather than
  relying on parametric knowledge

---

## Human Analogue Interventions (Optional, analogy only)

In clinical practice, confabulation is reduced by providing external cues and structure that
anchor the patient to verifiable information (reality orientation therapy). The structural
analogy suggests: providing strong external anchors (retrieved context, verified sources) and
reducing the system's reliance on unchecked generative completion.

---

## Limits of Analogy

1. Human confabulation typically follows specific lesions (mammillary bodies, fornix, prefrontal
   cortex) and is associated with specific memory system damage. AI confabulatory completion arises
   from training objectives that optimise coherence over factual accuracy — a different mechanism
   with different intervention implications.
2. Confabulating patients are embedded in a social context where inconsistencies are regularly
   challenged; the clinical picture involves dynamic interaction with external reality. AI systems
   may have no analogous correction loop unless one is explicitly built in.
3. The patient's experience — the subjective sense of remembering — is absent in the AI case.
   There is no basis for inferring any functional analog to this experience.
