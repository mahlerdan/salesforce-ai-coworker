# Video 2: "Build Your Own Salesforce AI Coworker — Setup"

**Format:** Tutorial / build-along. 10-15 minutes.
**Goal:** Viewer goes from zero to a working agent responding in Slack.

---

## Opening (30 seconds)

> "Last video I showed you my AI coworker for Salesforce. This is where we build yours.
>
> I'm going to walk through the exact setup I use. By the end of this video, you'll have
> an AI agent running in Slack that you can start customizing for your Salesforce work.
>
> Quick disclaimer — I'm not a DevOps person. I figured this out as a Salesforce
> professional who wanted a better way to work. If I can set this up, you can too."

---

## Section 1: What We're Building (60 seconds)

> "The agent runs on a platform called Hermes. It's open source, it connects to Slack,
> and it uses an LLM — in my case Claude — to actually think and respond.
>
> You'll need three things:
> 1. A machine to run Hermes on — your laptop works, or a cloud server for always-on
> 2. An API key from an LLM provider — I use Anthropic
> 3. A Slack workspace where you can install apps
>
> For hosting, NetworkChuck has a great video on setting up Hermes on a VPS. Link in
> the description if you want always-on access. For this tutorial, we'll run locally
> so you can see it work first."

---

## Section 2: Install Hermes (2-3 minutes)

*[Screen recording: terminal]*

> "Let's install Hermes."

```bash
# Show the install process
pip install hermes-agent
# or
uv pip install hermes-agent

hermes --version
```

> "Now we configure the LLM provider."

```bash
hermes setup
# Walk through: pick Anthropic, paste API key
```

> "That's it for the base install. Let's make sure it works."

```bash
hermes chat
# Type a test message, show it responds
# Exit
```

> "Hermes is running. Now let's give it an identity."

---

## Section 3: The SOUL — Your Agent's Identity (3-4 minutes)

> "This is the most important part. The SOUL file is what turns a generic AI into *your*
> coworker. It defines who the agent is, how it behaves, what it knows about your work,
> and what it's allowed to do.
>
> I have a starter template in the repo — link in the description."

*[Screen recording: editor with SOUL.md template]*

> "Let me walk through the key sections."

**Walk through each section, filling in example values:**

1. **Identity** — name, who you work for, your role
   > "I'm calling mine Scout. Yours can be whatever you want."

2. **What it does without asking** — research, organize, troubleshoot
   > "This is the stuff you want your agent doing immediately. No permission needed."

3. **What needs approval** — production changes, external comms
   > "This is your safety net. Anything consequential, the agent asks first."

4. **Salesforce context** — orgs, products, tech stack
   > "This is where it gets specific to you. List your orgs, what clouds you work in,
   > your tech stack. The more context here, the better Scout's answers."

5. **Projects** — active work
   > "Keep a running list. Scout uses this to connect the dots across your work."

6. **Red lines** — things the agent must never do
   > "Non-negotiable. Never touch production without approval. Never share creds.
   > Never contact clients without me saying so."

> "Save this file. We'll come back and refine it as we use Scout — the SOUL evolves."

---

## Section 4: Connect to Slack (3-4 minutes)

> "Now let's get Scout into Slack. This is the part that makes it feel real."

*[Screen recording: Slack app creation + Hermes config]*

**Steps to show:**
1. Create a Slack app at api.slack.com
2. Configure bot token scopes
3. Install to workspace
4. Copy tokens into Hermes config
5. Start the Slack gateway

> "And now..."

*[Show: DM to Scout in Slack]*

> "Hey Scout, are you there?"

*[Show: Scout responding]*

> "That's it. You have an AI coworker in Slack."

---

## Section 5: First Real Task (2-3 minutes)

> "Let's make sure this is actually useful. I'm going to paste some meeting notes and
> ask Scout to extract requirements."

*[Show: pasting notes, Scout processing, structured output]*

> "User stories, acceptance criteria, implementation notes. On the first try.
>
> But here's the thing — if that output isn't quite right, you tell Scout. 'The
> acceptance criteria need more detail.' 'Add complexity estimates.' The agent
> learns your preferences over time through its memory and skills."

---

## Close (30 seconds)

> "You now have a working AI coworker in Slack. Next video, I'm going to show you
> how to give Scout specialized Salesforce skills — meeting notes to requirements,
> troubleshooting, solution documentation, and more.
>
> Everything from this video is in the repo — SOUL template, setup guide, all of it.
> Link in the description."

---

## Production Notes

- **Dry run the entire flow before recording.** Time each section. Know where the
  friction points are so you can narrate through them naturally.
- **Have the SOUL template pre-loaded** but fill it in live. Don't skip this — it's
  the most valuable part for viewers.
- **Slack app creation has UI steps** — screen record carefully, zoom in on the
  important fields. Viewers will pause and follow along.
- **The "first real task" moment is the payoff.** Make sure you have good meeting
  notes ready. The quality of Scout's response here determines whether viewers
  continue to video 3.
- **Tone:** "I figured this out, here's how." Not "let me teach you." You're showing
  your setup, not lecturing.
