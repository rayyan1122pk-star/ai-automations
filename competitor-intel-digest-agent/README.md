# Competitor Intel Digest Agent

A scheduled agent that watches a list of competitor websites and news sources, detects what changed since the last run, and emails a short, ranked intelligence digest to your team.

## What it does

- Runs every weekday morning on a schedule
- Reads a watchlist of competitors (name, homepage/pricing URL, news query) from a Google Sheet
- Fetches each page and a news search for each competitor
- Compares a fresh content hash against the last stored hash to find real changes
- An AI Agent summarizes each change, tags it (Pricing, Product, Hiring, Funding, Messaging, Other), and rates impact (Low/Medium/High)
- Sends one HTML email digest, highest-impact items first
- Stores the new hash and a changelog row per competitor in Google Sheets

## Nodes

`Weekday Morning` -> `Get Watchlist (Sheets)` -> `Loop Over Competitors` -> `HTTP: Fetch Page` -> `HTTP: News Search` -> `Detect Change (Code)` -> `Something Changed?` -> `AI Agent: Summarize Change` (+ OpenAI, Structured Output) + `Update Hashes (Sheets)` -> `Append Changelog` -> `Aggregate Findings` -> `Send Digest Email`

## Setup

1. Import `workflow.json` into n8n
2. Connect Google Sheets, OpenAI, and Gmail (or SMTP) credentials
3. Set env vars: `WATCHLIST_SHEET_ID`, `STATE_SHEET_ID`, `DIGEST_RECIPIENTS`, `NEWS_API_KEY`
4. Watchlist sheet columns: `competitor | url | news_query`
5. State sheet: a `state` tab (`competitor | last_hash | last_checked`) and a `changelog` tab

## Notes

- Change detection is diff-based, not "fetch and summarize everything" - the LLM only runs on pages that actually moved, keeping cost low.
- Swap the news step for any provider (NewsAPI, Bing News, SerpAPI) - it only needs to return a list of `{title, url, snippet}`.
- For the first run every competitor is treated as unchanged; hashes are stored so subsequent runs have a baseline.
