# Customer Support Ticket Triage Agent

Classifies incoming support emails by category, urgency, and sentiment, then routes each one to the right place — billing team on Slack, a technical ticket log, or an auto-drafted reply for general questions.

## What it does

- Polls a support inbox for unread emails
- An AI Agent classifies each email (category: Billing/Technical/General, urgency, sentiment) via structured output
- Routes by category: Billing tickets ping a Slack channel with urgency noted, Technical tickets get logged to a tracking sheet, General questions get an auto-drafted reply
- Labels every processed email "Triaged" so nothing gets handled twice

## Nodes

`Gmail Trigger` → `AI Agent: Classify` (+ OpenAI, Structured Output) → `Switch by Category` → `Notify Billing` / `Log Technical Ticket` / `Draft Auto-Reply` → `Label as Triaged`

## Setup

1. Import `workflow.json` into n8n
2. Connect Gmail, Slack, Google Sheets, and OpenAI credentials
3. Create Gmail labels "support" (source) and "Triaged" (destination)
4. Adjust the classification categories to match your actual support taxonomy
