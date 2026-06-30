# TD Account Index
### docs/TD-ACCOUNTS.md

> One entry per TD account. Update when accounts are provisioned, repurposed, or retired.
> TD accounts are the development environment — there is no sandbox.

---

## ACCOUNT CARD TEMPLATE

```
### [Account ID]
- **MCP Connector:** [connector name in Claude]
- **Auth ID (VS Code):** [accountID]-admin
- **Type:** Dedicated | Shared STDDEMO
- **Primary Use:** [what this account is for]
- **SuiteCloud Project:** [repo/folder name, separate from this toolkit]
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
- **Auth ID (VS Code):** td3071658-admin
- **Type:** Dedicated
- **Primary Use:** Arista Networks CRM demo build
- **SuiteCloud Project:** `crmscripts` (local, not yet in GitHub)
- **Key Customizations:**
  - `custentity_llm_score` — AI lead score (Float) on Customer/Lead
  - Custom Sales Roles: Solution Engineer, Channel Manager
  - Sales Territories configured
  - Items 2803–2812 (noninventoryresaleitem, Arista product catalog)
  - Deployed scripts: lead_scoring_restlet, lead_score_display, quote_margin_userevent, quote_dealdesk_ue, provisioning_restlet
- **Restrictions:** None known — full dedicated account
- **Status:** Active
- **Notes:** OAuth 2.0 confirmed working. SDA tested and functional (VPN off required).

---

### TD3074265
- **MCP Connector:** dcillo_td3074265
- **Auth ID (VS Code):** Not yet configured
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
- MCP connector name is set when connecting in Claude — note it here when a new connector is added
- Multiple connectors can be active in Claude simultaneously — always confirm which one is being used at session start
- Each account gets its own SuiteCloud project — never share one project folder across multiple TD accounts

*Last updated: June 2026*
