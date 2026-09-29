# Example Skill: Solution Documentation

---
name: sf-solution-doc
description: Document a completed Salesforce solution with architecture, decisions, and maintenance notes
triggers:
  - User says they finished building something and wants to document it
  - User asks to create documentation for a feature, flow, integration, or customization
  - After completing an implementation
---

## When to Use

After building a Salesforce solution — custom object, Flow, Apex class, LWC, integration, or any configuration — and needing clean documentation for future reference, handoff, or client delivery.

## Steps

1. **Ask what was built** (if not already clear from context)

2. **Generate documentation using this structure:**

---

# [Solution Name]

## Overview
One paragraph: what this does, why it was built, who uses it.

## Business Problem
What business need or user request drove this solution.

## Solution Architecture

### Objects & Fields
| Object | Field | Type | Purpose |
|--------|-------|------|---------|
| | | | |

### Automation
| Type | Name | Trigger | What It Does |
|------|------|---------|--------------|
| Flow / Apex / Trigger / etc. | | | |

### Components (if applicable)
| Component | Type | Location | Purpose |
|-----------|------|----------|---------|
| | LWC / Aura / VF | | |

### Integrations (if applicable)
| System | Direction | Method | Auth | Frequency |
|--------|-----------|--------|------|-----------|
| | Inbound/Outbound | REST/SOAP/Platform Event | Named Credential / OAuth | Real-time / Batch |

## Key Decisions
- [Decision 1] — why this approach over alternatives
- [Decision 2] — tradeoffs considered

## Permissions
- Profiles/Permission Sets that grant access
- Sharing rules or OWD considerations
- Any FLS requirements

## Testing
- How to verify it works
- Key test scenarios
- Test data requirements

## Known Limitations
- What this doesn't handle
- Edge cases to watch for
- Future improvements considered but deferred

## Maintenance Notes
- What might need updating and when
- Dependencies on external systems
- Monitoring or alerting (if applicable)

---

3. **Review with your human** — documentation is only useful if it's accurate. Confirm details before finalizing.

4. **Save to project context** — add a reference to the documentation in the relevant project context file.

## Pitfalls

- Don't over-document simple config — a formula field doesn't need an architecture diagram
- DO document *why* — the what is in the metadata; the why disappears if you don't write it down
- Include the decisions that were *rejected* — "we considered X but chose Y because Z" prevents future teams from re-evaluating the same options
- Permissions are almost always under-documented — be thorough here
