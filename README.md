# NetSuite Dev Toolkit
### Christopher Hamilton — Oracle NetSuite Solutions Consultant

> Codex: read this file before starting any task. Oracle SuiteCloud Agent Skills handle NS domain knowledge — this file covers how we work, our environment, and what Oracle doesn't know about us.

---

## WHO WE ARE

**Christopher Hamilton** is an Oracle NetSuite Solutions Consultant building demo and proof-of-concept NetSuite environments for enterprise sales. He evaluates NetSuite against competing CRM/ERP platforms for prospects and builds custom SuiteScript/SDF solutions to showcase specific capabilities.

**Working style:** Results-oriented and pragmatic. Direct recommendations only — no option menus. He makes the final call, you execute. Flag overengineering immediately and propose a simpler path. Blockers get raised immediately, not worked around silently.

**Claude** handles strategy, architecture, demo narrative, decks, RFPs, and new tool evaluation. **Codex** handles the actual build — SuiteScript, SDF, GitHub, SuiteCloud CLI.

---

## HOW WE WORK WITH CODEX

### Toolchain
- **Codex Desktop** — primary build surface, shell access, SuiteCloud CLI at `/usr/local/bin/suitecloud` v3.1.3
- **GitHub** — source of truth for all repos. Local folders are disposable clones. Commit and push after every meaningful change.
- **NetSuite MCP connector** — configured in Codex but not always callable per-thread. Confirm it's active before relying on it. Use Claude.ai for MCP-heavy work.
- **Oracle SuiteCloud Agent Skills** — the installed local skill library is `~/.agents/skills/`. Current verified NetSuite skills: `$netsuite-suitescript-records-reference`, `$netsuite-sdf-project-documentation`, `$netsuite-owasp-secure-coding`, `$netsuite-sdf-roles-and-permissions`, and `$netsuite-ai-connector-instructions`. The upstream catalogue is `oracle/netsuite-suitecloud-sdk`; install additional skills only for a concrete need and record the change here.

### MCP Custom Tools & Apps

MCP is the authenticated connection layer; **custom tools** are separately deployed SuiteScript 2.1 capabilities that an AI client can invoke through that connection. They are not edits to the managed MCP Standard Tools SuiteApp.

- **Current TD state:** `Customization > Scripting > Custom Tools` contains only the managed MCP Standard Tools toolsets: Record, Reporting, Search, SuiteQL, and Prompt Library App.
- **Custom-tool structure:** an SDF project provides a custom tool script, a JSON tool schema, and a `toolset` XML definition. Set `exposetoaiconnector` to expose the tool; the toolset's permissions control visibility, while the connected NetSuite role controls the underlying data and actions.
- **MCP Apps:** custom tools can bundle a self-contained HTML interface that compatible AI clients render in chat. Use this only when a structured form, selector, or review step materially improves a workflow.
- **Starting point:** Oracle's [MCP-Sample-Tools](https://github.com/oracle-samples/netsuite-suitecloud-samples/tree/main/MCP-Sample-Tools) includes 2026.1-compatible sample toolsets and a minimal MCP App. Clone it into a standalone repo when a real use case is approved; do not deploy samples to a TD account merely for exploration.
- **Connection endpoint:** a deployed SuiteApp's custom tools are available at `https://<accountid>.suitetalk.api.netsuite.com/services/mcp/v1/suiteapp/<applicationid>`. The AI client must use OAuth 2.0 Authorization Code with PKCE, not a static bearer token.
- **First production pattern:** create one narrow tool with explicit inputs, role-scoped permissions, input validation, clear logging, and a confirmation/review step before any write action (for example, creating a marketing campaign).

### Project Setup
- Delivery projects are GitHub repos cloned into `~/Projects/[repo-name]`.
- Each delivery project has an `AGENTS.md` at its Git root (copy from `templates/AGENTS.md`).
- Training exercises may stay local and disposable; do not create a GitHub repo unless the exercise will become reusable demo or product work.
- For SuiteCloud CLI for Node.js projects, open Codex and run SuiteCloud CLI from the project root containing `suitecloud.config.js`. The SDF source folder is normally `src/`, which contains `manifest.xml`, `deploy.xml`, and `project.json`.
- Point a Codex Project at the project root, not the nested `src/` folder.
- This toolkit repo lives at `~/Projects/netsuite-dev-toolkit` — reference it from any project

### New Repo vs Existing
**Standalone repo** when: reusable across TD accounts, substantial enough for its own lifecycle, shareable independently.
**Add to toolkit `/scripts`** when: small, one-off, or tightly coupled to one engagement.
Quick test: would I copy this into a different TD account later? Yes → own repo. No → toolkit scripts.

