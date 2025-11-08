# Vector Stores and Vector Databases — Notes

## Overview
Vector stores persist embeddings and provide approximate nearest neighbor (ANN) search to retrieve semantically similar chunks. They are central to RAG performance and cost.

## Common Systems
- FAISS: fast, local, flexible. Good for prototyping and on-prem. Manual persistence/tuning.
- Chroma: easy local store with Python-first API and embedding integration.
- Pinecone: managed vector DB with scalability and APIs; good for production.
- Milvus / Weaviate: open-source vector DBs with rich feature sets (hybrid search, metadata filters, cloud options).
- DataStax (Astra DB with vector support): vector capabilities in a broader DB ecosystem.

## Index Types and Algorithms
- HNSW (Hierarchical Navigable Small World): widely used; supports dynamic inserts; low latency
- IVF (Inverted File) + PQ (Product Quantization): good for very large corpora and disk-backed indexes
- Flat (exact search): uses more memory but returns exact nearest neighbors

## Integration Patterns
1. Generate embeddings → store vectors in a vector DB with metadata
2. On query: compute embedding → top-K similarity search → optional rerank (cross-encoder/LLM)
3. Persist provenance info (source file, chunk index, offsets)

## Performance and Scaling
- Use ANN indexes for sub-second queries at scale
- Partition by tenant or dataset for multi-tenant systems
- Cache hot queries; pre-compute frequently used embeddings

## Security and Operations
- Keep API keys out of notebooks/code. Use environment variables or secret managers
- Monitor costs for managed services; set alerts for index size and request volume
- Back up embeddings and metadata; ensure disaster recovery for critical datasets

## Trade-offs Snapshot
- FAISS: + speed, - managed features, - manual persistence
- Pinecone: + managed, + scaling, - cost
- Chroma: + easy local usage, + pythonic, - limited at massive scale

## Notebook Summaries
- `1-chromadb.ipynb`: create a Chroma collection, add embeddings, simple queries
- `2-faiss.ipynb`: index creation, parameter tuning (nlist/nprobe), benchmarking
- `3-Othervectorstores.ipynb`: demos of Milvus / Weaviate / DataStax approaches
- `PineconeVectorDB.ipynb`: Pinecone setup, indexing, metadata filtering
- `Datastaxdb+(1).ipynb`: DataStax vector features

## Pre‑Production Checklist
- Choose model and chunking strategy; freeze for stable indexes
- Decide managed vs self-hosted based on budget and SLA
- Add tests to validate retrieval recall and latency
- Secure keys and rotate periodically

