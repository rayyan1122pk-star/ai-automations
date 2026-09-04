# RAG Company-Knowledge Slack Agent

A retrieval-augmented AI assistant that answers employee questions in Slack from your own company documents, with citations. Includes a separate ingestion workflow that keeps the knowledge base current.

## What it does

**Ingestion (scheduled)**
- Runs nightly, pulls documents from a Google Drive folder
- Splits them into chunks, embeds each chunk with OpenAI embeddings
- Upserts vectors into a Supabase (pgvector) table, tagging each chunk with its source file ID and name

**Answering (Slack)**
- Triggers on an app mention in Slack
- An AI Agent retrieves the most relevant chunks from Supabase as a tool
- Answers in the thread, quoting the source document
- If nothing relevant is retrieved, it says the knowledge base does not cover the question instead of guessing

## Nodes

**Ingest:** `Nightly Schedule` -> `Drive: List Files` -> `Download File` -> `Supabase Vector Store (insert)` (+ Embeddings, Default Data Loader + Recursive Splitter)

**Answer:** `Slack Trigger` -> `AI Agent: Knowledge Assistant` (+ OpenAI, Supabase Retriever Tool) -> `Slack: Reply in Thread`

## Setup

1. Import `workflow.json` into n8n - it contains two disconnected graphs (ingest + answer)
2. Create the Supabase table and `match_documents` function per the n8n Supabase Vector Store docs
3. Connect Google Drive, OpenAI, Supabase, and Slack credentials
4. Set env vars: `KB_DRIVE_FOLDER_ID`, `SUPABASE_KB_TABLE`
5. Invite the Slack bot to the channels where people should be able to ask questions

## Notes

- The agent's system prompt forbids answering from general knowledge - it must ground every answer in retrieved chunks or decline.
- Chunks carry `file_id` metadata so re-ingesting an edited document is straightforward to reconcile.
