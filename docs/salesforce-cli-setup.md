# Connecting Scout to Your Salesforce Org

This guide walks through giving your AI coworker secure, headless access to Salesforce
orgs via the SF CLI. Once configured, you can query data, check metadata, run tests,
and manage deployments — all from Slack.

## Why JWT?

When you run `sf org login web`, it opens a browser. That works on your laptop but
breaks on a server with no display. JWT (JSON Web Token) bearer flow authenticates
without a browser — the same pattern every CI/CD pipeline uses.

You set it up once per org. After that, Scout can authenticate silently.

## Prerequisites

- Salesforce CLI installed on the machine running Scout
  ```bash
  npm install -g @salesforce/cli
  sf --version
  ```
- Admin access to the Salesforce org (or help from an admin)
- OpenSSL (pre-installed on macOS/Linux)

## Step 1: Generate a Certificate and Key

```bash
# Create a directory for creds (this should NEVER be committed to git)
mkdir -p ~/.sf/jwt
cd ~/.sf/jwt

# Generate private key
openssl genrsa -out server.key 2048

# Generate self-signed certificate (valid 1 year — set a calendar reminder)
openssl req -new -x509 -key server.key -out server.crt -days 365 \
  -subj "/CN=Scout SF Agent/O=Your Company"
```

You'll end up with:
- `server.key` — private key (stays on Scout's machine, never shared)
- `server.crt` — certificate (uploaded to Salesforce)

## Step 2: Create a Connected App in Salesforce

1. **Setup → App Manager → New Connected App**
2. Fill in:
   - **Connected App Name:** Scout Agent
   - **API Name:** Scout_Agent
   - **Contact Email:** your email
3. **Enable OAuth Settings:**
   - **Callback URL:** `https://login.salesforce.com/services/oauth2/callback`
     (not actually used for JWT, but required)
   - **Use digital signatures:** ✅ Check this, upload `server.crt`
   - **Selected OAuth Scopes:**
     - `api` (Access and manage your data)
     - `refresh_token, offline_access`
     - `web` (Access and manage your web-based data)
     - Add more as needed, but start minimal
4. **Save** → wait 2-10 minutes for propagation

### Configure the Connected App Policies

1. **Setup → App Manager → find Scout Agent → Manage**
2. **Permitted Users:** "Admin approved users are pre-authorized"
3. **Add your user** (or a Permission Set) to the Connected App's allowed users:
   - Setup → Permission Sets → create "Scout Agent Access"
   - Assign it to your user
   - Back to Connected App → Manage → Permission Sets → add "Scout Agent Access"

### Get the Consumer Key

1. **App Manager → Scout Agent → View**
2. Copy the **Consumer Key** (also called Client ID)

## Step 3: Test the JWT Flow

```bash
sf org login jwt \
  --client-id YOUR_CONSUMER_KEY \
  --jwt-key-file ~/.sf/jwt/server.key \
  --username your.username@company.com \
  --instance-url https://login.salesforce.com \
  --alias my-org

# For sandboxes, use:
# --instance-url https://test.salesforce.com
```

Verify it worked:
```bash
sf org list
sf org display --target-org my-org
```

## Step 4: Configure Scout's Environment

Store credentials as environment variables, not in any committed file:

```bash
# Add to Scout's profile .env file (never committed)
# ~/.hermes/profiles/scout/.env

SF_CLIENT_ID=your_consumer_key_here
SF_JWT_KEY_FILE=/home/youruser/.sf/jwt/server.key
SF_USERNAME=your.username@company.com
SF_INSTANCE_URL=https://login.salesforce.com
```

## Step 5: Add the Salesforce CLI Skill

Copy the `sf-cli-access.md` skill from this repo's `skills/examples/` directory.
This teaches Scout how to authenticate and which commands it can run.

## What Scout Can Do Now

From Slack, you can ask:

| Request | What Scout Runs |
|---------|----------------|
| "Describe the Case object" | `sf sobject describe --sobject Case` |
| "Run all tests in sandbox" | `sf apex run test --test-level RunAllTestsInOrg` |
| "How many open cases?" | `sf data query --query "SELECT COUNT() FROM Case WHERE IsClosed = false"` |
| "Check my last deployment" | `sf project deploy report` |
| "List all flows" | `sf flow list` |
| "Show me the OpportunityTrigger apex class" | `sf apex get --name OpportunityTrigger` |
| "Deploy to sandbox" | Scout asks for confirmation first (per SOUL rules) |

## Security Considerations

- **Private key** stays on Scout's machine. Never in git, never in Slack, never in skills.
- **Connected App scopes** control what Scout can access at the Salesforce level.
- **SOUL red lines** define what Scout must ask permission for (e.g., any DML, any deploy to prod).
- **Permission Set** on the Connected App limits which orgs/users Scout can impersonate.
- **Certificate expiration** — set a reminder. When the cert expires, Scout loses access silently.
- **Audit trail** — all API calls made via JWT show up in Salesforce event logs under the connected app user. You have full visibility.

## Multiple Orgs

Repeat steps 1-3 for each org. Use aliases to distinguish:

```bash
sf org login jwt --alias client-prod ...
sf org login jwt --alias client-sandbox ...
sf org login jwt --alias dev-org ...
```

In Scout's SOUL, define which orgs exist and the access level for each:

```markdown
## Salesforce Orgs
| Alias | Org | Access Level |
|-------|-----|-------------|
| client-prod | Production | Read-only. No DML, no deploys without approval. |
| client-sandbox | Full Sandbox | Read/write. Can deploy, can run tests. |
| dev-org | Dev Org | Full access. |
```

## Troubleshooting

**"invalid_grant" error:**
- Connected App hasn't propagated yet (wait 10 min)
- User isn't in the Connected App's permitted users
- Certificate doesn't match the key
- Wrong instance URL (login.salesforce.com vs test.salesforce.com)

**"INVALID_LOGIN" error:**
- Username is wrong
- User doesn't have API access (check profile)
- Org has IP restrictions that block Scout's machine

**Certificate expired:**
- Regenerate cert, re-upload to Connected App
- `openssl x509 -enddate -noout -in server.crt` to check expiration
