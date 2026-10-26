# n8n Automation Workflows

Production-ready n8n workflows and AI agents built by Safian Abid —
AI Automation & Agentic AI Engineer ([devzink.com](https://devzink.com)).

Each workflow lives in its own folder with its JSON export and a README
explaining what it does, how it works, and how to set it up.

## Workflows

| Workflow | What it does |
| --- | --- |
| [rag-customer-support-website-agent](./rag-customer-support-website-agent) | RAG chatbot that answers questions from website content — scrapes site pages, embeds them in Pinecone, and serves answers through a Gemini-powered AI agent restricted to retrieved data. |

## About these exports

- All workflow JSONs are **sanitized before publishing**: credential references,
  n8n instance IDs, and workflow IDs are removed. Importing a workflow will
  prompt you to connect your own credentials.
- No API keys, tokens, or secrets are ever included — n8n stores credentials
  separately from workflow definitions.
- More workflows land here as they ship.

## Connect

- 🌐 [devzink.com](https://devzink.com)
- 💻 [github.com/Safiandev](https://github.com/Safiandev)
- ✉️ safianabid78@gmail.com
