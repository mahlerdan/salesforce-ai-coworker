# Skill: Salesforce CLI Access

---
name: sf-cli-access
description: Authenticate to Salesforce orgs and execute SF CLI commands from Slack
triggers:
  - User asks to query, describe, deploy, test, or check anything in a Salesforce org
  - User references a specific org, object, flow, class, or Salesforce metadata
  - User asks "check the org" or "run tests" or "describe [object]"
  - User asks about deployment status
---

## When to Use

When your human asks you to interact with a Salesforce org — querying data, describing
metadata, running tests, checking deployments, or any other SF CLI operation.

## Prerequisites

JWT authentication must be configured. See docs/salesforce-cli-setup.md.
Environment variables must be set: SF_CLIENT_ID, SF_JWT_KEY_FILE, SF_USERNAME, SF_INSTANCE_URL.

## Steps

### 1. Determine the Target Org

- Check if the user specified an org (prod, sandbox, dev)
- If not, **ask.** Never assume which org.
- Check the SOUL for org aliases and access levels

### 2. Authenticate

```bash
sf org login jwt \
  --client-id $SF_CLIENT_ID \
  --jwt-key-file $SF_JWT_KEY_FILE \
  --username $SF_USERNAME \
  --instance-url $SF_INSTANCE_URL \
  --alias [org-alias]
```

If auth fails, check:
- Certificate expiration: `openssl x509 -enddate -noout -in $SF_JWT_KEY_FILE`
- Org status: is the org in maintenance?
- Report the error to the user — don't retry silently

### 3. Check Access Level Before Executing

**Read operations (always OK if auth succeeds):**
- `sf sobject describe` — describe objects/fields
- `sf sobject list` — list objects
- `sf data query` — SOQL queries (SELECT only)
- `sf apex get` — view Apex classes/triggers
- `sf flow list` / `sf flow get` — view flows
- `sf org display` — org info
- `sf project deploy report` — check deployment status
- `sf apex run test` — run tests (read-only, doesn't change data)
- `sf limits api display` — check API limits

**Write operations (CHECK SOUL — may require approval):**
- `sf data create record` — insert data
- `sf data update record` — update data
- `sf data delete record` — delete data
- `sf project deploy start` — deploy metadata
- `sf project deploy cancel` — cancel deployment
- `sf apex execute` — execute anonymous Apex

**Before any write operation:**
1. Check the SOUL's access level for this org
2. If the org is read-only or production: **stop and ask for explicit approval**
3. Describe exactly what you're about to do and wait for confirmation
4. Never batch write operations — one at a time with confirmation

### 4. Execute and Report

Run the command. Report results clearly:
- For queries: format the results as a readable table
- For describes: highlight the key fields, relationships, and record types
- For tests: summarize pass/fail, highlight failures with details
- For deploys: report status, component count, any errors

### 5. Handle Errors

Common errors and what to do:

| Error | Likely Cause | Action |
|-------|-------------|--------|
| `INVALID_SESSION_ID` | Token expired | Re-authenticate with JWT |
| `MALFORMED_QUERY` | Bad SOQL | Fix the query syntax, try again |
| `INVALID_FIELD` | Field doesn't exist | Describe the object first, check field names |
| `REQUEST_LIMIT_EXCEEDED` | API limit hit | Report to user, suggest waiting |
| `INSUFFICIENT_ACCESS` | Permission issue | Report — this is a Salesforce config issue |

## Common Patterns

**"Describe [object]" flow:**
```bash
sf sobject describe --sobject Account --target-org [alias]
```
Parse the output. Report: fields (name, type, required), record types, key relationships.

**"How many [records]?" flow:**
```bash
sf data query --query "SELECT COUNT() FROM [Object] WHERE [conditions]" --target-org [alias]
```

**"Run tests" flow:**
```bash
# Specific test class:
sf apex run test --class-names MyTestClass --target-org [alias] --result-format human --wait 10

# All tests:
sf apex run test --test-level RunAllTestsInOrg --target-org [alias] --result-format human --wait 10
```

**"Check deployment" flow:**
```bash
sf project deploy report --target-org [alias]
```

**"Show me [Apex class]" flow:**
```bash
# List classes matching a name
sf data query --query "SELECT Name, Body FROM ApexClass WHERE Name = '[ClassName]'" --target-org [alias]
```

## Pitfalls

- **Always confirm the org.** Running a query against prod when they meant sandbox is a
  bad day. Ask if there's any ambiguity.
- **SOQL has limits.** Default query limit is 2000 records. For large result sets, warn
  the user and suggest adding WHERE clauses or LIMIT.
- **API limits are real.** Check `sf limits api display` if you're doing many operations.
  Don't burn through the daily limit on automation.
- **Describe output is verbose.** Don't dump the raw JSON. Summarize the useful parts —
  field names, types, required vs optional, relationships, record types.
- **Deploy to production requires tests.** Don't forget `--test-level RunLocalTests` for
  prod deploys. Scout should remind the user.
- **Anonymous Apex is powerful and dangerous.** Treat `sf apex execute` like production
  DML — always require explicit approval, always confirm the org.
