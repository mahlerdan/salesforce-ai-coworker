# Video 3: "Giving Your AI Coworker Salesforce Skills"

**Format:** Tutorial + demo. 10-12 minutes.
**Goal:** Viewer understands the skill system and builds their first custom skill.

---

## Opening (30 seconds)

> "So you've got an AI coworker running in Slack. Cool. But right now it's a smart
> generalist — it doesn't know how *you* work with Salesforce.
>
> That changes with skills. Skills are reusable instructions that teach your agent
> how to handle specific types of work. Think of them like SOPs for your AI coworker.
>
> I'm going to show you the skills I use, and then we'll build one together."

---

## Section 1: What Is a Skill? (2 minutes)

> "A skill is just a markdown file with a specific structure. It has:
> - A name and description
> - Trigger conditions — when should the agent use this skill?
> - Steps — what to do, in order
> - Pitfalls — what to watch out for
>
> When you message Scout and the request matches a skill's trigger, Scout loads
> that skill and follows the instructions. It's like giving a new hire a runbook."

*[Show: a skill file in the editor, walk through the structure]*

> "The repo has four starter skills for Salesforce work. Let me show you each one."

---

## Section 2: Starter Skills Walkthrough (3-4 minutes)

**Meeting Notes → Requirements**
> "You saw this in the last video. Paste meeting notes, get user stories with acceptance
> criteria and Salesforce implementation notes. This one skill has probably saved me
> more time than everything else combined."

*[Quick demo — show input/output]*

**Salesforce Troubleshooting**
> "When you hit an error, this skill walks Scout through a systematic diagnosis.
> Classify the problem type, check known issues, research, propose a fix, document
> the resolution."

*[Show: the skill file's diagnostic categories — Apex errors, Flow errors, LWC, etc.]*

**Slack Digest**
> "This one reviews Slack conversations and categorizes everything into action items,
> decisions made, FYI, and things needing clarification. Red, yellow, green priority."

**Solution Documentation**
> "After you build something, this skill generates clean documentation — objects,
> automation, components, integrations, key decisions, permissions, maintenance notes.
> The kind of documentation we all know we should write but never do."

---

## Section 3: Build a Custom Skill Live (4-5 minutes)

> "Those are the starters. But the real power is building skills for *your* specific work.
>
> Let me show you. I'm going to build a skill right now — a deployment checklist for
> one of my projects."

*[Screen recording: creating a new skill file]*

> "I know what my deployment process looks like. Let me teach Scout."

```markdown
# Skill: Deployment Checklist

---
name: deployment-checklist
description: Pre- and post-deployment verification for [project]
triggers:
  - User says they're about to deploy or just deployed
  - User asks for a deployment check
---

## Steps

1. Confirm which org (sandbox or production)
2. Pre-deployment checks:
   - All tests passing?
   - Code review completed?
   - Changeset or source tracking — what's included?
   - Any dependent metadata not in the deployment?
   - Destructive changes?
3. Post-deployment:
   - Smoke test key functionality
   - Check for errors in debug logs
   - Verify permissions
   - Update documentation
   - Notify stakeholders

## Pitfalls
- Watch for profile/permission set metadata — it often includes more than intended
- Validate rules and triggers in the target org may behave differently than sandbox
- Always check for hard-coded IDs (record types, queue IDs, profile IDs)
```

> "That took two minutes to write. Now every time I mention a deployment, Scout
> knows to walk me through this checklist.
>
> And here's the thing — when I inevitably forget a step and it causes a problem,
> I add that to the pitfalls section. The skill gets smarter over time."

---

## Section 4: How Skills Evolve (60 seconds)

> "Skills aren't static. After using the meeting notes skill a dozen times, I've
> refined it. Added 'Salesforce implementation notes' to the output. Added a section
> for 'out of scope items.' Made the acceptance criteria more specific.
>
> Your agent can even suggest creating new skills. If you solve a tricky problem
> and Scout notices it took several steps, it'll ask: 'Want me to save this as
> a skill for next time?'
>
> That's the loop. Use the agent → notice a pattern → create a skill → the agent
> gets better → repeat."

---

## Close (30 seconds)

> "Skills are what make this yours. The SOUL defines who your agent is. Skills define
> what it knows how to do.
>
> All the starter skills are in the repo. Grab them, customize them, and build your own.
>
> Next video: the tools that make everything work — memory, cron jobs, Slack integration,
> and more."

---

## Production Notes

- **Build the custom skill live.** Don't pre-write it and reveal. The "thinking out loud"
  about what to include is the most valuable part for viewers.
- **Show a real skill triggering.** Message Scout something that matches, show it loading
  the skill and following the steps. The connection between "I wrote this file" and "now
  the agent behaves differently" is the aha moment.
- **Keep the starter skills walkthrough brisk.** Show the output, not the full file.
  Viewers can read the files in the repo.
