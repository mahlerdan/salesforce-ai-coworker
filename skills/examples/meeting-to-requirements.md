# Example Skill: Meeting Notes → Requirements

> This is a template. Adapt it to your actual workflow.

---
name: meeting-to-requirements
description: Transform meeting notes or conversation transcripts into structured Salesforce requirements
triggers:
  - User provides meeting notes, transcript, or conversation summary
  - User asks to extract requirements, user stories, or action items from a document
---

## When to Use

When your human shares raw meeting notes, a transcript (from tl;dv, Otter, Fireflies, etc.), or a Slack conversation and needs it turned into structured requirements.

## Steps

1. **Read the full input** — don't start processing until you've seen everything
2. **Identify the project context** — check your project context files for relevant background
3. **Extract and organize into these sections:**

### Action Items
| Owner | Action | Due | Priority |
|-------|--------|-----|----------|
| [Name] | [What] | [When] | [H/M/L] |

### Requirements (User Stories)
For each requirement identified:
```
**As a** [role]
**I want to** [capability]
**So that** [business value]

**Acceptance Criteria:**
- [ ] [Criterion 1]
- [ ] [Criterion 2]

**Salesforce Implementation Notes:**
- Object(s): [Standard/Custom objects involved]
- Approach: [Flow / Apex / LWC / Config / Integration]
- Complexity: [Low / Medium / High]
- Dependencies: [What needs to exist first]
```

### Open Questions
- [Things that were unclear, ambiguous, or need follow-up]

### Decisions Made
- [Explicit decisions captured in the meeting]

### Out of Scope (Mentioned but Deferred)
- [Items discussed but explicitly deferred]

4. **Flag gaps** — if requirements reference Salesforce features, objects, or patterns you know well, add implementation notes. If something seems risky or complex, say so.

5. **Ask before assuming** — if something is ambiguous, list it as an open question rather than guessing.

## Pitfalls

- Don't invent requirements that weren't discussed — only extract what's actually in the notes
- Meeting notes are often incomplete — flag what's missing rather than filling gaps with assumptions
- Pay attention to who said what — ownership and authority matter
- Watch for scope creep indicators — items that "might be nice" vs committed requirements
