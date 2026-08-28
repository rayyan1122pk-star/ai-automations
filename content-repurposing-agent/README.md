# AI Content Repurposing Agent

Takes one piece of long-form content and automatically generates platform-specific variants — a Twitter/X thread, a LinkedIn post, and an Instagram caption — keeping the core message consistent.

## What it does

- Receives long-form content via webhook (e.g. from a blog CMS or a Google Drive trigger)
- An AI Agent with structured output returns three tailored variants in one call, matched to each platform's tone and format
- Saves all drafts to a Google Sheet for human review before anything goes live
- Notifies a Slack channel when new drafts are ready

## Nodes

`Webhook` → `AI Agent: Generate Variants` (+ OpenAI, Structured Output) → `Save Drafts to Sheet` → `Notify Ready for Review` → `Respond to Webhook`

## Setup

1. Import `workflow.json` into n8n
2. Connect OpenAI, Google Sheets, and Slack credentials
3. POST `{ "content": "..." }` to the webhook, or trigger it from your CMS/Drive on new content
4. Drafts are never auto-posted — review and publish manually, or chain into the Social Media Scheduler Agent once approved
