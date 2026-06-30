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
| 2026 | Codex Project repository mapping | A Codex Project points to a local folder, not directly to a GitHub repository |
| 2026 | Codex local project durability | Treat the folder as a disposable clone; commit and push verified work regularly |
| 2026 | SuiteCloud CLI project detection | Run from the SuiteCloud project root containing `manifest.xml` |
| 2026 | Repository boundary | Create a standalone repo when the customization may be copied into another TD account; otherwise keep it in the owning repo |

## Historical Notes — VS Code, Cline, and SuiteCloud Developer Assistant

These behaviors apply only to legacy workspaces. VS Code, Cline, and SDA are not the active build or deployment workflow.

| Date | Legacy Behavior | Historical Reality |
|------|-----------------|--------------------|
| 2026 | VS Code terminal deployment | The earlier workflow used the VS Code integrated terminal because standalone terminal sessions were unreliable |
| 2026 | SuiteCloud Developer Assistant auth | VPN had to be off to avoid connection reset errors |
| 2026 | SDA API key | Regenerated on every service restart and had to be retrieved from the local service |
| 2026 | SDA port conflict | Port 8181 could conflict; legacy workspaces commonly used 8182 |
| 2026 | SDA settings | Auth ID and Enable had to be set in VS Code Workspace settings |
| 2026 | SDA + Codex | SDA worked through Cline only and was not compatible with Codex |

*Last updated: June 2026*
