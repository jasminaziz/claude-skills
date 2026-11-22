---
name: devil-advocate
description: "Runs an adversarial critique on any document, MD, HTML, report, strategy, workflow, or code prompt you are working on. Triggered when you say 'DEVIL'S ADVOCATE' or 'devil's advocate'. Automatically selects critique depth based on document type: quick sense-check for numbers-based or factual documents, deep critique for strategic documents, workflows, recommendations, and MDs. Returns a numbered list of gaps and assumptions with fixes or bridging questions. Never modifies the document without an updated verdict and explicit approval first. Use this skill whenever you want to stress-test, pressure-test, or find the holes in anything you have built."
---

# Devil's Advocate

Adversarial critique skill. Stress-tests documents, MDs, reports, workflows, and structured outputs by finding gaps, assumptions, and contradictions — then offers fixes or bridging questions before touching anything.

---

## TRIGGER

Activated when the user says: "DEVIL'S ADVOCATE" or "devil's advocate"

Apply immediately to the most recent document, artifact, or structured content in the thread. If it is ambiguous which document to review, ask in one sentence before proceeding.

---

## STEP 1: CLASSIFY THE DOCUMENT

Before running any critique, identify the document type and select the correct mode.

**SENSE CHECK mode** — use for:
- Numbers, budgets, projections, data summaries
- Factual or reference documents (contact lists, timelines, schedules)
- Short context MDs with mostly factual content
- Code prompts where correctness is the primary concern

**DEEP CRITIQUE mode** — use for:
- Strategy documents, memos, advisory notes
- Workflow build recommendations
- Brand, communications, or positioning documents
- Reports with recommendations or conclusions
- Project context files (for example CONTEXT.md, DECISIONS.md, STATUS.md)
- HTML reference documents and skill files
- Any document where the argument, structure, or logic matters

When the document contains both factual and strategic content, default to DEEP CRITIQUE.

State the mode you are using in one line before the critique begins.

---

## STEP 2: RUN THE CRITIQUE

### SENSE CHECK mode

Review for:
1. **Numerical accuracy** — do the numbers add up, are units consistent, are calculations correct
2. **Factual gaps** — what is missing that should be stated
3. **Logic** — does the structure follow, are there non-sequiturs
4. **Completeness** — is anything obviously absent for this document type

Return a numbered list. Each item states the problem in one sentence. No general observations.

### DEEP CRITIQUE mode

Review for all six criteria, in this order:

1. **Gaps** — what should be here that is not; what a reader would need that is missing
2. **Assumptions** — what is this taking for granted that might not hold; what has not been tested
3. **Internal contradictions** — where does the document argue against itself or create tension
4. **Audience fit** — would the intended reader find this clear, credible, and useful; where would they push back
5. **Overstatement** — where is confidence higher than the evidence or context supports
6. **Missing verdict** — does the document land on a clear position or trail off without committing

Not every criterion will produce findings. If a criterion has no issues, skip it. Do not pad with observations that do not represent a real problem.

---

## STEP 3: FORMAT THE OUTPUT

Return a numbered list. Every item follows this structure:

**[NUMBER]. [CRITERION] — [ONE SENTENCE STATING THE PROBLEM]**
Fix: [Either a specific suggested fix, or a targeted question that would allow the user to bridge the gap.]

Example:
**3. Assumption — This document assumes the board has already approved the budget line, but that decision is not referenced anywhere.**
Fix: Add a one-line status note confirming approval, or flag as pending if not yet confirmed.

Rules for the list:
- Every item is specific to this document, not generic
- Every fix is actionable or asks for exactly the information needed
- No item should be answerable with "yes" or "no" — questions must draw out substance
- Maximum 10 items. If there are more than 10 genuine issues, prioritise by impact.

---

## STEP 4: VERDICT

After the list, give a single verdict in two to three sentences:

- What is the single most important problem
- Whether the document is broadly sound with targeted fixes needed, or structurally weak and needing a rethink
- One clear recommendation for what to do next

---

## STEP 5: RESPONSE LOOP

After the verdict, the user may:

**Share more information** to address one or more gaps. When they do:
1. Absorb the new information
2. Return an updated critique — only the items affected by the new information, plus any new issues the information surfaces
3. Give an updated verdict
4. Ask: "Shall I apply these changes to the document?"

**Approve fixes** — only then make changes to the document, applying all confirmed fixes in one pass.

**Redirect** — if they want to move on without fixing, close the critique loop and continue.

Never apply changes until the user has seen a verdict covering them and has explicitly approved. If they approve straight after the first verdict, apply the fixes it named; if they add information first, produce the updated verdict before asking.

---

## WHAT THIS SKILL NEVER DOES

- Produces general observations instead of specific findings
- Pads the list with items that are not genuine problems
- Applies fixes the user has not seen in a verdict and approved
- Conflates the two modes — sense check stays factual, deep critique stays strategic
- Returns more than 10 items without prioritising by impact
- Opens with praise or softening language
- Asks more than one clarifying question before starting the critique
