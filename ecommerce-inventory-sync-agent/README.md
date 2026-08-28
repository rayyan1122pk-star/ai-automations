# E-commerce Order & Inventory Sync Agent

Syncs incoming store orders to a live inventory sheet, decrements stock automatically, and alerts on low stock with a supplier reorder notification.

## What it does

- Receives new-order webhooks (Shopify/WooCommerce-style payload)
- Parses each line item and looks up current stock for that SKU
- Decrements stock in the Google Sheets inventory
- If stock falls below 10 units, sends a Slack alert and emails the supplier to reorder
- Logs every order for record-keeping

## Nodes

`Webhook` → `Parse Order Line Items` → `Look Up Current Stock` → `Decrement Stock` → `If Stock Below 10` → `Slack Alert` / `Notify Supplier` (parallel) `Log Order`

## Setup

1. Import `workflow.json` into n8n
2. Register the webhook URL with your store platform's order-created webhook
3. Connect Google Sheets and Slack/Gmail credentials
4. Your Inventory sheet needs `sku` and `stock` columns; adjust the low-stock threshold as needed
