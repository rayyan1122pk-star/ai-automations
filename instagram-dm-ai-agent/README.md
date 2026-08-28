# Instagram DM AI Agent

An AI agent that automatically responds to Instagram DMs — verifying webhook events, answering customer questions using a live knowledge-base tool, and maintaining conversation memory per user.

## What it does

- Handles the Meta webhook verification handshake (GET) and message events (POST) on the same endpoint
- Extracts sender ID and message text from the Instagram Graph API payload
- Routes the message to an n8n native AI Agent with:
  - **OpenRouter Chat Model** — swappable LLM backend (works with Groq/Gemini too via the same OpenAI-compatible interface)
  - **Conversation Memory** — keyed per Instagram user so context persists across messages
  - **get_agency_info tool** — a Supabase-backed knowledge base the agent queries for real facts instead of hallucinating
- Sends the AI's reply back via the Instagram Graph API `/me/messages` endpoint

## Nodes

`Webhook` → `If (verification?)` → `Respond With Challenge` / `Acknowledge Event` → `Extract Message Data` → `AI Agent` (+ Chat Model, Memory, Tool) → `Send Instagram Reply`

## Setup

1. Import `workflow.json` into n8n
2. Set environment variables: `INSTAGRAM_PAGE_ACCESS_TOKEN`, `SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY`
3. Register the webhook's production URL with Meta's App Dashboard (Instagram → Webhooks), subscribed to `messages`
4. Create a Supabase table (`agency_info`) with your own business facts for the tool to query
