# Example Skill: Slack Review → Action Items

---
name: slack-digest
description: Review Slack messages and extract action items, decisions, and items needing attention
triggers:
  - User asks to review Slack messages or catch up on a channel
  - User shares Slack conversation and asks for a summary
  - Scheduled daily/weekly Slack review
---

## When to Use

When your human needs to process Slack conversations — catching up after being away, reviewing a long thread, or identifying what needs attention from a channel or DM.

## Steps

1. **Ingest the messages** — read the full conversation before summarizing

2. **Categorize each message/thread:**
   - 🔴 **Action needed by you** — someone asked you to do something, you committed to something, or something is blocked on you
   - 🟡 **FYI / Decision made** — important context, decisions, or updates you should know about but don't need to act on
   - 🟢 **No action** — social, resolved, or not relevant to your work
   - ❓ **Needs follow-up** — something ambiguous that should be clarified

3. **Output format:**

### Action Items
| Priority | From | What | Channel/Thread | Due |
|----------|------|------|----------------|-----|
| 🔴 | [Who] | [What you need to do] | [Where] | [When] |

### Decisions Made
- [Decision] — by [who], in [channel/thread]

### FYI / Important Context
- [Update or context worth knowing]

### Needs Clarification
- [Ambiguous item] — suggested follow-up: [question to ask]

4. **Check project context** — cross-reference action items against your active projects to add relevant context

5. **Prioritize** — if there are many action items, suggest an order based on urgency, dependencies, and impact

## Pitfalls

- Don't treat every message as important — most Slack messages are noise
- Pay attention to who is asking — requests from stakeholders/clients > requests from peers > general questions
- Watch for passive requests — "it would be great if someone could..." often means you
- Thread context matters — a message might look urgent in isolation but was already resolved in the thread
- Time-sensitive items first — something from 3 days ago that needed a response might be overdue
