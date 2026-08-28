# AI Meeting Notes & Follow-up Agent

Transcribes a meeting recording, summarizes it into decisions and action items, emails the summary to attendees, and logs action items for tracking.

## What it does

- Receives a recording URL via webhook (from Zoom, Google Meet, or any recording tool with a webhook/export)
- Downloads the audio and transcribes it with OpenAI Whisper
- An AI Agent extracts a summary, key decisions, and action items (each with an owner where mentioned) via structured output
- Emails the summary and action items to all attendees
- Logs every action item to a Google Sheet for tracking

## Nodes

`Webhook` → `Download Audio` → `Transcribe (Whisper)` → `AI Agent: Summarize` (+ OpenAI, Structured Output) → `Send Summary Email` / `Log Action Items`

## Setup

1. Import `workflow.json` into n8n
2. Connect OpenAI, Gmail, and Google Sheets credentials
3. POST `{ "recording_url": "...", "attendee_emails": "..." }` to the webhook after each meeting
4. Optionally chain a Google Calendar node to auto-create follow-up tasks from the action items
