# Job Application Draft Agent

Scans job listings for relevant matches, generates a tailored cover letter for each, and creates a Gmail draft for human review — never auto-sends.

## What it does

- Daily search of job board listings for relevant keywords
- Filters to genuinely matching listings (skill/keyword overlap)
- An AI Agent writes a short, tailored cover letter per listing, referencing real experience
- Creates a Gmail **draft** (not sent) addressed to the listing's contact email, and logs the application to a tracking sheet
- Notifies via Slack when new drafts are ready for review

## Nodes

`Schedule (daily)` → `Search Job Boards` → `Filter Matching Listings` (Code) → `Generate Cover Letter` (AI Agent) → `Create Gmail Draft` / `Log Application Status` → `Notify Drafts Ready`

## Setup

1. Import `workflow.json` into n8n
2. Swap the job board HTTP request for your actual source (LinkedIn Jobs RSS, Indeed API, a scraper, etc. — the placeholder URL is illustrative)
3. Connect Gmail, Google Sheets, Slack, and OpenAI credentials
4. **By design, this never sends automatically** — every draft requires manual review and send, consistent with responsible outreach practice
