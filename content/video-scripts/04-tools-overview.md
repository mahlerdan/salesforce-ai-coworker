# Video 4: "The Tools That Make Your AI Coworker Actually Useful"

**Format:** Feature showcase + demo. 10-12 minutes.
**Goal:** Viewer understands the key Hermes capabilities beyond chat.

---

## Opening (30 seconds)

> "So far we've set up an AI coworker, given it an identity, and taught it Salesforce
> skills. But right now it only does things when you ask.
>
> This video is about the tools that make it proactive, persistent, and actually
> integrated into how you work. Memory, scheduled tasks, file access, and more."

---

## Section 1: Memory — How Scout Remembers (2-3 minutes)

> "Every time you start a new conversation with an AI, it forgets everything. That's
> the fundamental problem. You spend the first five minutes re-explaining your project.
>
> Hermes has persistent memory. Two types."

**User memory:**
> "Facts about you — your name, role, preferences, how you like things formatted.
> Scout learns these as you work together."

*[Show: a memory entry being saved after a correction]*

> "If I say 'always include complexity estimates in requirements,' Scout saves that.
> Next session, it's already there."

**Agent memory:**
> "Things Scout learns about the environment — project conventions, tool quirks,
> things that worked or didn't."

> "I don't have to re-teach my coworker every morning. That's the whole point."

**Context files:**
> "For deeper project context, I keep markdown files that Scout reads at the start
> of each session. Active projects, org details, architecture decisions, client
> preferences. Think of it as Scout's notebook."

---

## Section 2: Cron Jobs — Scheduled Tasks (2-3 minutes)

> "This is where it gets interesting. You can schedule Scout to do things automatically."

*[Show: creating a cron job]*

**Example: Daily Slack digest**
> "Every morning at 8 AM, Scout reviews approved Slack channels and sends me a
> summary. Action items, decisions, things that need my attention. I don't have
> to ask — it's just there when I open Slack."

**Example: Weekly project status**
> "Every Friday, Scout compiles a status update from my project context files.
> What moved forward, what's blocked, what's next week. I review it, edit if
> needed, and send it to stakeholders."

> "These run in the background. Scout is working even when I'm not talking to it."

---

## Section 3: File System Access (1-2 minutes)

> "Scout can read and write files on the machine it runs on. That means it can:
> - Read documentation you point it to
> - Write meeting notes, requirements, and documentation to your project folders
> - Maintain its own context files
> - Run scripts
>
> This is what makes it a coworker and not just a chat window. It has a workspace."

---

## Section 4: Terminal Access (1-2 minutes)

> "Scout has a terminal. It can run commands, install packages, run scripts, check
> logs. For Salesforce work, that means it can:
> - Run SFDX commands
> - Check deployment status
> - Run tests
> - Parse log files
> - Execute data scripts
>
> Obviously this comes with guardrails. The SOUL defines what Scout can and can't do.
> But having terminal access means Scout can actually *do* things, not just talk
> about doing things."

---

## Section 5: Web Research (1-2 minutes)

> "When Scout is troubleshooting a Salesforce issue, it can search the web. Salesforce
> docs, Known Issues, Stack Exchange, Trailblazer Community.
>
> It's not guessing from training data. It's looking up the current answer."

*[Show: Scout researching a Salesforce issue in real time]*

---

## Section 6: What's Coming (60 seconds)

> "I'm still building this out. Things I'm working on:
> - Connecting to Salesforce orgs for metadata awareness
> - Jira integration for creating and tracking stories
> - Calendar awareness for meeting prep
> - Computer use — the agent can actually interact with your screen
>
> But honestly? Memory, skills, Slack, and cron jobs cover 80% of what I need.
> Start there."

---

## Close (30 seconds)

> "These tools are what take an AI coworker from 'neat demo' to 'I actually use this
> every day.' Memory means no re-explaining. Cron means it works while you don't.
> File and terminal access mean it can do real work, not just suggest it.
>
> Next video: I'm going to walk through a full real-world workflow — taking raw
> meeting notes and turning them into a complete set of Salesforce requirements,
> start to finish."

---

## Production Notes

- **Memory demo is key.** Show a correction in one session, then show Scout remembering
  it in the next session. That before/after is the aha moment.
- **Cron job demo:** Pre-create a daily digest cron job. Show the output. If you can
  show Scout's morning summary arriving in Slack, that's the money shot.
- **Don't try to cover everything.** These are highlights. Link to Hermes docs for
  the full feature set.
- **Terminal/file demos should be fast.** Show Scout running a command, reading a file.
  Don't belabor it — viewers understand CLI access.
