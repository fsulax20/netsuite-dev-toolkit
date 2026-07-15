# Demo Dataset Reference — TD3102894 (Consumer Goods)

Structured, durable reference facts about the demo dataset living in TD3102894. This file exists so Codex and Claude can reference real item/customer/location data when building custom solutions against this account, without needing a live MCP query every time.

Source of truth for the full narrative version: NetSuite custom record "Dataset Info Guide" (customrecord_pn_demo_script, internal ID 2206), which links to the underlying Word doc `Consumer_Goods_Demo_Dataset_Guide_2.docx` (File Cabinet ID 22490, folder 3818). Pull that record directly via MCP if you need the exhaustive location/vendor mapping tables — this file covers what's needed for day-to-day building.

## Account Lineage

This dataset was not built directly in TD3102894. Internal references found in the account's own metadata point to a layered build structure:

- **TD3074569** — named directly in the dataset's own description as the source "CPG Wholesale Distribution & Retail demo dataset" account. Likely the core/master build.
- **TD3097623** — referenced in at least two places (the "Bill Capture" demo flow description, and the scriptId of the Dataset Info Guide record itself). Likely an intermediate layer.
- **TD3102894** — the account we're actually connected to and building against. Likely a downstream vertical-specific copy (Consumer Goods).

Internal references to the older account numbers were not scrubbed during cloning, which is how this lineage was discovered. Treat TD3102894 as a derivative copy, not the canonical source, if data model questions ever come up that this file doesn't answer.

## Business Narrative

Wholesale distribution business running on NetSuite for ~3 years. Full P2P and O2C document chains. Growth-with-seasonality story arc underlies the demo scenarios.

## Subsidiary Coverage

US and Canada both carry multi-year transaction history, but **all seeded demo scenarios and use cases live in the US subsidiary**. Canada exists for intercompany/multi-subsidiary demos (e.g. "Intercompany Inventory Flow: Canada Buys from U.S.") — don't stage new single-subsidiary scenarios there.

## Item Naming Convention

Pattern: `TYPE/CLASS-MNEMONIC-DIGITS`

Examples: `ELEC-LAPTOP-01`, `APPL-FRIDGE-01`

Suffixes:
- `-LOT` — lot-tracked item
- `-SERNO` — serial-tracked item

## Stocking Strategy

Each of the 24 product classes is anchored to one stocking location. **Denver is the only bin-managed location** in the dataset — reserved specifically for WMS, Ship Central, Manufacturing Mobile, and Smart Count demos. This explains why saved-search inventory on this account skews heavily WMS/Manufacturing — it's intentional, not bundle noise.

## 24 Showcase Items (one per product class)

| Item ID |
|---|
| APPL-FRIDGE-01-SERNO |
| APPRL-POLO-01 |
| AUT-ANT-7462-SERNO |
| COMP-SERVER-01-SERNO |
| CONV-BVRG-01 |
| COSM-SERUM-01-LOT |
| ELEC-LAPTOP-01-SERNO |
| FNB-PNB-1612-LOT |
| FRN-SOF-9921 |
| GIFT-BLK-1003 |
| HHC-CLN-2441-LOT |
| HIM-SAW-4412-SERNO |
| HLTH-PROTEIN-01-LOT |
| JWL-ANL-2258-SERNO |
| MED-CRS-3521 |
| OFP-PNR-3847 |
| PCG-SKN-0842-LOT |
| PET-TRT-7765-LOT |
| PHOTO-CAMERA-01-SERNO |
| RENTAL-PROJECTOR-01-SERNO |
| SGO-CMP-5512-SERNO |
| TELECOM-ROUTER-01-SERNO |
| TYG-ELC-9901 |
| VIT-PROBIO-01-LOT |

## 18 Anchor / Showcase Customers

| Customer |
|---|
| Big Sky Auto Parts |
| BlueStem Apparel |
| ByteBox Computers |
| Eclipse Jewelers |
| FastLane Gas & Go |
| Frontier Pharmacy |
| FurEver Pets |
| Golden Bay Gift Gallery |
| Granite Electronics |
| Horizon Play Store |
| InkJet Office World |
| Kettle & Field Market |
| Lakeview Furniture |
| NailDown Hardware |
| Rain City Wellness Store |
| Spokane River Outdoor Gear |
| Storyline Media Store |
| Summit AV & Furniture Rentals |

## 29 Pre-Built Demo Flows

Documented in the "Demo Dashboards" saved search (customsearch146, custom record type customrecord_pn_demo_script). Spans Advanced Financials, CRM Campaigns, Fixed Assets, Intercompany, Advanced Procurement (5 sub-flows), Quality Management, Warranty/RMA, Bill Capture, Electronic Bank Payments, and more. Query customsearch146 directly via MCP (ns_runSavedSearch) for the current full list rather than duplicating it here, since it's likely to grow.

## When Building Custom Solutions Here

- Use showcase items/customers above for test data and demo scripts instead of querying NetSuite fresh each time.
- Don't assume this is a clean, purpose-built Consumer Goods account — it inherited a full Manufacturing/WMS/Wholesale Distribution feature set from its lineage. Check whether existing saved searches, custom records, or workflows already cover a need before building new ones.
- If a data model question comes up that this file doesn't answer, pull customrecord_pn_demo_script ID 2206 directly via MCP for the full guide, or ask an admin about the TD3074569 / TD3097623 relationship.
