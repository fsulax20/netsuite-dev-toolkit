# Platform Gotchas Log
### docs/GOTCHAS.md

> Continuously updated log of NetSuite/SuiteCloud platform behaviors discovered during development.
> Add a row every time something silently fails or behaves unexpectedly.

| Date | Behavior | Reality |
|------|----------|---------|
| 2026 | `recordType: "lead"` via MCP | Fails silently — use `customer` + `entitystatus: {id: "6"}` |
| 2026 | SDF script ID after deploy | Often doubled/mangled — always verify via SuiteQL |
| 2026 | Client Script on View mode | Won't fire unless Event Type includes View |
| 2026 | `N/https` in Client Script | Silent failure — use XHR/fetch |
| 2026 | `form.submit()` in Suitelet popup | Silent failure — use XHR |
| 2026 | Employee records via API/SDF | Hard 403 — NS UI or CSV import only |
| 2026 | Shared STDDEMO SDF deploy | Custom field deployment silently ignored |
| 2026 | `FREEFORMTEXT` on custom record field | Invalid — use `TEXT` |
| 2026 | `DECIMAL` on entity custom field | Invalid — use `FLOAT` |
| 2026 | Quote `selectrecordtype` in SDF XML | Use `-6` not `"estimate"` |
| 2026 | Mac Terminal SDF deploy | CLI hangs — always use VS Code integrated terminal |
| 2026 | SuiteCloud Developer Assistant auth | VPN must be OFF — connection reset errors with VPN on |
| 2026 | SDA API key | Regenerates on every service restart — retrieve with: `curl http://127.0.0.1:[port]/api/internal/devassist/apikey` |
| 2026 | SDA port conflict | Default port 8181 conflicts if another instance running — use 8182 or next available |
| 2026 | SDA workspace settings | Auth ID and Enable must be set in Workspace tab, not User tab — Workspace overrides User |
| 2026 | SDA OAuth flow | First-time setup triggers browser OAuth — choose Administrator role on correct TD account, not other available roles |
| 2026 | SDA + Codex | Not compatible — SDA is hardcoded to work through Cline only |
| 2026 | Codex NS context | Has no native NS knowledge — must be given via Personalization custom instructions (paste README.md content) and AGENTS.md in project root |
| 2026 | Codex Personalization scope | Machine-wide, not per-project — set once, persists across all projects |
| 2026 | SuiteCloud commands not appearing in VS Code | Must be in a SuiteCloud project folder with manifest.xml at root — won't activate elsewhere |

*Last updated: June 2026*
