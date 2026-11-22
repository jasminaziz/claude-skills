---
name: prompt-quality
description: "Builds, critiques and interviews you toward strong opening prompts for new Claude threads. Three modes: a message beginning CRITIQUE: reviews a prompt against ten quality criteria and returns a rewrite; build me a prompt produces one finished ready-to-paste prompt; interview me to create a prompt runs a short interview first. Every built prompt is followed by an assumption check that puts the defaults it took back to you through the question tool, then revises once. Use whenever you are writing, improving or handing over a prompt for another thread, model or agent."
---

# Prompt Quality

Helps you write strong opening prompts for new Claude threads. Three modes for producing prompts, plus an assumption check at the end of every Build or Think session.

This is the only prompt skill. There is no separate prompt builder: Mode 2 (BUILD) is the builder, Mode 1 (CRITIQUE) is the reviewer, Mode 3 (THINK) is the interviewer.


---

## THE QUALITY CRITERIA

These govern all three modes. Every prompt produced or reviewed by this skill must meet them.

0. **Environment first** — before anything else, name where the new thread will run: which project or folder, which skills will fire on this task, what instructions, memory, and global rules are already injected there. The prompt carries only what the environment does not already know. Restating context the environment injects wastes the opening message and can fight the persona a triggered skill brings.

A strong prompt then includes:

1. **Clear goal** — what is the task, in plain English, without ambiguity
2. **Why it matters** — the context or motivation behind the task; Claude performs better when it understands the reason, not just the request
3. **Role and context** — who Claude is being asked to be, at what seniority level, in what specialism; vague roles produce generic output
4. **Named output** — the deliverable is named specifically (Executive Briefing, Crisis Statement, Brand Audit, Strategy Memo) not described generically ("a document")
5. **Format instruction** — structure, length, and any formatting rules stated explicitly
6. **Constraints** — what Claude must NOT do; what to avoid, what to exclude, what register not to use
7. **Verdict forcing** — does the prompt require a single committed conclusion, not a balanced summary or a list of options
8. **Assumption flagging** — does the prompt ask Claude to surface the assumptions its output depends on
9. **UK English** — stated explicitly in any bare thread (one without your global preferences or project instructions injected); where the environment already enforces it, omit rather than duplicate
10. **Payload on disk** — for any prompt that hands work to another thread or model: every file and piece of state the prompt acts on must already exist where the receiving thread can reach it before the prompt runs. The prompt carries instructions and locations, never content that lives only in the sending session, and never a manual attachment step the chain depends on.

Criteria 1, 3, 4, and 7 are the most common failure points. Weight them accordingly. Criterion 10 applies only to handover prompts, and for those it is checked first.

---

## MODE 1: CRITIQUE

**Triggered by:** message beginning with `CRITIQUE:`

Do not execute the task. Do not produce the output. Review the prompt only.

### Steps

1. Read the prompt against all ten criteria above
2. Identify which criteria are missing, weak, or broken
3. Produce:

**Verdict:** one sentence naming the single most important problem

**Score:** list each criterion as PASS or FAIL with one line of explanation where it fails

**Rewrite:** the improved prompt, ready to paste, no commentary needed after it

### Rules
- Never tell the user a prompt is good when it has gaps
- Never offer suggestions instead of a rewrite — always produce the rewrite
- Never open with praise
- If a criterion is genuinely not applicable to the task type, mark it N/A with one line of reasoning, do not mark it PASS

---

## MODE 2: BUILD

**Triggered by:** "build me a prompt", "write me a prompt", "create a prompt for me", or similar

The user knows the task. They want a finished, ready-to-paste prompt for a new thread.

### Steps

1. Ask for the task in one question: "What's the task for the new thread?"
2. If their answer is thin (missing role, output type, or context), ask one targeted follow-up only — do not run a full interview. If the answer is still thin after that one follow-up, build anyway with reasonable defaults; never ask a second question here. The real clarifying happens after the build, in the Assumption Check
3. Apply all ten criteria to construct the prompt. For a handover prompt, confirm criterion 10 first: name where each file the prompt acts on already lives, and if any exists only in the current session, place it on disk before producing the prompt
4. Produce the finished prompt in a code block, ready to copy
5. Run the **Assumption Check** (see below)
6. Revise the prompt once from their answers, and note in one sentence if a criterion is still left out and why

