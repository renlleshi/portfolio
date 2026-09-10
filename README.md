# AI Automation Portfolio — n8n + LLM Workflows

Hi, I'm **[YOUR FULL NAME]** — an AI Automation Specialist with a background in Information Security (BSc) and a Master's in Computer Science & Artificial Intelligence (expected Nov 2026). I build workflows that connect business tools with LLMs (OpenAI / Anthropic Claude) to remove manual, repetitive work.

📧 [your.email@gmail.com] · 🔗 [LinkedIn URL] · 📍 Open to remote work

This repository documents three end-to-end automation workflows I designed and built with **n8n**, each targeting a different real-world business problem. Every workflow is exported as importable JSON, with a dedicated README explaining the problem, the logic, and how to set it up.

## 📂 Projects

| # | Project | Category | Key tools |
|---|---------|----------|-----------|
| 1 | [AI Email Triage & Auto-Draft Agent](./projects/01-email-triage-agent) | Communication / Support | n8n, OpenAI API, Gmail, Sheets, Slack |
| 2 | [Lead Enrichment & Scoring Pipeline](./projects/02-lead-enrichment-pipeline) | Sales / RevOps | n8n, OpenAI API, HTTP Request, Sheets, Slack |
| 3 | [Security Alert Triage & Summarization](./projects/03-security-alert-triage) | Security / IT Ops | n8n, OpenAI API, Webhook, Sheets, Slack |

Each project folder contains:
- `workflow.json` — the n8n workflow, ready to import
- `README.md` — problem statement, logic breakdown, diagram, and setup steps

## 🧠 What these projects demonstrate
- Designing multi-step automation logic (triggers, conditionals, branching, error fallbacks)
- Integrating LLMs into real workflows for classification, summarization, and drafting — not just chat
- Working with REST APIs, webhooks, and structured JSON between systems
- Thinking about **data handling and reliability**: fallback parsing when the AI output isn't clean JSON, audit logging, and not overstating what the AI actually knows (see project 3)
- Documenting workflows clearly enough that someone else could pick them up and run them

## ⚙️ How to use these workflows
1. Clone or download this repo.
2. Open your n8n instance (n8n.io cloud or self-hosted).
3. Go to **Workflows → Import from File** and select the `workflow.json` from any project folder.
4. Reconnect your own credentials (Gmail, OpenAI, Google Sheets, Slack) — credentials are never included in exported files.
5. Follow the setup notes in each project's README to configure sheet IDs, channel names, etc.

## 📝 A note on these projects
These are personal / portfolio projects built to demonstrate real automation patterns end-to-end, tested with sample or simulated data rather than live production systems. I'm sharing them as working examples of how I think about and structure automation — happy to walk through the logic or extend any of them in an interview.

## 🛠️ Tech I work with
`n8n` · `Make (Integromat)` · `Zapier` · `OpenAI API` · `Anthropic Claude API` · `Google Workspace` · `Slack API` · `REST APIs / Webhooks` · `JSON` · `Python (basic-intermediate)` · `SQL fundamentals`

## 📬 Contact
Open to remote roles and freelance automation projects — feel free to reach out at [your.email@gmail.com].
