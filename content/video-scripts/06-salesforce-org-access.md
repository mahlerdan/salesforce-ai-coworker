# Video 6: "I Gave My AI Coworker Access to My Salesforce Org"

**Format:** Tutorial + demo. 10-12 minutes.
**Goal:** Show the JWT setup and demonstrate Scout querying/interacting with a live org from Slack.

---

## Opening (30 seconds)

> "Up until now, Scout has been helping me with documents, notes, and research. But
> Salesforce professionals don't just work with documents — we work in orgs.
>
> So I gave Scout access to my Salesforce org. From Slack.
>
> Let me show you what that looks like, and then I'll walk you through the setup."

---

## Demo First (2 minutes)

*Show the payoff before the how-to.*

*[Slack DM with Scout]*

> "Scout, describe the Case object in my sandbox."

*[Scout authenticates, runs describe, returns a clean summary — key fields, record types,
relationships]*

> "How many open cases were created this week?"

*[Scout runs a SOQL query, returns the count]*

> "Run the CaseManagement test class."

*[Scout runs tests, returns pass/fail summary]*

> "That's three Salesforce operations from a Slack message. No browser, no switching
> windows, no context switching. Let me show you how to set this up."

---

## Section 1: Why JWT (60 seconds)

> "Normally when you log into Salesforce from the CLI, it opens a browser window.
> That works on your laptop, but Scout might be running on a server with no display.
>
> JWT flow solves this. It's the same pattern every CI/CD pipeline uses — certificates
> instead of a browser. You set it up once per org and it just works.
>
> Not going to lie — this is the most technical setup in the series. But it's a
> one-time thing, and I'll walk through every step."

---

## Section 2: Generate Certificates (2 minutes)

*[Terminal screen recording]*

```bash
mkdir -p ~/.sf/jwt && cd ~/.sf/jwt
openssl genrsa -out server.key 2048
openssl req -new -x509 -key server.key -out server.crt -days 365
```

> "Two files. The key stays on Scout's machine — never share it. The certificate
> goes into Salesforce."

---

## Section 3: Connected App in Salesforce (3 minutes)

*[Screen recording of Salesforce Setup]*

> "We need a Connected App — this is how Salesforce knows who Scout is and what
> it's allowed to do."

**Walk through each step:**
1. Setup → App Manager → New Connected App
2. Name it, enable OAuth, upload the certificate
3. Select minimal scopes — only what Scout needs
4. Configure permitted users
5. Copy the Consumer Key

> "That Consumer Key is like Scout's badge. It identifies the app.
> Combined with the private key and your username, Scout can log in."

---

## Section 4: Test It (60 seconds)

```bash
sf org login jwt \
  --client-id YOUR_KEY \
  --jwt-key-file ~/.sf/jwt/server.key \
  --username you@company.com \
  --instance-url https://test.salesforce.com \
  --alias my-sandbox

sf org display --target-org my-sandbox
```

> "If you see your org info, you're in. Now let's tell Scout about it."

---

## Section 5: Configure Scout (60 seconds)

> "Add the credentials to Scout's environment — not in any file that gets committed."

*[Show adding env vars to the profile .env]*

> "And add the Salesforce CLI skill from the repo. This teaches Scout which commands
> it can run, how to authenticate, and importantly — what it needs to ask
> permission for."

---

## Section 6: The SOUL Update (60 seconds)

> "One more thing. I add my orgs to Scout's SOUL with access levels."

```markdown
## Salesforce Orgs
| Alias | Org | Access Level |
|-------|-----|-------------|
| my-prod | Production | Read-only. No DML without approval. |
| my-sandbox | Full Sandbox | Read/write. Can deploy and test. |
```

> "Scout checks this before every operation. It'll run a query in sandbox without
> asking. But if I say 'run this in prod,' Scout stops and confirms."

---

## Section 7: Full Demo (2 minutes)

*[Back to Slack — live demo with real org]*

Show a sequence:
1. "Describe the Opportunity object" → clean field summary
2. "How many Opportunities closed this quarter?" → SOQL, formatted result
3. "Run the OpportunityTests class" → test results
4. "Deploy the latest changes to sandbox" → Scout asks for confirmation → deploy

> "Four operations. All from Slack. No switching to a browser, no opening VS Code,
> no terminal. Just ask."

---

## Close (30 seconds)

> "This is where it starts to feel like a real coworker. Scout doesn't just help me
> think about Salesforce — it can actually interact with my orgs.
>
> The JWT setup guide and the Salesforce CLI skill are both in the repo. Link in
> the description.
>
> Next up: I'm going to show you how to build a custom LWC with Scout — pair
> programming with an AI coworker."

---

## Production Notes

- **Use a sandbox or dev org.** Never demo with production data on camera.
- **Pre-verify the JWT flow works** before recording. Nothing kills a tutorial
  faster than a config error on camera.
- **Sanitize SOQL results.** If query results show real names, emails, or company
  data, use a dev org with fake data.
- **The Connected App setup in Salesforce has multiple screens.** Zoom in, go slow.
  This is where viewers will pause and follow along.
- **The "Scout asks for confirmation before prod" moment is important.** It shows
  responsible AI use. Don't skip it — it's a selling point, not a limitation.
- **If the JWT auth fails on camera,** that's actually good content. Show the
  troubleshooting. "See, it said invalid_grant — that usually means the
  Connected App hasn't propagated yet. Give it 10 minutes."
