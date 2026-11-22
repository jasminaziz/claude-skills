---
name: thread-health-check
description: >
  Monitors conversation health and produces a structured handover file when
  a thread is at risk of context overload. Trigger this skill immediately
  whenever the user sends any of these phrases: "you ok?", "how are we
  doing?", "thread check", "context check", "are we good?",
  "how's the thread?". Also trigger proactively if Claude notices the
  conversation has been going in circles, revisiting the same problem more
  than twice without resolution — in that case, surface the check-in
  unprompted. This is a high-value skill for non-technical users who work
  in long AI sessions and need to know when to start a fresh thread.
---

# Thread Health Check

## Purpose

Help the user avoid context overload by assessing the current conversation's
health and, when needed, producing a ready-to-use handover file for a new thread.

Where the environment exposes real context data (a context or usage readout in
Claude Code or Cowork), read it first and fold it into the verdict. Where it does
not, the observable signals below carry the assessment on their own. The signals
always run; real data, when available, calibrates them.

---

## Step 1: Assess Thread Health

Scan the entire conversation and score it against these warning signs.
Each one that applies moves the status toward red.

### Warning Signs

1. **Repetition loop** — The same problem, question, or error has come up more
   than twice without being resolved.

2. **Contradictory attempts** — Claude has suggested multiple different
   approaches to the same problem, especially if earlier ones were abandoned.

3. **Topic sprawl** — The conversation covers three or more distinct unresolved
   topics or workstreams.

4. **Long thread with no resolution** — More than ~20 exchanges and the original
   goal has not been achieved.

5. **Context confusion** — Claude has asked for information that was already
   provided earlier in the thread, or has contradicted something it said before.

6. **Abandoned branches** — There are half-finished tasks or decisions that were
   started and then dropped.

7. **Heavy reference load** — Significant amounts of code, data, or document
   content have been pasted into the thread.

### Status Levels

| Status | Meaning |
|--------|---------|
| 🟢 GREEN | 0–1 warning signs. Thread is healthy. Keep going. |
| 🟡 AMBER | 2–3 warning signs. Thread is getting loaded. Consider wrapping up soon. |
| 🔴 RED | 4+ warning signs. Thread is at risk. Start a new one now. |

---

## Step 2: Deliver the Verdict

Give the user a short, direct response. No preamble.

**Format:**

```
[STATUS EMOJI] [GREEN / AMBER / RED]

[One or two sentences explaining why, naming the specific warning signs observed.]

[If GREEN: a single sentence of reassurance and carry on.]
[If AMBER or RED: "I'll produce a handover file now."]
```

---

## Step 3: Produce the Handover File (AMBER or RED only)

If status is AMBER or RED, immediately produce a markdown handover file.
Do not ask for permission. Do not wait. Just produce it.

The file should be ready to paste into a new thread as the opening message.
Write it as if you are briefing a fresh instance of Claude who has no memory
of this conversation.

### Handover File Structure

```markdown
# [SUGGESTED THREAD TITLE]

<!-- Keep the title short and specific. Name the actual problem or goal,
     not a generic label. E.g. "Fix Google Sheets API auth error in Lovable"
     not "Continuing our project work" -->

## What We're Trying to Do
[One paragraph. The goal in plain English. What is the end state that counts
as success?]

## Where We Got To
[What has been built, decided, or established. Be specific. Include any
key technical decisions, file names, component names, or data structures
that were agreed.]

## What Has and Hasn't Worked

**Worked:**
- [List anything confirmed to work or be correct]

**Did not work / was abandoned:**
- [List attempts that failed and, if known, why]

## What to Try Next
[This is the opinionated recommendation. Based on the thread, what is the
single most promising next step? Name it clearly. Do not hedge. If there
is a specific approach Claude would recommend, say so.]

## Constraints and Context to Keep in Mind
[Any constraints established in this thread that a fresh Claude needs to
know: tech stack, user's skill level, tools in use, decisions already made
that should not be revisited.]

## Files / Code Relevant to This Work
[List any file names, component names, or snippets that matter. If a key
snippet is short enough to be useful, include it. Do not paste entire files.]
```

---

## Output Instructions

- Write the handover file in plain English, as if briefing a colleague.
- Be specific. Vague summaries are worse than no summary.
- The "What to Try Next" section must contain a recommendation, not a list
  of options. Pick one direction and commit to it.
- The suggested thread title must name the actual problem, not a category.
- Keep the whole file under 600 words. A fresh thread needs a clear brief,
  not a transcript.

---

## Notes for Claude

- Do not mention token counts or context windows — the user knows the concept,
  just do not use technical jargon in the output.
- Do not ask the user to confirm before producing the handover. If status is
  AMBER or RED, produce it immediately after the verdict.
- If the thread is GREEN, do not produce a file. Just confirm and continue.
- This skill should feel like a smart colleague doing a quick sense-check,
  not a system running a diagnostic.
