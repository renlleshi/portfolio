# 🛡️ Security Alert Triage & Summarization

**Category:** Security / IT Operations Automation
**Tools:** n8n · OpenAI API (GPT-4o-mini) · Webhook · Google Sheets · Slack

## Problem
Small security/IT teams get flooded with alerts (failed logins, suspicious IPs, phishing reports) from various monitoring tools. Reading and triaging every one manually is slow, and low-value noise often buries the alerts that actually matter.

## What this workflow does
1. **Receives alerts via webhook** — this can come from a SIEM tool, a monitoring script, or a simple form used to report suspicious emails/activity.
2. **Normalizes the alert** into a consistent structure (source, type, user, IP, description, timestamp), since different tools send data in different shapes.
3. Sends the normalized alert to an **LLM**, which classifies severity (`low/medium/high/critical`), writes a **plain-language summary**, and suggests a **recommended next action** — without inventing facts not present in the alert.
4. **Logs every alert** to a Google Sheet for a full audit trail.
5. If severity is **high or critical**, it **immediately posts to a dedicated Slack security channel** so the on-call person doesn't have to read a raw log to understand what's happening.
6. Sends an acknowledgment response back to the system that triggered the webhook.

## Why it matters
This is the project that reflects my Information Security background directly: it's not just "connect tool A to tool B" — it's about reducing alert fatigue while keeping a clear, honest audit trail and not letting the AI overstate what it actually knows about an incident.

## Workflow diagram
```
Security Alert Webhook → Normalize Alert Payload → Classify Severity & Summarize → Parse AI Output
                                                                                       ├── Log to Audit Sheet
                                                                                       ├── Respond to Webhook
                                                                                       └── IF Severity High/Critical → (true) → Alert Security Channel
```

## Setup instructions
1. Import `workflow.json` into n8n.
2. Connect credentials for: **OpenAI API**, **Google Sheets (OAuth2)**, **Slack API**.
3. Activate the workflow to get a live webhook URL (Production URL shown on the Webhook node).
4. Create a Google Sheet named `AlertLog` with columns: `Timestamp, Source, Alert Type, User, IP, Severity, AI Summary, Recommended Action`.
5. Test by sending a sample POST request, e.g.:
   ```bash
   curl -X POST https://YOUR_N8N_URL/webhook/security-alert-intake \
     -H "Content-Type: application/json" \
     -d '{"source":"AWS GuardDuty","alert_type":"Suspicious login","user":"jdoe","ip":"185.23.14.9","description":"Login from unrecognized country after 3 failed attempts"}'
   ```

## Notes
Tested with simulated alert payloads (not connected to a real production SIEM). The AI is explicitly instructed not to invent details beyond what's in the alert — this matters in security contexts where a hallucinated "root cause" could mislead an analyst.
