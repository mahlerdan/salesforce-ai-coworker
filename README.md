# Scout — Your AI Coworker for Salesforce

Build your own AI coworker for Salesforce — powered by [Hermes Agent](https://hermes-agent.nousresearch.com/).

> **"I built myself an AI coworker for Salesforce. His name is Scout."**

This project is a practical, open-source guide to building an AI agent that helps Salesforce professionals do their actual jobs: reviewing meeting notes, writing requirements, troubleshooting problems, building solutions, and keeping track of everything.

This isn't a customer-facing bot. It's an AI coworker — built around how *you* work.

## What's Inside

```
├── docs/                    # Setup guides, architecture, security
│   ├── getting-started.md   # From zero to working agent
│   ├── slack-setup.md       # Connecting your agent to Slack
│   ├── security.md          # Permissions, boundaries, what to never automate
│   └── architecture.md      # How the pieces fit together
├── skills/                  
│   └── examples/            # Salesforce-oriented skill templates
├── templates/
│   ├── SOUL.md              # Starter SOUL (agent identity/instructions)
│   └── onboarding.md        # Questions to configure your agent around your work
├── scripts/                 # Utility scripts
└── content/                 # Blog posts and build-along documentation
```

## Who This Is For

- **Salesforce Admins** — action item tracking, documentation, requirements gathering
- **Business Analysts** — meeting notes → user stories, acceptance criteria, follow-up questions
- **Developers** — Apex/LWC/Flow troubleshooting, architecture review, solution documentation
- **Consultants** — project context memory, multi-client organization, research
- **Architects** — solution design thinking, integration planning, documentation

## Philosophy

- **Build for yourself first.** Your agent should make *you* measurably more productive before you try to package it for anyone else.
- **Real workflows, not demos.** Every skill and example in this repo comes from actual work.
- **Human in the loop.** The agent makes you more effective. It doesn't replace your judgment on consequential decisions.
- **Open by default.** Give away the tools. The value is in the configuration and context specific to how you work.

## Getting Started

See [docs/getting-started.md](docs/getting-started.md).

## Prerequisites

- [Hermes Agent](https://hermes-agent.nousresearch.com/) installed
- An LLM provider (Anthropic, OpenAI, etc.)
- Slack workspace (optional but recommended)

## License

MIT — use it, modify it, build a business on it.

## About

This project is maintained by [Dan Mahler](https://github.com/mahlerdan). It started as a personal experiment: *What happens when you give an AI agent deep context about your Salesforce work and let it help?*

The answer: it gets useful fast.
