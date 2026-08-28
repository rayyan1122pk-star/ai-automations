# Social Media Scheduler & Auto-Poster

Reads approved, scheduled posts from a Google Sheet and publishes them automatically across Instagram, LinkedIn, and Twitter/X at the right time.

## What it does

- Checks a "ScheduledPosts" sheet every hour for pending posts
- Filters to posts whose scheduled time has arrived
- Routes each post to the right platform's API based on a `platform` column
- Marks each post "posted" once published, so it's never sent twice

## Nodes

`Schedule (hourly)` → `Read Scheduled Posts` → `Filter Due Now` → `Route by Platform` → `Post to Instagram` / `Post to LinkedIn` / `Post to Twitter` → `Mark as Posted`

## Setup

1. Import `workflow.json` into n8n
2. Connect Instagram Graph API, LinkedIn, and Twitter/X credentials
3. Your sheet needs columns: `platform`, `content`, `media_url`, `scheduled_time`, `status`
4. Feed it from the Content Repurposing Agent for a full draft → schedule → publish pipeline
