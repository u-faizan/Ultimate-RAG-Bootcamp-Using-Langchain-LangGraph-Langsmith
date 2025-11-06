# Section 1 — Notes

These are my consolidated lecture notes for Section 1 (Introduction). The file contains essential notes and references.

## Overview
Retrieval-Augmented Generation (RAG) augments large language models with an external retrieval step so the model can condition on up-to-date, grounded documents. The retriever finds relevant text; the LLM uses that context to generate answers with citations.

## Core pipeline (brief)
1. Ingest documents (PDF, DOCX, JSON, CSV, DB rows)
2. Preprocess and clean text (remove boilerplate, normalize whitespace)
3. Chunk documents to fit model context with overlap
4. Compute embeddings for chunks
5. Insert vectors + metadata into a vector store
6. On query: retrieve top-k candidates, assemble prompt, call LLM, and produce an answer with citations

## Key concepts
- Chunking: choose sizes to balance context vs. specificity; overlap helps preserve context across boundaries
- Metadata: preserve source, page, paragraph id for traceability and citations
- Embeddings: pick a model based on quality, cost, and latency needs
- Retriever types: sparse (BM25) for lexical matches, dense (vector) for semantic matches; hybrid often combines strengths

## Short references
- RAG paper: Lewis et al., Retrieval-Augmented Generation for Knowledge-Intensive NLP
- LangChain docs: https://langchain.readthedocs.io

---
This file intentionally contains focused notes; exercises and cheatsheets are omitted to keep it concise.
