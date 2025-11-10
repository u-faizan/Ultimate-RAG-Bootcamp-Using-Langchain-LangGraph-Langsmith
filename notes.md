# RAG Quick Recall — Repo Root Notes

This file summarizes core concepts so you can quickly refresh your memory without opening individual sections. It consolidates material from Sections 1–7.

---

## What is RAG?
Retrieval-Augmented Generation combines a retrieval system with an LLM so outputs are grounded in external documents. The retriever locates relevant chunks; the LLM uses that context to answer with citations and improved factuality.

Use cases
- Domain knowledge too large or fast-changing to fit in model weights
- Need for traceable, citation-backed answers

Benefits
- Update knowledge without finetuning
- Reduced hallucinations (with good retrieval)
- Source traceability and auditability

---

## RAG Pipeline (end-to-end)
1. Load documents (PDF, DOCX, CSV, JSON, DB rows)
2. Preprocess and clean text (remove boilerplate, normalize whitespace)
3. Chunk text with overlap (keep coherence at sentence/paragraph boundaries)
4. Generate embeddings per chunk
5. Index in a vector store with metadata (source, page, ids)
6. Retrieve top-k candidates for a query
7. Build the prompt with retrieved context
8. Generate and post-process (citations, re-ranking, formatting)

---

## Core Components (Section 3)
- Document loaders and stores: PDFs, DOCX, CSV, JSON, DB rows; attach provenance metadata
- Embedding system: model choice, dimensionality, throughput
- Retrieval system: index types, ranking, filters, caching
- Generation system: prompt templates, formatting, model selection
- Orchestration: LangChain chains/agents, LangGraph flows
- Evaluation: relevance, latency, hallucination checks

---

## Ingestion and Parsing (Section 5)
- Loaders: text, PDF (PyPDF), Word (python-docx), CSV/Excel (pandas), JSON/JSONL, DB rows
- Text splitters: RecursiveCharacter, Token, etc.; set chunk size/overlap intentionally
- Preprocessing: normalize whitespace, remove boilerplate, handle encoding
- Data folder structure: keep sample files and formats for reproducible labs

---

## Embeddings (Section 6)
- Models: OpenAI, sentence-transformers (MiniLM, MPNet), local vs hosted
- Similarity metrics: cosine, dot product; normalize vectors for IP
- Indexing: ANN for large datasets; tune parameters (nlist/nprobe, efSearch)
- Reranking: cross-encoders or LLM scoring for better ordering

---

## Vector Stores (Section 7)
- Options: FAISS, Chroma, Milvus, Pinecone, Weaviate, DataStax
- Algorithms: HNSW, IVF, PQ; Flat for exact search
- Configuration: FAISS (IndexFlat, IVF+PQ), HNSW (M, ef), Pinecone (metric, pods), Chroma (persist)
- Operations: snapshot/export, reindex on model changes, hybrid retrieval (sparse + dense)

---

## Chunking Guidance
- Target chunk size: 512–1024 tokens, leaving room for the prompt and question
- Overlap: 10–30% to preserve boundary context
- Metadata: always attach source filename, page, paragraph id, chunk id
- Keep chunks coherent (sentence/paragraph boundaries preferred)

---

## Minimal Experiment Template
- ID: exp_YYYYMMDD_N
- Objective: e.g., embeddings A vs B recall@5
- Dataset: docs + QA pairs
- Env: python version, env name
- Embedding: model name
- Vector store: type and index params
- Retriever: k and strategy
- Reranker: model or heuristic
- Metrics: recall@k, MRR, latency, cost
- Notes: observations and next steps

---

## Navigation
- Section 1 notes: `Section 1 - Intro/notes.md`
- Section 2 notes: `Section 2 - Introduction to RAG/notes.md`
- Section 3 notes: `Section 3 - Core Components in RAG/notes.md`
- Section 4 notes: `Section 4 - Anaconda Installation And VS Code Installation/notes.md`
- Section 5 notes: `Section 5 - Data Ingestion and Data Parsing Techniques/notes.md`
- Section 6 notes: `Section 6 - Vector Embedding and vector Data Bases/notes.md`
- Section 7 notes: `Section 7 - Vector Stores and Vector Data Bases/notes.md`

