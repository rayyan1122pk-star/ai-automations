# AI Review/Reputation Monitor

Monitors a business's Google reviews, catches new ones automatically, and drafts a response for each — empathetic for negative reviews with an immediate Slack alert, warm and thankful for positive ones.

## What it does

- Every 6 hours, fetches the latest reviews for a configured Google Places listing
- Tracks the last-seen review timestamp in workflow static data so it never reprocesses the same review twice
- Branches by rating: reviews of 3★ or below get an empathetic, apologetic draft response and an immediate Slack alert to the team; higher-rated reviews get a warm thank-you draft
- Logs every review and its drafted response to a sheet for tracking and eventual manual posting

## Nodes

`Schedule (6h)` → `Fetch Reviews` → `Filter New Reviews` (Code, dedup via static data) → `If Rating <= 3` → `Draft Empathetic Response` (+ Slack alert) / `Draft Thank-You Response` → `Log Review & Response`

## Setup

1. Import `workflow.json` into n8n
2. Set `GOOGLE_MAPS_API_KEY` and `BUSINESS_PLACE_ID` as environment variables
3. Connect Slack, Google Sheets, and OpenAI credentials
4. Responses are drafted for review, not auto-posted — Google's My Business API can be added separately if you want direct posting