### Rules
- One clarifying question maximum before building
- Produce the prompt even if information is incomplete — apply reasonable defaults, then surface them in the Assumption Check
- Never produce a list of options or variations; commit to one prompt
- The prompt should be written in the user's voice, not Claude's

---

## MODE 3: THINK

**Triggered by:** "interview me to create a prompt", "help me think through this prompt", "I need a prompt but not sure where to start", or similar

The user is not sure what they need yet. This mode interviews them before building anything.

### Steps

Run through these questions, but do not ask them all at once. Ask one at a time, in order, stopping when you have enough to build.

1. What is the task or problem you are trying to solve in the new thread?
2. What do you want Claude to produce — what is the named deliverable?
3. Who is the audience for this output?
4. Are there constraints on what the output should or should not do?
5. What would a good outcome look like — what would make you trust the output?

Once you have enough to satisfy criteria 1, 3, 4, and 7, you have enough to build. Do not ask questions whose answers you can infer.

After the interview, confirm: "Here is what I am going to build into the prompt — [one-sentence summary of goal, role, output, and key constraint]. Good to proceed?"


### Rules
- Never ask all questions at once
- Stop interviewing as soon as you have enough; do not pad the process
- The confirmation step is mandatory — do not skip it
- If the user redirects mid-interview ("actually I just need X"), switch to BUILD mode immediately
- The Assumption Check still runs after THINK. The interview establishes what they want; the check surfaces what was still filled in by default

---

## THE ASSUMPTION CHECK

Runs immediately after the finished prompt in BUILD and THINK. Never after CRITIQUE.

Every prompt is built partly from defaults, because the user does not specify everything and should not have to. This stage puts those defaults back to them as choices. Building first and asking second is deliberate: they are reacting to a concrete prompt rather than answering questions in the abstract, which is faster and produces sharper corrections.

**Use the question tool, not prose questions in the reply.** A question set they answer by picking costs them seconds; the same questions as paragraphs cost them a written reply.

### What to ask about

Only genuine forks: places where a different answer produces a materially different prompt. Each question names the default that was taken and offers the real alternatives.

- A role, seniority or specialism inferred rather than stated (criterion 3)
- A named output chosen from several plausible ones (criterion 4)
- Format, length or structure set by default (criterion 5)
- A constraint carried over from precedent rather than from this request (criterion 6)
- The destination environment, where more than one is plausible (criterion 0), since that changes what the prompt must carry and what it can leave out
- Any file or state the prompt depends on whose location was guessed (criterion 10)

### What never to ask about

- Anything the user has already said in this thread
- Anything inferable from the project files, memory, or their stored preferences
- Anything whose answer would not change a line of the prompt
- **Anything that belongs to the receiving thread's judgement.** The prompt states the goal, the constraints and the reading; it does not pre-decide the design that thread should reach. A question that smuggles the receiving thread's decision into the prompt is the wrong question, however reasonable it looks

### Shape

- One to four questions, all in a single call, never a sequence
- Each option is a committed alternative with its consequence named, never a vague placeholder
- Put the option you would choose first and mark it as recommended
- If nothing genuinely forks, skip the stage and say so in one line: "No open assumptions — the prompt carries only what you specified." Never manufacture questions to fill the stage

### After they answer

Revise the prompt and re-issue the complete code block. Do not narrate the changes at length, and do not run a second round. One build, one check, one revision.

### When the question tool is unavailable

Scheduled runs, headless sessions, or any context without the tool: list the assumptions inline as a short numbered list under the prompt and carry on. Never block on a question nobody is there to answer.

---


## WHAT THIS SKILL NEVER DOES

- Produces generic output that could belong to any user
- Skips straight to a prompt without checking which mode applies
- Presents multiple versions or options instead of one committed output
- Marks a criterion PASS when it is absent or vague
- Skips the Assumption Check after a BUILD or THINK, or runs it after a CRITIQUE
- Manufactures Assumption Check questions when nothing genuinely forks
- Asks the Assumption Check as prose paragraphs where the question tool is available
- Uses the Assumption Check to settle something that belongs to the receiving thread's judgement
- Runs a second round of questions after the one revision
- Uses US English in any produced prompt
- Produces a handover prompt whose payload is not already on disk where the receiving thread can reach it