# RAG Customer Support Website Agent

An n8n AI agent that answers questions about a website using **retrieval-augmented
generation (RAG)** — it only answers from content actually scraped from the site,
never from the model's general knowledge.

Built for [DevZink](https://devzink.com) — the agent knows DevZink's services,
company info, and contact details because it ingested devzink.com itself.

## How it works

Two flows in one workflow (19 nodes):

### 1. Ingestion flow (manual trigger)

1. Four HTTP Request nodes fetch the site's pages: Home, Services, About, Contact.
2. Four HTML nodes extract the meaningful sections via CSS selectors
   (hero, services, process, about, contact list, ...).
3. The extracts are merged, split with a Recursive Character Text Splitter,
   embedded with **Google Gemini embeddings**, and inserted into a
   **Pinecone** vector index.

### 2. Chat flow (RAG agent)

1. A chat trigger receives the visitor's question.
2. An **AI Agent** node (Google Gemini chat model) answers using:
   - the Pinecone vector store **as a tool** — it must search the index
     before answering,
   - a short conversation memory (buffer window),
   - a system prompt that restricts it to retrieved data only.

## Stack

- n8n (workflow engine)
- Google Gemini — chat model + embeddings
- Pinecone — vector store (retrieval + insert)
- LangChain nodes inside n8n (AI Agent, text splitter, data loader)

## Setup (import in your own n8n)

1. Import `rag-customer-support-website-agent.json` into n8n.
2. Connect your own credentials when prompted:
   - Google Gemini API (chat model + embeddings nodes),
   - Pinecone API (both vector store nodes).
3. Create a Pinecone index and set its name in both vector store nodes
   (this copy uses `devzink3`).
4. Point the four HTTP Request nodes at your own website's pages and adjust
   the CSS selectors in the HTML nodes to match your site's structure.
5. Run the ingestion flow once (manual trigger) to fill the index,
   then activate the chat flow.

## Notes

- No credentials are included in this file — n8n stores credentials separately
  from workflow JSON, and all credential references were removed before publishing.
- The workflow name inside n8n was "Basics"; it is published here under its
  descriptive name.
