# Lahore Live — Real-Time City Data & Alert System

An automated pipeline that aggregates live weather, air quality, financial market, flight-tracking, and civic data for Lahore from 8+ public APIs, merges it into a single normalized dataset, and runs threshold-based alert detection.

## What it does

- Pulls live data from Open-Meteo (weather + air quality), OpenAQ (ground sensor stations), Overpass/OSM (hospitals, schools, police, parks), open.er-api.com (forex), PSX Data Portal (KSE100/KMI30 indices), a gold/silver spot API, OpenSky Network (flight tracking), and Tavily Search (civic info fallback for data with no public API)
- Runs on two triggers: an hourly schedule for live data, and a REST webhook for on-demand queries — both feed the same merge/alert pipeline
- Custom JavaScript (n8n Code nodes) normalizes every source into one consistent JSON shape
- Rule-based alerting flags extreme heat, flood risk, and hazardous air quality
- Logs every run to Google Sheets for historical tracking
- Every external call uses `onError: continueRegularOutput` — if one API is down, the pipeline still returns partial results instead of failing completely

## Nodes

`Schedule Trigger` → `HTTP Request` (×8 data sources) → `Code` (merge + normalize) → `Code` (alert detection) → `Google Sheets` (log) / `Respond to Webhook`

## Setup

1. Import `workflow.json` into n8n
2. Set `OPENAQ_API_KEY` and `TAVILY_API_KEY` as environment variables in your n8n instance
3. Connect your own Google Sheets credential and replace the placeholder document ID
4. Activate the workflow — the webhook path is `/lahore-live`
