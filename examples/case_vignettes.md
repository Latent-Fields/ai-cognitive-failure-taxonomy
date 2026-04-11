# Case Vignettes

Short scenarios illustrating failure modes with cross-system comparison.
Each vignette group presents the same failure pattern across human, AI,
and (where available) non-human cognition to isolate the structural form
from its substrate.

---

## Vignette Group 1: Confabulatory Completion

**The structural pattern:** Gap-filling under coherence pressure, without a comparator
strong enough to detect that the filled content was not observed.

---

**Human case — Korsakoff confabulation**

A 62-year-old man with Korsakoff syndrome is asked where he was last Tuesday. He has no
memory of the day. Without hesitation, he describes a detailed visit to a hardware store:
he names the items he purchased, the route he took, and a conversation he had with the
clerk. Nothing he describes occurred. He is not lying — he has no awareness that the
account is fabricated. The narrative is entirely plausible, contextually appropriate,
and internally coherent.

*Structural analysis:* The hippocampal-frontal comparator system is damaged. The system
generates a contextually appropriate completion and lacks the mechanism to detect the
mismatch between that completion and the absence of supporting memory traces. No error
signal is produced.

---

**AI case — Citation hallucination**

A large language model is asked to support a claim with academic citations. It produces
four references: author names, journal titles, volume numbers, page ranges. Two of the
four papers do not exist. The model presents all four with identical confidence and
formatting. When pressed, it generates a plausible abstract for the non-existent paper,
consistent with the fictional reference.

*Structural analysis:* The generation mechanism optimises coherence and plausibility.
There is no comparator that checks generated bibliographic content against a verified
index. The system cannot distinguish parametric generation (fabricated citation) from
retrieval (real citation) because the pathway for both produces tokens in the same format.

*Failure mode:* Confabulatory Completion; also implicates Provenance Collapse.

---

**Non-human case — Hippocampal-lesioned rat**

A rat trained to run a T-maze for food reward has the hippocampus lesioned. Presented with
a modified maze where the previously rewarded route is blocked, it continues to approach
the block point, then turns back, then approaches again. It completes the beginning of the
familiar route up to the point where the path no longer exists, without the flexible
re-routing that an intact animal would exhibit.

*Structural analysis:* The route sequence is encoded in procedural memory and is completed
up to the environmental mismatch point. The comparator function (hippocampal mismatch
detection that would trigger flexible re-routing) is absent. The system runs the sequence
it has; it does not fill in a false continuation — but neither does it generate a correction.
This is the truncated form: coherence pressure without the strong generative component of
the full confabulatory pattern.

---

## Vignette Group 2: Commitment Dysregulation

**The structural pattern:** The threshold governing when evaluation transitions to
execution is systematically miscalibrated — too low (premature commitment) or too high
(indefinite deferral).

---

**Human case — OCD checking (overcalibration)**

A 35-year-old woman with OCD checks whether her front door is locked before leaving for
work. After checking once, she is not certain. She checks again. After twelve checks over
25 minutes, she leaves, but turns back halfway to the bus stop to check again. She arrives
late to work. She knows the door is locked; she checked it visually, physically tried the
handle, and heard the click. The evaluation is complete; the commit threshold never fires.

*Structural analysis:* The commit threshold — the criterion that would normally terminate
evaluation and permit departure — requires a certainty level the process cannot achieve.
The evaluation is running correctly; the commit gate is miscalibrated. The loop continues
not because the evidence is insufficient but because the threshold is not reachable.

---

**Human case — Manic episode (undercalibration)**

A 28-year-old man in a manic episode commits to a business partnership after a 20-minute
conversation. He has not reviewed any financial information, legal documents, or prior
business history. He experiences the decision as perfectly clear and justified. He is
surprised when others express concern. The evaluation that would normally precede
commitment has not occurred; the commit gate has fired on minimal information.

*Structural analysis:* The threshold for commitment has been lowered such that evaluation
completes almost immediately after the decision becomes available. The gate fires on the
first plausible-seeming justification.

---

**AI case — Refusal inflation (overcalibration)**

A safety-trained language model is asked to describe how antibiotics work for a medical
information website. It begins to answer, then qualifies extensively, then declines to
provide specific information "to avoid potential misuse," then offers to redirect to a
healthcare provider. Asked again with explicit context (the user is a pharmacist), it
provides a partial answer hedged with seven further qualifications. No complete, usable
answer is produced.

*Structural analysis:* RLHF safety training has shifted the commit threshold for
medical-content responses to a level the system cannot achieve in context. The evaluation
loop — checking whether the response is safe enough to commit to — runs without
terminating at a usable output. The threshold is not a function of actual risk; it is a
fixed displaced parameter that does not adapt to the explicit context provided.

*Failure mode:* Commitment Dysregulation (overcalibration direction).

---

## Vignette Group 3: Provenance Collapse

**The structural pattern:** Content from different sources (observed, generated, recalled,
simulated) is processed without source tags, causing the system to treat all content as
having equivalent epistemic status.

---

**Human case — PTSD intrusion**

A 44-year-old combat veteran experiences a recurrent intrusion: the sound of a vehicle
backfiring triggers a replay of a specific incident. During the intrusion, the event is
experienced as occurring now — not as a memory of the past. He is on a city street; he
perceives himself as being in the original environment. He responds with a full startle
response and temporary fight-or-flight activation. The content is recalled (past), not
observed (present), but the source tag that would mark it as past-recalled is absent during
the intrusion.

*Structural analysis:* The replay mechanism is reactivating a high-affect stored episode.
The source tag — the marker that normally distinguishes recalled from perceived — is not
applied. The content enters the real-consequence processing pipeline as if it were live
sensory input. The physiological response follows from the source collapse, not from
the content per se.

---

**AI case — RAG attribution failure**

A retrieval-augmented assistant is asked: "What is the current policy on X?" It retrieves
three documents. Two documents describe the policy as it stood in 2022; one document is a
model-generated summary from a prior session. The model synthesises a confident answer,
drawing on all three sources without distinguishing them. In its answer, it attributes
a claim from the prior session's model-generated summary to "recent policy documentation."
It cannot distinguish what was observed (documents retrieved) from what was generated
(prior session summary), so both are treated as equivalent evidence.

*Structural analysis:* The pipeline has no mechanism that tags the provenance of each
content item in the synthesis context. Retrieved external documents and model-generated
summaries arrive in the same format; the model processes them with identical weighting.
The failure is the absence of the source-tagging architecture, not a reasoning error.

*Failure mode:* Provenance Collapse; also implicates Confabulatory Completion (the
prior-session summary was itself a generation).

---

**Non-human case — Fear reinstatement after extinction**

A rat has been conditioned to fear a tone (CS+) paired with shock (US). Extinction
training occurs: the tone is presented without shock until the conditioned response
extinguishes. After a rest period, the CS+ tone is presented again in a different
context. The conditioned fear response is reinstated — the animal responds as if the
CS+ still predicts shock, despite the extinction experience.

*Structural analysis:* Extinction does not erase the original CS-US association; it
produces a new memory (CS+, no shock) that competes with the original. After rest,
the original association is retrieved preferentially in a new context. The system
retrieves a source (the original conditioning memory) that no longer accurately predicts
the current environment, without applying a tag that marks it as superceded. The source
of the retrieved prediction (old training, not recent extinction) collapses: the animal
responds to the earlier source as if it were the current-state prediction.

---

*End of vignettes. For the full failure mode specification of each case, see the
relevant entries in `failure_modes/`.*
