# WhatsApp Order-Taking AI Agent

A conversational AI agent that takes customer orders over WhatsApp, validates items against a live product catalog, calculates the total, confirms with the customer, and logs the order for fulfilment.

## What it does

- Receives inbound WhatsApp messages via the WhatsApp Business Cloud API webhook
- Loads the current product catalog (name, price, stock) from a Google Sheet
- An AI Agent holds a natural back-and-forth with the customer, using the catalog as a tool to check prices and availability
- When the customer confirms, the agent emits a structured order (items, quantities, total, delivery address)
- The order is appended to an `Orders` sheet and a confirmation message is sent back over WhatsApp
- Low-stock items are flagged to a Slack channel

## Nodes

`WhatsApp Trigger` -> `Get Catalog (Sheets)` -> `AI Agent: Order Assistant` (+ OpenAI, Catalog Tool, Session Memory, Structured Output) -> `Order Confirmed?` -> `Append Order (Sheets)` + `Notify Low Stock (Slack)` / `Send WhatsApp Reply`

## Setup

1. Import `workflow.json` into n8n
2. Connect WhatsApp Business Cloud, Google Sheets, OpenAI, and Slack credentials
3. Set env vars: `CATALOG_SHEET_ID`, `ORDERS_SHEET_ID`, `LOW_STOCK_SLACK_CHANNEL`, `WHATSAPP_PHONE_NUMBER_ID`
4. Point your WhatsApp Business number's webhook at the trigger URL
5. Catalog sheet columns: `sku | name | price | stock`

## Notes

- The agent is instructed never to invent products or prices - it only sells what the catalog tool returns.
- Session memory is keyed by the customer's phone number so multi-message orders stay in context.
