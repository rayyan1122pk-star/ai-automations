# Invoice & Payment Reminder Agent

Tracks a Google Sheets invoice ledger and automatically sends payment reminders — a friendly nudge before the due date, and an escalated tone once significantly overdue.

## What it does

- Runs daily and reads all unpaid invoices from a Google Sheet
- Filters to invoices due within 3 days or already overdue
- Branches tone by days overdue: a friendly reminder for upcoming/just-due invoices, an escalated reminder for anything over 7 days overdue
- Updates the sheet with the last-reminder timestamp so reminders don't spam the client

## Nodes

`Schedule (daily)` → `Read Invoices` → `Filter Overdue/Due Soon` (Code) → `If Overdue > 7 Days` → `Send Escalated Reminder` / `Send Friendly Reminder` → `Update Last Reminder Sent`

## Setup

1. Import `workflow.json` into n8n
2. Connect Google Sheets and Gmail credentials
3. Your sheet needs columns: `invoice_number`, `client_email`, `due_date`, `status`, `last_reminder_sent`
4. Adjust the overdue threshold and reminder copy to match your tone
