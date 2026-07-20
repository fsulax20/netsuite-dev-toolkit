<!-- Copy this file into the root of each new SuiteCloud project repo. Fill in the four fields below. -->

# THIS PROJECT

| Field | Value |
|-------|-------|
| Customer | [customer name] |
| TD Account | [TD account ID] |
| MCP Connector | [connector name] |
| Auth ID | [SuiteCloud CLI auth ID] |

# TOOLKIT

Read `~/Projects/netsuite-dev-toolkit/README.md` for the working model, environment rules, and platform gotchas.

Work from this repository's root in Visual Studio Code with the Codex IDE extension. Run SuiteCloud CLI commands from the project root containing `suitecloud.config.js`, not from `src/`.

- `$netsuite-suitescript-records-reference` — Verify SuiteScript record types, field IDs, field types, and search support.
- `$netsuite-sdf-project-documentation` — Generate and maintain documentation for SuiteCloud projects.
- `$netsuite-owasp-secure-coding` — Apply OWASP security patterns to SuiteScript and JavaScript.
- `$netsuite-sdf-roles-and-permissions` — Validate SDF permissions and least-privilege role configurations.
- `$netsuite-ai-connector-instructions` — Apply the correct NetSuite connector tool order, output rules, and SuiteQL safeguards.
- If this project targets TD3102894, read `~/Projects/netsuite-dev-toolkit/docs/DEMO-DATASET-TD3102894.md` before creating test data, sample records, or demo scenarios.

# RULES

- Read the toolkit README before writing code.
- Confirm `manifest.xml` exists before running SuiteCloud CLI commands.
- Before using the NetSuite MCP connector, confirm the intended TD account, role, and callable tools for the current task.
- When targeting TD3102894, use its existing showcase items and customers instead of inventing demo data.
- Never hardcode account IDs or credentials.
- Commit and push after every meaningful change.
- Verify the script ID via SuiteQL after every deploy.
- Do not deploy without explicit approval.
