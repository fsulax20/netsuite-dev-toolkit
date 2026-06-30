# AGENTS.md
### SuiteCloud Project — Coding Agent Context Bridge

> Copy this file into the root of each new SuiteCloud project.
> Tells Cline, Codex, or any coding agent where to find toolkit context.

---

## TOOLKIT LOCATION

This project should be opened in VS Code alongside the `netsuite-dev-toolkit` repo as a second workspace folder, or via the combined `.code-workspace` file.

```
~/[wherever you cloned it]/netsuite-dev-toolkit/
```

---

## KEY CONTEXT FILES

Read these before starting any task:

| File | Path | Purpose |
|------|------|---------|
| Agent Spec | `netsuite-dev-toolkit/README.md` | Core dev rules, patterns, gotchas |
| Gotchas Log | `netsuite-dev-toolkit/docs/GOTCHAS.md` | Platform behaviors discovered |
| TD Accounts | `netsuite-dev-toolkit/docs/TD-ACCOUNTS.md` | Active accounts and their state |
| Reusable Scripts | `netsuite-dev-toolkit/scripts/` | Existing patterns by script type |

---

## THIS PROJECT

```
Customer:        [customer name]
TD Account:      [TD account ID]
MCP Connector:   [connector name]
Auth ID:         [accountID]-admin
Project Path:    [local path to this SuiteCloud project]
Active Sprint:   [current focus]
```

---

## RULES FOR THIS SESSION

1. Read `netsuite-dev-toolkit/README.md` before writing any code
2. Check `netsuite-dev-toolkit/scripts/` for existing patterns before building new ones
3. Confirm TD account and MCP connector before any deployment
4. Deploy from VS Code integrated terminal only — never Mac Terminal
5. After every deploy, verify script ID via SuiteQL
6. If a script built here is reusable, add it to `netsuite-dev-toolkit/scripts/`
7. Log new platform gotchas to `netsuite-dev-toolkit/docs/GOTCHAS.md`

---

## SUITECLOUD PROJECT STRUCTURE

```
/[project-root]
  AGENTS.md                        ← this file
  /src
    /FileCabinet
      /SuiteScripts
        /[project-name]
          [script-name].js
    /Objects
      /[customfield_scriptid].xml
      /[customrecord_scriptid].xml
  /deploy.xml
  /manifest.xml
```

---

*Keep this file at the project root. Update the project section for each new engagement.*
