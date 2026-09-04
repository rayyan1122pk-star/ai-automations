# Ascenta — AI Automations & Agents

A collection of production-style n8n workflows built for real business automation use cases: AI agents, lead generation, financial ops, content, and customer support. Each folder contains a working `workflow.json` (importable directly into n8n) and a `README.md` explaining what it does and how it's wired.

Built by [Ascenta](https://ascenta-agency.vercel.app) — web development & AI automation agency.

## Workflows

| Workflow | Category | Description |
|---|---|---|
| [instagram-dm-ai-agent](./instagram-dm-ai-agent) | Customer Engagement | AI agent that auto-responds to Instagram DMs using a live knowledge base |
| [vapi-voice-booking-agent](./vapi-voice-booking-agent) | Voice AI | AI voice agent that answers calls, qualifies leads, and books appointments |
| [gmail-ai-auto-responder](./gmail-ai-auto-responder) | Email Automation | Drafts AI-generated replies to unread emails automatically |
| [lahore-live-data-system](./lahore-live-data-system) | Data Aggregation | Real-time multi-API city data feed with rule-based alerting |
| [ai-accountant-agent](./ai-accountant-agent) | Finance | Extracts invoice data, categorizes expenses, flags anomalies, logs to a ledger |
| [lead-scraper-enrichment-agent](./lead-scraper-enrichment-agent) | Sales | Finds and scores local business leads from Google Maps data |
| [content-repurposing-agent](./content-repurposing-agent) | Content | Turns one long-form piece into platform-specific social variants |
| [invoice-payment-reminder-agent](./invoice-payment-reminder-agent) | Finance | Tracks due/overdue invoices and sends automated reminders |
| [support-ticket-triage-agent](./support-ticket-triage-agent) | Customer Support | Classifies incoming support emails and routes or drafts replies |
| [meeting-notes-followup-agent](./meeting-notes-followup-agent) | Productivity | Transcribes calls, summarizes action items, emails follow-ups |
| [social-media-scheduler-agent](./social-media-scheduler-agent) | Content | Posts scheduled content across platforms automatically |
| [job-application-draft-agent](./job-application-draft-agent) | Outreach | Finds matching job posts and drafts tailored applications for review |
| [ecommerce-inventory-sync-agent](./ecommerce-inventory-sync-agent) | E-commerce | Syncs orders to inventory and alerts on low stock |
| [review-reputation-monitor-agent](./review-reputation-monitor-agent) | Reputation | Monitors new reviews and drafts responses automatically |
| [whatsapp-order-taking-agent](./whatsapp-order-taking-agent) | Commerce | Conversational WhatsApp agent that takes orders against a live catalog and logs them |
| [rag-company-knowledge-agent](./rag-company-knowledge-agent) | Internal Ops | Slack RAG assistant answering from company docs, with a nightly ingestion workflow |
| [competitor-intel-digest-agent](./competitor-intel-digest-agent) | Market Intelligence | Diff-based competitor watch that emails a ranked change digest each weekday |

## Stack

n8n (workflow engine) · OpenRouter / OpenAI (LLM providers) · Supabase / Google Sheets (data) · Google Calendar, Gmail, Slack, WhatsApp, Instagram Graph API (integrations)

## Note on credentials

All API keys and credential IDs in these workflows are referenced via environment variables (`$env.VARIABLE_NAME`) or placeholder credential IDs — never hardcoded. Set your own credentials in n8n before importing.
