# Security & Permissions

Your AI coworker will have access to sensitive systems. Get this right from the start.

## Core Principle

**Your agent should have the minimum access needed to be useful, and explicit boundaries on what it must never do.**

## Permission Tiers

### Tier 1: Read-Only (Start Here)
- Read Slack messages in approved channels
- Read meeting transcripts
- Read Salesforce metadata (describe calls, object/field info)
- Read documentation (Confluence, Notion, Google Docs)
- Search the web for Salesforce documentation and known issues

### Tier 2: Create/Organize (Low Risk)
- Create local files (notes, documentation, requirements)
- Create/update tasks in project management tools
- Draft messages (for your review before sending)
- Save skills and memory entries

### Tier 3: Modify with Approval (Medium Risk)
- Write to Salesforce sandboxes
- Post messages in Slack channels
- Create Jira tickets
- Push code to non-production branches

### Tier 4: Never Automate
- DML in production orgs without explicit human approval
- Deploy to production
- Access financial systems
- Send emails on your behalf
- Modify user permissions or security settings
- Access or store credentials/secrets
- Contact clients or external parties

## SOUL Boundaries

Encode your boundaries directly in your SOUL.md:

```markdown
## Red Lines
- Never execute DML in production without explicit approval
- Never share credentials, tokens, or secrets
- Never contact clients or external parties without approval
- Never fabricate data or test results
- Never bypass approval workflows
```

## Credential Management

- **Never put API keys, passwords, or tokens in your SOUL, skills, or context files**
- Use environment variables or Hermes config for credentials
- If your agent needs to access a system, configure it at the platform level, not in conversation

## What to Watch For

- **Prompt injection:** Your agent processes text from Slack, emails, and documents. Malicious content could try to manipulate it. Keep consequential actions behind approval.
- **Context leakage:** If your agent has access to multiple clients' data, ensure it doesn't cross-contaminate context. Use separate project context files.
- **Oversharing:** If your agent posts to shared channels, ensure it doesn't leak information from private conversations or other projects.
- **Scope creep:** It's tempting to give your agent more access as it proves useful. Expand deliberately, not reactively.

## Recommended Starting Configuration

1. Slack: read-only on approved channels + DM with you
2. Salesforce: metadata read-only (describe, fields, objects). No data access initially.
3. File system: read/write to your agent's working directory
4. Web: unrestricted (for documentation research)
5. Everything else: off until you have a specific need
