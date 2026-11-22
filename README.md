# Claude skills for people who think for a living

Three skills I use every day with Claude. I'm a communications strategist, and I wrote these to fix problems I kept running into: work that looked finished but hadn't been tested, prompts that left a new thread guessing, and long sessions that went off the rails.

A skill is a set of instructions Claude loads when a task calls for it. Each one here is a single file you can read in one sitting and change to suit how you work.

| Skill | The problem it solves | Say this to use it |
|---|---|---|
| [Devil's advocate](skills/devil-advocate/SKILL.md) | You've written a strategy, a plan or a brief, and everyone who has read it agrees with it. Nobody has tried to break it. | "devil's advocate" |
| [Prompt quality](skills/prompt-quality/SKILL.md) | You're handing work to a new Claude thread or agent, and the prompt leaves it to guess the goal, the reader or what done looks like. | "build me a prompt", "interview me to create a prompt", or start a message with "CRITIQUE:" |
| [Thread health check](skills/thread-health-check/SKILL.md) | A long session has started going in circles, and you can't tell whether to push on or start again. | "you ok?" or "thread check" |

## What each one does

**Devil's advocate** reads the document in front of it and decides how hard to push: a quick sense check for numbers and facts, a deep critique for anything that argues or recommends. It returns at most ten problems, each with a fix or the one question that would close the gap, then a verdict. It never changes your document until you've seen the updated verdict and said yes.

**Prompt quality** holds every prompt to ten criteria, after a check most people skip: where the new thread will run and what it already knows. It builds the prompt first, then asks you about the defaults it had to assume, because reacting to a real draft is faster than answering questions in the abstract. It commits to one prompt, never a menu of options.

**Thread health check** scores the conversation against seven warning signs: going in circles, abandoned approaches, too many open threads at once. It answers green, amber or red. On amber or red it writes a handover brief you can paste into a fresh thread, with a clear recommendation for the next step.

## How to install

**In the Claude app (claude.ai or the desktop app):**
1. Download the skill's folder from this repo (open the folder, then use the download option, or download the whole repo as a ZIP from the green Code button).
2. Zip the single skill folder, for example `devil-advocate`, so the zip contains `devil-advocate/SKILL.md`.
3. In Claude, go to Customize, then Skills. Click the + button, choose Create skill, then Upload a skill, and pick the zip.

Skills need code execution turned on in your Claude settings.

**In Claude Code:**
Copy the skill's folder into `~/.claude/skills/` on your computer. Claude Code picks it up in your next session.

## Make them yours

Each skill is plain text. Change the trigger phrases, the criteria or the tone to fit your own work. They are written in UK English and they ask Claude to take a position rather than list options; if you prefer otherwise, edit the rules in the file.

## About me

I'm Jasmin Aziz, a communications strategist for values-led organisations, with AI built into how I deliver. More at [jasminaziz.co.uk](https://www.jasminaziz.co.uk), and essays on working with AI on [Substack](https://jasminaziz.substack.com).
