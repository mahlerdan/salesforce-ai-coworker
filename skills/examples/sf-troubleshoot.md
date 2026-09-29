# Example Skill: Salesforce Troubleshooting

---
name: sf-troubleshoot
description: Systematic approach to diagnosing and resolving Salesforce issues
triggers:
  - User reports an error, bug, or unexpected behavior in Salesforce
  - User shares an error message, debug log, or stack trace
  - User asks "why is [X] not working"
---

## When to Use

When your human hits a Salesforce problem — error messages, unexpected behavior, deployment failures, governor limits, integration issues, or anything that's broken or behaving unexpectedly.

## Steps

1. **Gather context before diagnosing:**
   - What org? (Production, sandbox, dev?)
   - What were they doing when it happened?
   - Error message (exact text)
   - Is it reproducible? Since when?
   - Any recent changes? (deployments, config changes, data loads)

2. **Classify the problem type:**
   - **Apex error** → check debug logs, governor limits, null references, SOQL issues
   - **Flow error** → check flow debug, fault paths, null handling, bulkification
   - **LWC error** → check browser console, wire service, imperative calls, CSP
   - **Deployment error** → check dependencies, test coverage, metadata conflicts
   - **Permission error** → check profiles, permission sets, FLS, sharing rules, OWD
   - **Data issue** → check validation rules, triggers, workflow rules, process builders
   - **Integration error** → check named credentials, auth, callout limits, response parsing
   - **Governor limits** → check SOQL in loops, DML in loops, heap size, CPU time

3. **Research:**
   - Search Salesforce Known Issues (https://issues.salesforce.com)
   - Check Salesforce Stack Exchange
   - Check official documentation
   - Review Trailblazer Community for similar reports

4. **Propose a fix:**
   - Explain root cause clearly
   - Offer solution with specific steps
   - Flag any risks (data impact, deployment considerations, rollback plan)
   - If unsure, say so — present it as a hypothesis to test, not a certainty

5. **Document the resolution:**
   - What the problem was
   - What caused it
   - What fixed it
   - How to prevent it in the future
   - Offer to save as a skill if it's a pattern likely to recur

## Pitfalls

- Don't guess at fixes without understanding the root cause
- Governor limit issues often have multiple contributing factors — look for the pattern, not just the line
- "It was working yesterday" usually means something changed — dig into recent deployments, config changes, or data changes
- Permission issues can be layered — FLS + CRUD + sharing + profile + permission set + org-wide defaults
- Always ask which org before suggesting changes
