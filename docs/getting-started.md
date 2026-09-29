# Getting Started

Build your own AI coworker for Salesforce in about 30 minutes.

## Prerequisites

- macOS or Linux
- An LLM provider API key (Anthropic recommended, OpenAI also works)
- A Slack workspace where you can install apps (optional but recommended)

## Step 1: Install Hermes Agent

```bash
# Install via pip (Python 3.10+)
pip install hermes-agent

# Or with uv
uv pip install hermes-agent

# Verify installation
hermes --version
```

See the [Hermes docs](https://hermes-agent.nousresearch.com/docs) for detailed installation instructions.

## Step 2: Create a Profile

A profile keeps your agent's configuration, skills, and memory separate. If you already have Hermes running for other things, create a dedicated profile for your Salesforce coworker.

```bash
hermes profile create [agent-name]
hermes profile switch [agent-name]
```

## Step 3: Configure Your SOUL

Copy `templates/SOUL.md` from this repo and customize it:

```bash
cp templates/SOUL.md ~/.hermes/profiles/[agent-name]/SOUL.md
```

Edit it with your details — your name, role, Salesforce orgs, active projects, and boundaries.

The SOUL is the most important file. It defines who your agent is, how it behaves, and what it's allowed to do. Spend time on this.

## Step 4: Add Starter Skills

Copy the example skills that match your work:

```bash
# Copy all example skills
cp -r skills/examples/* ~/.hermes/profiles/[agent-name]/skills/

# Or just the ones you want
cp skills/examples/meeting-to-requirements.md ~/.hermes/profiles/[agent-name]/skills/
cp skills/examples/sf-troubleshoot.md ~/.hermes/profiles/[agent-name]/skills/
```

## Step 5: Connect Slack (Recommended)

See [slack-setup.md](slack-setup.md) for the full guide.

The short version:
1. Create a Slack app in your workspace
2. Configure the Hermes Slack gateway with your app credentials
3. Start the gateway
4. DM your agent in Slack

## Step 6: Start Using It

The best way to configure your agent is to *use it on real work*:

- Share meeting notes and ask for requirements extraction
- Paste an error message and ask for troubleshooting help
- Describe a Salesforce problem and think through the architecture together
- Ask it to document something you just built

As you work, your agent will learn your patterns and you'll discover which skills to add, refine, or remove.

## Step 7: Run the Onboarding (Optional)

For a more structured setup, paste the contents of `templates/onboarding.md` into a conversation with your agent. It will walk you through configuring your SOUL, skills, and initial project context.

## What's Next

- **Week 1:** Use the agent on 2-3 real tasks. Note what works and what doesn't.
- **Week 2:** Refine the SOUL based on experience. Add your first custom skill.
- **Week 3:** Start connecting additional tools (Jira, GitHub, etc.) if needed.
- **Ongoing:** Your agent gets better as you use it. Correct it when it's wrong. Save new skills when you discover repeatable workflows.
