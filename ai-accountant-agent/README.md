# AI Accountant Agent

Extracts invoice/expense data from inbound emails, categorizes spend, logs it to a running ledger, and generates monthly financial summaries — with large-expense alerts along the way.

## What it does

- Every 6 hours, scans Gmail for unread emails labeled "invoices"
- An AI Agent extracts vendor, amount, currency, date, and a best-guess expense category via structured output
- Appends each entry to a Google Sheets ledger and marks the source email as processed
- Flags any expense over $500 with an immediate Slack alert to a finance channel
- On the 1st of each month, reads the full ledger, computes total spend and a per-category breakdown, and emails a summary report

## Nodes

`Schedule (6h)` → `Get Invoice Emails` → `AI Agent` (extract) → `Append to Ledger` → `If > $500` → `Slack Alert` / `Mark Processed`
`Schedule (monthly)` → `Read Ledger` → `Compute Summary` → `Send Monthly Summary`

## Setup

1. Import `workflow.json` into n8n
2. Connect Gmail, Google Sheets, Slack, and OpenAI credentials
3. Create a Gmail label "invoices" (source) and "Processed" (destination)
4. Set your own Google Sheet as the ledger and update the recipient email in the summary node
