# New TD Account Setup
### docs/SETUP.md

> Reusable step-by-step procedure for onboarding a new TD account and starting a new project.
> Run through this every time a new TD account is provisioned or a new engagement begins.

---

## PREREQUISITES

- TD account provisioned and accessible at `https://[accountID].app.netsuite.com`
- Administrator login credentials available
- Codex Desktop installed with shell access
- Git and the SuiteCloud CLI installed and available in the Codex shell
- A GitHub repository selected or created using the decision criteria below

---

## STEP 0 — CHOOSE THE REPOSITORY

Ask: **Would I copy this customization into a different TD account later?**

- **Yes:** create a standalone repository. This is the right boundary for a portable SuiteApp, integration, or proof of concept that may be deployed to another TD account.
- **No:** add the work to the existing repository that owns the account- or customer-specific solution.

Avoid a standalone repo for a one-off script that cannot operate independently of its current project.

---

## STEP 1 — CLONE LOCALLY AND OPEN IN CODEX

1. Clone the selected GitHub repository to a local folder.
2. Open that folder as a Codex Project.
3. Confirm the current branch and remote before editing.
4. Copy `templates/AGENTS.md` into the repository root and fill in the project details.

A Codex Project is linked to the local folder, not directly to GitHub. Treat the folder as a disposable clone: GitHub is the durable copy, so commit and push every verified unit of work. Never leave important work only in the local folder.

---

## STEP 2 — CREATE OR CONFIRM THE SUITECLOUD PROJECT

From the Codex Desktop shell:

1. Confirm `manifest.xml` and `deploy.xml` exist at the SuiteCloud project root.
2. If this is a new project, create it with the SuiteCloud CLI and use the standard SDF structure.
3. Confirm the CLI can identify the project before adding scripts or objects.

Keep the SuiteCloud project at the repository root unless the repository intentionally contains multiple independently deployable packages.

---

## STEP 3 — CONFIGURE SUITECLOUD CLI AUTHENTICATION

1. Start SuiteCloud CLI account setup from the Codex shell.
2. Name the auth ID `[accountID]-admin` (for example, `td3071658-admin`).
3. Complete the browser OAuth flow and select the **Administrator** role on the correct TD account.
4. Confirm the CLI recognizes the auth ID.
5. Keep authentication data local; do not commit it.

---

## STEP 4 — CONNECT AND VERIFY THE MCP CONNECTOR

1. Confirm the NetSuite MCP connector for the TD account is available in Codex.
2. Record its exact name in `docs/TD-ACCOUNTS.md` and the project's `AGENTS.md`.
3. Test it with a small read-only SuiteQL query.
4. Confirm the account returned by the query matches the intended TD account before any write or deployment.

---

## STEP 5 — BUILD, DEPLOY, AND VERIFY

1. Build in Codex Desktop and use its shell for SuiteCloud CLI validation and deployment.
2. Deploy only from the SuiteCloud project root.
3. Verify the actual script and deployment IDs with SuiteQL; never trust the manifest alone.
4. Verify event types, file paths, logs, and writeback behavior in the target TD account.
5. Commit and push the verified change immediately.

---

## STEP 6 — UPDATE TOOLKIT DOCS

Update `docs/TD-ACCOUNTS.md` with the account ID, MCP connector, SuiteCloud CLI auth ID, repository/folder, purpose, and status.

---

## HISTORICAL NOTE — VS CODE, CLINE, AND SDA

Older projects used the VS Code SuiteCloud extension, Cline, and SuiteCloud Developer Assistant. Those tools are no longer the primary workflow and are not required for new projects. Legacy SDA environments may still require VPN disconnection, workspace-scoped settings, a local port, and a regenerated API key; preserve those details only when maintaining an existing legacy workspace.

## GOTCHAS

| Issue | Fix |
|-------|-----|
| Wrong role in OAuth flow | Click "Choose another role" — select Administrator |
| Codex Project appears disconnected from GitHub | Expected: it points to a local folder. Check the Git remote and push explicitly. |
| Work exists only in the local folder | Commit and push it; the local clone is disposable. |
| SuiteCloud CLI cannot find the project | Run it from the folder containing `manifest.xml`. |
| Shared STDDEMO account | SDF custom field deploy silently ignored — use dedicated TD accounts for dev work |

See `docs/GOTCHAS.md` for the full platform behavior log.

*Last updated: June 2026*
