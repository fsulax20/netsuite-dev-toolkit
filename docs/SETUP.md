# New TD Account Setup
### docs/SETUP.md

> Reusable step-by-step procedure for onboarding a new TD account and starting a new project.
> Run through this every time a new TD account is provisioned or a new engagement begins.

---

## PREREQUISITES

- TD account provisioned and accessible at `https://[accountID].app.netsuite.com`
- Administrator login credentials available
- VPN **disconnected** before starting any SDA work
- VS Code open with SuiteCloud extension installed

---

## STEP 0 — VS CODE: CREATE SUITECLOUD PROJECT

Each engagement gets its own SuiteCloud project, separate from this toolkit repo.

1. `Cmd+Shift+P` → `SuiteCloud: Create Project`
2. Name it `[customer]scripts`
3. Save it outside this toolkit repo, e.g. `~/[Customer Name]/[customer]scripts`
4. Open this toolkit repo as a second folder in the same VS Code workspace (`File → Add Folder to Workspace`)
5. Save the combined workspace as `[customer].code-workspace` for one-click reopening later

---

## STEP 1 — VS CODE: ADD AUTH ID

1. `Cmd+Shift+P` → `SuiteCloud: Manage Accounts`
2. Select **"New authentication ID"**
3. Name it `[accountID]-admin` (e.g. `td3071658-admin`)
4. Complete the browser OAuth flow — select **Administrator** role on the correct account
5. Confirm the auth ID appears in the accounts list

---

## STEP 2 — VS CODE: CONFIGURE SUITECLOUD DEVELOPER ASSISTANT (if using Cline)

1. `Cmd+,` → search `suitecloud.developerAssistant`
2. Select the **Workspace** tab (not User — Workspace overrides User)
3. Set **Auth ID** to `[accountID]-admin`
4. Set **Local Port** to `8182` (or next available if in use)
5. Check **Enable**
6. Check Output panel → SuiteCloud filter — confirm service starts

---

## STEP 3 — VS CODE: GET SDA API KEY (if using Cline)

Run in VS Code terminal:
```
curl http://127.0.0.1:8182/api/internal/devassist/apikey
```

A popup appears with the generated key. Click **Copy API Key**, then in Cline settings:
- **API Provider** → `OpenAI Compatible`
- **Base URL** → `http://127.0.0.1:8182/api/internal/devassist`
- **OpenAI Compatible API Key** → paste the copied key
- **Model ID** → `devassist`

Test with: `Create a simple SuiteScript 2.1 RESTlet that returns hello world`

---

## STEP 4 — CODEX: PERSONALIZATION (one-time per machine, not per account)

This only needs to be done once on this machine — it persists across all future projects.

1. Codex Settings → **Personalization** → **Custom instructions**
2. Paste the contents of this repo's `README.md`, from "WHO YOU ARE" to the end
3. Click **Save**

If already done, skip this step.

---

## STEP 5 — CLAUDE.AI: CONNECT MCP CONNECTOR

1. Claude.ai → Settings → Connectors
2. Find or add the NetSuite MCP connector for the new TD account
3. Note the connector name (e.g. `dcillo_td3071658`)
4. Test with a simple SuiteQL query via `ns_runCustomSuiteQL`

---

## STEP 6 — UPDATE TOOLKIT DOCS

Update `docs/TD-ACCOUNTS.md` with the new account entry — MCP connector, auth ID, SuiteCloud project path, status.

---

## STEP 7 — COPY AGENTS.MD

Copy `templates/AGENTS.md` into the new SuiteCloud project root (`[customer]scripts/AGENTS.md`) and fill in:
- Customer name
- TD account ID
- MCP connector name
- SuiteCloud project path

---

## GOTCHAS

| Issue | Fix |
|-------|-----|
| VPN on during SDA setup | Disconnect VPN — connection reset errors will block OAuth |
| Wrong role in OAuth flow | Click "Choose another role" — select Administrator |
| Port 8181 conflict | Change SDA port to 8182 or next available in Workspace settings |
| API key invalid after restart | Re-run curl command to get new key, paste into Cline |
| SDA settings not sticking | Must be set in **Workspace** tab, not User tab |
| SuiteCloud commands not appearing | Must be in a SuiteCloud project folder with manifest.xml — not this toolkit repo |
| Adding toolkit repo breaks SDA | Save as a combined `.code-workspace` file rather than ad-hoc "Add Folder to Workspace" |
| Shared STDDEMO account | SDF custom field deploy silently ignored — use dedicated TD accounts for dev work |

See `docs/GOTCHAS.md` for the full platform behavior log.

*Last updated: June 2026*
