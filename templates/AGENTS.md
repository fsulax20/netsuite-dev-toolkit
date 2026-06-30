# AGENTS.md
### SuiteCloud Project — Coding Agent Context Bridge

> Copy this file into the root of each new SuiteCloud project.
> Tells Codex Desktop where to find toolkit context and how to operate this project.

---

## TOOLKIT LOCATION

Open this repository's local clone as a Codex Project. Codex Projects point to local folders, not directly to GitHub repositories. Treat the folder as disposable: commit and push verified work regularly so the repository can be recloned without loss.

The toolkit may remain in its own local clone. Reference it at:

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
CLI Auth ID:     [accountID]-admin
GitHub Repo:     [owner/repository]
Project Path:    [local path to this SuiteCloud project]
Active Sprint:   [current focus]
```

---

## RULES FOR THIS SESSION

1. Read `netsuite-dev-toolkit/README.md` before writing any code
2. Check `netsuite-dev-toolkit/scripts/` for existing patterns before building new ones
3. Confirm TD account and MCP connector before any deployment
4. Validate and deploy with the SuiteCloud CLI from the Codex Desktop shell at the project root
5. After every deploy, verify script ID via SuiteQL
6. Commit and push each verified unit of work; never rely on the local clone as the durable copy
7. If a script built here is reusable, add it to `netsuite-dev-toolkit/scripts/`
8. Log new platform gotchas to `netsuite-dev-toolkit/docs/GOTCHAS.md`

## REPOSITORY BOUNDARY

Ask: **Would I copy this customization into a different TD account later?**

- If yes, it belongs in a standalone repository with its own deployment boundary.
- If no, keep it in the existing repository that owns the account- or customer-specific solution.

## HISTORICAL NOTE

Older projects may contain VS Code workspace files or instructions for Cline and SuiteCloud Developer Assistant. They are legacy artifacts, not active setup or deployment instructions.

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
