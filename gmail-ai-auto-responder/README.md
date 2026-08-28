# Gmail AI Auto-Responder

An agent that monitors an inbox for unread emails, decides whether it has enough information to draft a reply, and drafts one automatically using structured output — cutting manual email triage.

## What it does

- Polls Gmail every minute for unread messages
- Extracts sender, subject, and body
- Passes the email to an AI Agent with a structured output parser returning `{ can_respond, draft_reply }`
- If the agent has enough context, it creates a Gmail draft reply and labels the thread "Action" for human review before sending
- If not, the email is left untouched for manual handling — the agent never sends automatically, only drafts

## Nodes

`Gmail Trigger` → `Get Unread Email` → `Get Required Fields` → `AI Agent` (+ OpenAI model, Memory, Structured Output Parser) → `If Can Respond` → `Create a draft` → `Label Email`

## Setup

1. Import `workflow.json` into n8n
2. Connect a Gmail OAuth2 credential and an OpenAI credential
3. Create a Gmail label named "Action" (or change the label ID in the last node)
4. Activate — drafts always require manual send, by design
