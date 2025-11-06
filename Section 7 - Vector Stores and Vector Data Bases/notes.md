# Vector Stores and Vector Databases - Notes

## Overview

Vector stores persist vector embeddings and provide approximate nearest neighbor (ANN) search to retrieve semantically similar document chunks. They are central to RAG performance and cost.

## Common systems

- FAISS: fast, local, flexible. Good for prototyping and on-prem setups. Requires manual persistence and tuning.
- Chroma: easy local store with Python-first API and embeddings integration.
- Pinecone: managed vector DB with scalability and APIs; good for production.
- Milvus / Weaviate: open-source vector DBs with rich feature sets (hybrid search, metadata filters, cloud-hosted options).
- Datastax (Astra DB with vector support): vector capabilities built into larger DB ecosystems.

## Index types & algorithms

- HNSW (Hierarchical Navigable Small World): widely used, great for dynamic inserts and low latency.
- IVF (Inverted File) + PQ (Product Quantization): good for very large corpora and disk-backed indexes.
- Flat (exact search): uses more memory but returns exact nearest neighbors.

## Integration patterns

1. Embedding generation → store vectors in vector DB with metadata
2. For queries: compute embedding → vector DB top-K similarity search → optional rerank with cross-encoder or LLM
3. Persist provenance info (source file, chunk index, offsets)

## Performance & scaling

- Use ANN indexes for sub-second queries at scale.
- Partition by tenant or dataset for multi-tenant systems.
- Use caching for hot queries and pre-compute frequently used embeddings.

## Security & operations

- Keep API keys out of notebooks and code. Use environment variables or secret managers.
- Monitor costs for managed services; set up alerts for index size and request volume.
- Back up embeddings and metadata; ensure disaster recovery for critical datasets.

## Example: trade-offs table (short)

- FAISS: + speed, - managed features, - persistence (manual)
- Pinecone: + managed, + scaling, - cost
- Chroma: + easy to use locally, + pythonic, - less mature at massive scale

## Notebook summaries

- `1-chromadb.ipynb`: shows creating a Chroma collection, adding embeddings, simple queries.
- `2-faiss.ipynb`: index creation, parameter tuning (nlist/nprobe), and benchmarking.
- `3-Othervectorstores.ipynb`: short demos of Milvus / Weaviate / Datastax approaches.
- `PineconeVectorDB.ipynb`: Pinecone setup, indexing, and filtering by metadata.
- `Datastaxdb+(1).ipynb`: example using Datastax vector features.

## Quick checklist before production

- Choose model & chunking strategy and freeze for stable indexes
- Decide managed vs self-hosted based on budget and SLA
- Add tests to validate retrieval recall and latency
- Secure keys and rotate periodically
