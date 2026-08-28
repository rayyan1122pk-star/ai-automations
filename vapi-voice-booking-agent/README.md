# AI Voice Agent — Automated Call Booking & Lead Qualification

A voice AI system (Vapi + n8n) that answers calls, extracts booking details, checks calendar availability, books appointments automatically, and routes qualified vs. unqualified leads.

## What it does

- Receives Vapi function-call and end-of-call webhook events on one endpoint, routed by event type
- On a booking function call: extracts caller name/requested time, checks Google Calendar availability, books the event if free, and responds back to Vapi with the result (so the voice agent can tell the caller)
- On end-of-call: logs the call to Google Sheets, then checks Vapi's built-in success evaluation to branch — qualified leads notify the sales team on Slack, unqualified leads get an automated follow-up email

## Nodes

`Vapi Call Webhook` → `Route Event Type` (Switch) → `Extract Booking Params` → `Check Calendar Availability` → `If Slot Free` → `Create Calendar Event` / `Respond: Slot Taken`
(parallel branch) → `Log Call to Google Sheet` → `If Qualified Lead` → `Notify Sales Team (Slack)` / `Send Follow-up Email`

## Setup

1. Import `workflow.json` into n8n
2. Connect Google Calendar, Google Sheets, Slack, and Gmail credentials
3. Configure your Vapi assistant with function-calling tools (`checkAvailability`, `bookSlot`) pointing at this webhook's URL
4. Adjust the qualification condition to match your Vapi assistant's `successEvaluation` config
