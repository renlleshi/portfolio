# 🎯 Lead Enrichment & Scoring Pipeline

**Category:** Sales / RevOps Automation
**Tools:** n8n · OpenAI API (GPT-4o-mini) · HTTP Request · Google Sheets · Slack

## Problem
Sales teams often receive raw, unqualified leads (just a name, email, and website) and waste time manually researching each company before deciding whether it's worth pursuing — this is exactly the kind of "waterfall enrichment" work tools like Clay are built around.

## What this workflow does
1. **Watches a Google Sheet** for new lead rows (name, company, email, website).
2. **Fetches the lead's company website** automatically via HTTP request.
3. Strips the raw HTML down to clean text and sends it to an **LLM**, which generates:
   - a short company summary
   - an estimated industry and company size
   - a **qualification score (0–100)** based on fit criteria
4. **Writes the enrichment data back into the same row** of the sheet — no manual copy-pasting.
5. If the score is **70 or higher**, it automatically **notifies the sales channel on Slack** so hot leads get followed up on immediately.

## Why it matters
This mirrors real enrichment/waterfall workflows used in sales tooling (e.g. Clay + HubSpot), showing the ability to go from "a spreadsheet of names" to "a scored, research-backed pipeline" without manual work.

## Workflow diagram
```
New Lead (Sheets Trigger) → Fetch Company Website → Extract Text Content
   → Enrich & Score with AI → Parse Enrichment Output → Update Lead in Sheet
   → IF Score >= 70 → (true) → Notify Sales on Slack
```

## Setup instructions
1. Import `workflow.json` into n8n.
2. Connect credentials for: **Google Sheets (OAuth2)**, **OpenAI API**, **Slack API**.
3. Create a Google Sheet named `Leads` with columns: `LeadName, Company, Email, CompanyWebsite, Summary, Industry, Estimated Size, Score`.
4. Replace `REPLACE_WITH_YOUR_SHEET_ID` in both Google Sheets nodes.
5. Replace the Slack channel name `sales-hot-leads` with your own.

## Notes
Built and tested with a small sample list of real company websites (public, non-sensitive) to validate the enrichment logic. The scoring criteria in the AI prompt is written for a company selling AI automation services — swap it for whatever ICP (ideal customer profile) fits the target business.
