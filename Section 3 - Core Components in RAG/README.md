# Section 3 — Core Components in RAG

This section should consolidate the core building blocks of a RAG system. Use this README as a checklist and quick reference while you work through lectures and demos.

Core components
---------------
- Document loaders (PDF, Word, JSON, CSV, databases)
- Chunking & text splitting strategies
- Embeddings (model options and tradeoffs)
- Vector stores / indexers (FAISS, Chroma, Milvus, etc.)
- Retriever types and tuning (k, score threshold, hybrid strategies)
- Prompt templates and response shaping
- Orchestration (LangChain chains, agents, LangGraph flows)
- Evaluation / metrics (relevance, latency, hallucination checks)

Suggested files to add
----------------------
- `loaders.md` — loader patterns and examples.
- `chunking.md` — chunking strategies and code snippets.
- `embeddings.md` — models used and evaluation notes.
- `vectorstores.md` — local setup notes for FAISS/Chroma.
- `prompts.md` — prompt recipes and templates.

Best practices / reminders
--------------------------
- Keep small reproducible experiments (one notebook per experiment).
- Keep metadata with chunks (source, page, timestamp) so you can trace answers back to originals.
- Save reproducible environment setup (requirements.txt or conda env export) near the notes.

---
This README is a structural hub for Section 3. Add code examples and links to notebooks as you progress.