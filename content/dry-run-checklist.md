# Dry Run Checklist — Video 2 (Scout Setup)

## Goal
Walk through the exact setup process on a clean machine (or clean profile) to:
1. Identify friction points before recording
2. Time each section
3. Capture exact commands and screens needed

## Pre-Recording Setup

### On your work machine:
- [ ] Hermes installed (`pip install hermes-agent` or `uv pip install hermes-agent`)
- [ ] Anthropic API key ready (don't show on camera — paste off-screen or pre-configure)
- [ ] Slack workspace ready (use your work Slack or a test workspace)
- [ ] Slack app pre-created OR create live on camera (see below)
- [ ] Terminal with clean history (no sensitive commands visible)
- [ ] Clone the scout repo: `git clone https://github.com/mahlerdan/salesforce-ai-coworker.git`

### Slack App Setup (do this before recording OR show live)
1. Go to https://api.slack.com/apps
2. Create New App → From scratch
3. Name: "Scout" (or whatever the viewer names theirs)
4. Bot Token Scopes needed:
   - `chat:write`
   - `im:history`
   - `im:read`
   - `im:write`
   - `users:read`
   - `app_mentions:read`
   - `channels:history` (if monitoring channels)
   - `groups:history` (if monitoring private channels)
5. Install to workspace
6. Copy Bot Token + App Token
7. Configure in Hermes:
   ```bash
   hermes config set slack.bot_token xoxb-...
   hermes config set slack.app_token xapp-...
   ```
8. Start gateway: `hermes gateway slack`

**Decision:** Show Slack app creation live or pre-create and just show the config step?
Recommendation: Pre-create but briefly show the api.slack.com screen with the scopes
highlighted. Full Slack app creation is boring on camera and error-prone. Link to
docs/slack-setup.md in the repo for the detailed walkthrough.

## Dry Run Steps

### 1. Install (time target: 2 min)
```bash
# If clean machine:
pip install hermes-agent
hermes --version

# Initial setup:
hermes setup
# Select provider: Anthropic
# Paste API key
```

### 2. Create Profile (time target: 1 min)
```bash
hermes profile create scout
hermes profile switch scout
```

### 3. Configure SOUL (time target: 3-4 min)
```bash
# Copy template from repo
cp ~/Projects/salesforce-ai-coworker/templates/SOUL.md ~/.hermes/profiles/scout/SOUL.md

# Edit live — fill in:
# - Name: Scout
# - Your name and role
# - 1-2 Salesforce orgs
# - Products you use
# - Red lines
```

### 4. Add Starter Skills (time target: 1 min)
```bash
cp ~/Projects/salesforce-ai-coworker/skills/examples/*.md ~/.hermes/profiles/scout/skills/
```

### 5. Test in CLI (time target: 1 min)
```bash
hermes chat
# "Hey Scout, what do you know about me?"
# Should reflect SOUL content
# "I just got out of a meeting about building a case management portal in Service Cloud.
#  Here are my notes: [paste sample notes]"
# Exit
```

### 6. Connect Slack (time target: 2 min)
```bash
# Pre-created Slack app, just configure:
hermes config set slack.bot_token xoxb-...
hermes config set slack.app_token xapp-...
hermes gateway slack
```

### 7. First Slack Message (time target: 1 min)
- DM Scout in Slack
- "Hey Scout, are you there?"
- Show response
- Paste meeting notes, show requirements output

## Sample Meeting Notes for Demo

Use these (or adapt from a real meeting):

---
Meeting: Case Management Portal - Requirements
Client: [Redacted]
Date: [Today]

- client wants customers to log in and see their cases
- need to submit new cases from portal
- they use Service Cloud, have about 3000 contacts
- CEO mentioned wanting to see account info too — billing address, contact list
- they asked about knowledge articles — maybe phase 2?
- need to handle file attachments on cases — they send a lot of screenshots
- security is big concern — each contact should only see their own cases
- mobile access important — field techs use phones
- they want email notifications when case status changes
- talked about SLAs briefly but no decisions made
- timeline: want to launch in Q1
- current process is all email based — no visibility into case status
- asked about chatbot on portal — I said let's scope separately
---

## Timing Notes (fill in during dry run)

| Section | Target | Actual | Notes |
|---------|--------|--------|-------|
| Install | 2 min | | |
| Profile | 1 min | | |
| SOUL | 3-4 min | | |
| Skills | 1 min | | |
| CLI test | 1 min | | |
| Slack | 2 min | | |
| First msg | 1 min | | |
| **Total** | **11-12 min** | | |

## Known Friction Points to Watch For

- [ ] `hermes setup` — does it prompt cleanly? Any confusing options?
- [ ] Profile creation — any permissions issues?
- [ ] SOUL file location — is the path obvious?
- [ ] Slack gateway — does it connect on first try? Error messages?
- [ ] First response — how long does Scout take? Timeout risk?
- [ ] API key — don't accidentally show it on camera

## Post Dry Run

- Note anything that was confusing or took longer than expected
- Update video script with actual commands (not guesses)
- Update docs/getting-started.md if any steps were wrong
- Decide if Slack app creation should be live or pre-done
