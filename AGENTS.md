# NetSuite Dev Toolkit

This repository is the shared operating guide for NetSuite demo and proof-of-concept work. It is not a deployable SuiteCloud project.

## Documentation rules

- Keep guidance concise, evidence-based, and specific to the current toolchain.
- Treat `README.md` as the operating-model source of truth; keep templates and supporting documents aligned with it.
- When a training lesson conflicts with verified product behavior, update the toolkit with the verified behavior and record the verification date.
- Never add credentials, account secrets, access tokens, or raw PII to toolkit documentation.
- Retain account IDs, script IDs, deployment IDs, and internal URLs when they are needed for internal operations.

## Verification and maintenance

- Before documenting SuiteCloud CLI behavior, verify it against the installed CLI or Oracle documentation.
- Before documenting a skill as available, verify it is installed in `~/.agents/skills/`.
- Review the skill inventory and tooling guidance quarterly, before major demos, and whenever a training or tool update reveals a conflict.
- Commit documentation changes as focused Conventional Commits and push after verification.
