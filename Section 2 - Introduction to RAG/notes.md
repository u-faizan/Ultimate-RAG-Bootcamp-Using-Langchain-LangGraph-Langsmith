# Section 2 — Notes (Introduction to RAG)

These are consolidated lecture notes for Section 2 (Introduction to Retrieval-Augmented Generation). This file focuses on core concepts you will use across the bootcamp: the RAG pipeline, embeddings, retrievers, vectorstores, and a short experiments template. Visuals in this folder (`rag_pipeline.svg`, `chunking_flow.svg`) illustrate the pipeline and chunking flow.

---

## 1. What is RAG (short)
Retrieval-Augmented Generation (RAG) augments a language model with an external retrieval step so the model can condition on up-to-date, grounded documents. The retriever finds relevant chunks; the LLM reads that context to produce grounded answers and citations.

When to use RAG
- Knowledge that changes frequently or is too large to store in model weights.
- Need for grounded answers, citations, or traceability.

Core benefits
- Updatability without finetuning
- Reduced hallucinations (when retrieval quality is high)
- Traceability to source documents

---

## 2. RAG pipeline (concise)
1. Document loaders: convert PDFs, Word, JSON, CSV, DB rows into text.
2. Preprocessing: clean, remove headers/footers, normalize whitespace.
3. Chunking / text splitting: choose chunk size and overlap appropriate to your model.
4. Embedding generation: produce vectors for each chunk.
5. Index / vectorstore: upsert vectors + metadata.
6. Retrieval: on query, retrieve top-k candidates.
7. Prompt assembly: include retrieved context and user query in a prompt template.
8. Generation & post-processing: LLM produces answer; extract citations, rerank if needed.

See `rag_pipeline.svg` and `chunking_flow.svg` for visuals.

---

## 3. Chunking recommendations
- Chunk size: aim for chunks that leave room in the model context for the prompt and question (e.g., 512–1024 tokens depending on model).
- Overlap: 10–30% overlap helps prevent lost context at boundaries.
- Metadata: attach source filename, page, paragraph id, and chunk id for traceability.
- Keep chunks coherent (prefer splitting at sentence or paragraph boundaries when possible).

---

## 4. Embeddings
What they are
- Numeric vectors representing semantic meaning. Similar text → nearby vectors.

Model choices
- Hosted APIs (OpenAI embeddings): high quality, simple to use, pay-per-use.
- Managed providers (Cohere, Anthropic): alternatives with tradeoffs in quality & cost.
- Local models (sentence-transformers / SBERT): run locally, cheaper at scale, may need GPU for speed.

Practical tips
- Normalize text before embedding (trim whitespace; avoid heavy stemming).
- Keep original metadata.
- Re-embed when documents change or when switching embedding models.
- Dimensionality affects storage and search performance; higher dims may improve quality but cost more.

Evaluation
- Nearest-neighbor sanity checks (manual inspection).
- Retrieval metrics (recall@k) on a labeled dev set.

---

## 5. Retrievers
Types
- Sparse: BM25 / TF-IDF — good for lexical matches and fast CPU-based search.
- Dense: vector search via embeddings + ANN (HNSW, IVF, PQ) — semantic matches.
- Hybrid: combine sparse and dense scores (often best practical results).

Tuning
- k (candidates returned): start with 10–20 for experiments.
- Distance metric: cosine is common for embeddings; some vectorstores use inner product.
- Re-ranking: use a cross-encoder or a lightweight scoring model to improve ordering.

Failure modes and fixes
- Low recall: increase k, check embeddings, test with nearest neighbor probes.
- Conflicting info: strengthen re-ranking or use evidence verification steps.

---

## 6. Vectorstores & indexing
Options
- FAISS: local, many index types (IndexFlat, HNSW, IVF+PQ), requires care for large corpora.
- Chroma: developer-friendly, integrated with LangChain, good for notebooks.
- Qdrant / Milvus: production-grade vector DBs with features like persistence and replication.
- Pinecone / Weaviate: hosted managed services.

Recommendations
- Prototype: Chroma or FAISS IndexFlat for simplicity.
- Production: Qdrant / Milvus or hosted providers depending on scale and SLA.
- Store metadata alongside vectors; ensure you can export/import snapshots for reproducibility.

Local FAISS quick example (conceptual)
```python
import faiss
# vectors: numpy array shape (n, d)
index = faiss.IndexFlatIP(d)  # use IndexFlatL2 or IP depending on normalization
index.add(vectors)
D, I = index.search(query_vecs, k)
```

---

## 7. Experiments template (keep short)
- ID: exp_YYYYMMDD_N
- Objective: what you test (e.g., embeddings A vs B recall@5)
- Dataset: brief description (docs, QA pairs)
- Env: python version, env name
- Embedding model: name
- Vectorstore: type + index params
- Retriever: k and strategy
- Reranker: model or heuristic
- Results: recall@k, MRR, latency, cost estimate
- Notes: observations and next steps

Keep one parameter change per experiment for clarity.

---

## 8. Quick links & references
- LangChain docs: https://langchain.readthedocs.io
- RAG paper: Lewis et al., Retrieval-Augmented Generation for Knowledge-Intensive NLP
- Files in this folder: `rag_pipeline.svg`, `chunking_flow.svg` (visuals), plus PDFs provided by the instructor.

---

This notes file intentionally contains focused lecture notes and practical references only. If you want, I can later add a small runnable demo (Python script) under a scripts/ folder that performs embed→index→query using a local vectorstore; tell me if you'd like that and whether you prefer a script or a notebook.