### Session Start (confirm once)
1. Working directory contains `manifest.xml`?
2. MCP connector callable in this thread?
3. Check `/scripts` for existing patterns before building new

### Completion Checklist
- [ ] Script deploys without SDF errors
- [ ] Script ID verified via SuiteQL (not assumed from manifest)
- [ ] Script fires on correct event type(s)
- [ ] File path in NS record matches deployed path
- [ ] Error handling in place, logs at entry points and error paths
- [ ] Behavior verified in the actual TD account
- [ ] Committed and pushed to GitHub

### Commit Conventions
feat: add lead ingestion restlet
fix: resolve script ID mangling on deploy
chore: verify deployed script IDs via suiteql
docs: update TD account index

### Documentation Maintenance
- **Personal Codex behavior:** `~/.codex/AGENTS.md`
- **Operating model and toolchain facts:** this `README.md`
- **Project-specific rules:** the project's root `AGENTS.md`
- **TD account and demo-data facts:** `docs/TD-ACCOUNTS.md` and the relevant dataset document
- **Available NetSuite skills:** `~/.agents/skills/`; upstream source: `oracle/netsuite-suitecloud-sdk`

Run a read-only setup and documentation audit when a training lesson conflicts with verified behavior, before a major demo or deployment, after changing a tool or skill, and at least quarterly. Update this toolkit only after verifying the change from the installed tool, local configuration, or an authoritative source.

---

## ENVIRONMENT

Christopher works across multiple NetSuite TD (Trial/Demo) accounts. No sandbox exists — TD accounts are the dev environment. See `docs/TD-ACCOUNTS.md` for the current account index.

`docs/DEMO-DATASET-TD3102894.md` — structured reference for the TD3102894 demo dataset (item/customer/lineage facts).

| Tier | Notes |
|------|-------|
| **Dedicated TD** | Full SDF and custom field support |
| **Shared STDDEMO** | SDF deploys silently ignored, DOM injection blocked — avoid for dev |

**Never hardcode account IDs, internal IDs, or credentials in scripts.** API keys go in Script Deployment parameters. Shared secrets go in deployment parameters.

---

## HARD-WON GOTCHAS

Things Oracle's skills don't know about — discovered through actual builds:

| Behavior | Reality |
|----------|---------|
| `recordType: "lead"` via MCP | Fails silently — use `customer` + `entitystatus: {id: "6"}` |
| SDF script ID after deploy | Often doubled/mangled — always verify via SuiteQL |
| Client Script on View mode | Won't fire unless Event Type includes View — check deployment record |
| `N/https` in Client Script | Silent failure — use XHR/fetch |
| `form.submit()` in Suitelet popup | Silent failure — use XHR |
| Employee records via API/SDF | Hard 403 — NS UI or CSV import only |
| Shared STDDEMO SDF deploy | Custom field deployment silently ignored |
| `FREEFORMTEXT` on custom record field | Invalid — use `TEXT` |
| `DECIMAL` on entity custom field | Invalid — use `FLOAT` |
| Quote `selectrecordtype` in SDF XML | Use `-6` not `"estimate"` |
| Codex MCP connector | May be configured but not callable per-thread — confirm each session |
| SuiteCloud commands not activating | Must be run from folder containing `manifest.xml` at root |

**SuiteQL diagnostic for deployed script IDs:**
```sql
SELECT s.scriptid, s.name, sd.scriptid as deployment_id, sd.status
FROM script s
JOIN scriptdeployment sd ON sd.script = s.id
WHERE s.name LIKE '%your_script_name%'
```

---

## TECHNOLOGY RADAR

New tools and features Christopher has discovered. Codex: when you see a task type matching an "Adopt" or "Evaluate" item, proactively suggest it.

### Adopt — actively using
- Oracle SuiteCloud Agent Skills (installed globally via `npx skills`)
- NetSuite MCP connector (Claude.ai and Codex)
- SuiteCloud CLI v3.1.3 via Codex shell

### Evaluate — discovered, worth trying
- `N/LLM` — NetSuite's native LLM module for server-side AI calls without external RESTlet. Evaluate for lead scoring, deal analysis, any task currently using OpenAI via external API.

### Watch — on the horizon
- NetSuite Apps within Claude (MCP-based NS apps surfaced directly in Claude.ai)

> To add something new: share it with Claude first. Claude evaluates fit and updates this section. Codex reads it next session and applies it where relevant.

---

*Source of truth for how we work. Oracle SuiteCloud Agent Skills cover NS domain knowledge. This file covers everything else.*
