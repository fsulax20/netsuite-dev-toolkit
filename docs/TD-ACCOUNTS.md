# TD Account Index
### docs/TD-ACCOUNTS.md

> One entry per TD account. Update when accounts are provisioned, repurposed, or retired.
> TD accounts are the development environment — there is no sandbox.

---

## ACCOUNT CARD TEMPLATE

```
### [Account ID]
- **MCP Connector:** [connector name in Codex]
- **SuiteCloud CLI Auth ID:** [accountID]-admin
- **Type:** Dedicated | Shared STDDEMO
- **Primary Use:** [what this account is for]
- **SuiteCloud Project:** [GitHub repo and local clone folder]
- **Key Customizations:** [custom fields, scripts, records deployed]
- **Restrictions:** [any known limitations]
- **Status:** Active | Dormant | Retired
- **Notes:**
```

---

## ACCOUNTS

---

### TD3071658
- **MCP Connector:** dcillo_td3071658
- **SuiteCloud CLI Auth ID:** td3071658-admin
- **Type:** Dedicated
- **Primary Use:** Arista Networks CRM demo build
- **SuiteCloud Project:** `crmscripts`
- **Key Customizations:**
  - `custentity_llm_score` — AI lead score (Float) on Customer/Lead
  - Custom Sales Roles: Solution Engineer, Channel Manager
  - Sales Territories configured
  - Items 2803–2812 (noninventoryresaleitem, Arista product catalog)
  - Deployed scripts: lead_scoring_restlet, lead_score_display, quote_margin_userevent, quote_dealdesk_ue, provisioning_restlet
- **Restrictions:** None known — full dedicated account
- **Status:** Active
- **Notes:** OAuth 2.0 confirmed working. Legacy SDA setup was previously tested; it is not the active workflow.

---

### TD3092021
- **MCP Connector:** netsuite_stwy_manf-_26-1
- **SuiteCloud CLI Auth ID:** Not yet documented
- **Type:** Dedicated
- **Primary Use:** Lead ingestion queue build
- **SuiteCloud Project:** `lead-ingestion-queue`
- **Key Customizations:** Lead ingestion queue project
- **Restrictions:** None known
- **Status:** Active
- **Notes:** Primary build surface is Visual Studio Code with the Codex IDE extension and the integrated-terminal SuiteCloud CLI.

---

### TD3102894
- **MCP Connector:** chamilton_td3102894
- **SuiteCloud CLI Auth ID:** td3102894-admin
- **Type:** Dedicated
- **Primary Use:** Consumer Goods (new)
- **SuiteCloud Project:** `lead-ingestion-queue`
- **Key Customizations:** None documented
- **Restrictions:** Do not assume retail-specific saved searches exist. The saved-search inventory is dominated by WMS/Manufacturing-prefixed searches, including WMS Open Task, Mfg Mobile, Cycle Count, and Pick Task. The account was likely provisioned from the same bundle/template as TD3092021 (Stairway Manufacturing); verify the actual data model before building Lead Triage Console logic.
- **Status:** Active
- **Notes:** SuiteCloud CLI authentication was verified in the `final-assessment` training project on July 20, 2026. The NetSuite connector is configured through the ChatGPT desktop app; confirm the current account, role, and callable tools at the start of each task.

---

### TD3074265
- **MCP Connector:** dcillo_td3074265
- **SuiteCloud CLI Auth ID:** Not yet configured
- **Type:** Shared STDDEMO
- **Primary Use:** General NS demos, not custom dev
- **SuiteCloud Project:** N/A
- **Key Customizations:** None — shared account
- **Restrictions:** Entity/transaction custom field SDF deployment silently ignored. Client Script DOM injection blocked in NS Next UI. Avoid for any custom SuiteScript or SDF work.
- **Status:** Dormant for dev use
- **Notes:** Use only for out-of-box NS feature demos where no customization is needed.

---

## ACCOUNT NOTES

- New accounts get provisioned as TD (Trial Demo) accounts through Oracle internal process
- Always confirm account type (dedicated vs shared) before starting any SDF or custom field work
- Record the exact MCP connector name here when a connector is added
- Multiple connectors can be active simultaneously — always confirm which one is being used at session start
- A SuiteCloud project may target different TD accounts only when it is intentionally portable and its authentication remains local
- Codex Projects point to local folders, not GitHub; commit and push regularly so the local clone remains disposable
- The NetSuite MCP connector is accessed through the ChatGPT desktop app. Confirm the account, role, and callable tools before relying on it in a task.

*Last updated: July 2026*
