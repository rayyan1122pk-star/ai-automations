# Lead Scraper & Enrichment Agent

Finds local business leads via Google Maps, scores them by opportunity signals (no website, low rating with many reviews, review volume), and logs high-potential leads with an instant Slack alert.

## What it does

- Searches Google Places Text Search for a keyword + location (e.g. "dentist in Lahore")
- Splits results into individual leads
- Scores each lead using simple, explainable rules: businesses with no website score highest (clear web-dev opportunity), followed by reputation-management opportunities (low rating, many reviews) and established businesses with real review volume (budget signal)
- Appends every lead to a Google Sheet regardless of score, so nothing is lost
- Sends a Slack alert immediately for any lead scoring 50+

## Nodes

`Manual Trigger` → `Google Maps: Search Businesses` → `Split Out` → `Score Lead` (Code) → `Append to Leads Sheet` → `If High Score` → `Notify Hot Lead`

## Setup

1. Import `workflow.json` into n8n
2. Set `GOOGLE_MAPS_API_KEY` as an environment variable (enable Places API in Google Cloud Console)
3. Connect Google Sheets and Slack credentials
4. Trigger manually with `{ "keyword": "...", "location": "..." }`, or swap the Manual Trigger for a schedule to run it on autopilot
