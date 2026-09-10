# 📧 AI Email Triage & Auto-Draft Agent

**Category:** Communication / Support Automation
**Tools:** n8n · OpenAI API (GPT-4o-mini) · Gmail API · Google Sheets · Slack

## Problem
Small teams lose hours every week manually reading, sorting, and replying to inbound emails — separating urgent issues from routine questions, sales inquiries, and spam.

## What this workflow does
1. **Watches a Gmail inbox** for new unread messages.
2. Sends the email content to an **LLM (GPT-4o-mini)**, which classifies it into `Sales`, `Support`, `Urgent`, or `Spam`, assigns a priority, and drafts a short suggested reply.
3. **Logs every processed email** (sender, subject, category, priority) to a Google Sheet for visibility and reporting.
4. If the category is **not Spam**, it automatically **creates a Gmail draft** with the AI-suggested reply — a human still reviews and hits send.
5. If the priority is **high (urgent)**, it posts an instant alert to a **Slack channel** so nothing time-sensitive gets missed.

## Why it matters
This is the kind of "first win" automation most businesses ask for: it doesn't remove the human from the loop (drafts still need approval), but it removes the slowest part — reading and triaging — while keeping a clear audit trail in the sheet.

## Workflow diagram
```
Gmail Trigger → Extract Email Data → Classify & Draft with AI → Parse AI Output
                                                                     ├── Log to Sheet
                                                                     ├── IF Is Spam → (false) → Create Gmail Draft
                                                                     └── IF Is Urgent → (true) → Notify Slack
```

## Setup instructions
1. Import `workflow.json` into your n8n instance (**Workflows → Import from File**).
2. Connect your own credentials for: **Gmail (OAuth2)**, **OpenAI API**, **Google Sheets (OAuth2)**, **Slack API**.
3. Replace the placeholder values in the node parameters:
   - `REPLACE_WITH_YOUR_SHEET_ID` → your Google Sheet ID
   - Slack channel name `inbox-alerts` → your own channel
4. Create a Google Sheet with columns: `From, Subject, Category, Priority, Processed At`.
5. Test with the manual "Execute Workflow" button before activating the trigger.

## Notes
This is a personal/demo project built to demonstrate the pattern end-to-end. It was tested with sample inbox data, not production email traffic. Field mappings (e.g. `$json.from.value[0].address`) may need small adjustments depending on your Gmail node version.
