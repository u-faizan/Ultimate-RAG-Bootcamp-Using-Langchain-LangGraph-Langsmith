# Section 7: Vector Stores and Vector Databases

This section covers vector stores and vector databases used to persist embeddings, perform efficient similarity search, and serve as the retrieval backbone for RAG systems.

## Topics Covered
- Vector stores vs vector databases (conceptual differences)
- Common implementations: FAISS, Chroma, Milvus, Pinecone, Weaviate, DataStax (Astra DB)
- Managed vs self-hosted trade-offs
- Index types and ANN algorithms (HNSW, IVF, PQ)
- Persistence, metadata storage, and hybrid search (sparse + dense)
- Deployment and scaling considerations

## Notebook Index
- `1-chromadb.ipynb` — Working with Chroma (local, Python-first)
- `2-faiss.ipynb` — Building and tuning FAISS indexes
- `3-Othervectorstores.ipynb` — Overview of Milvus, Weaviate, Pinecone
- `PineconeVectorDB.ipynb` — Pinecone usage examples
- `Datastaxdb+(1).ipynb` — DataStax/Astra DB vector features
- `23-+Vector+store+vs+Vector+Databases.pdf` — Instructor slides / comparison

## Learning Objectives
- Understand the role of vector stores in retrieval pipelines
- Choose between local and managed vector stores depending on use case
- Configure and tune index parameters for speed/recall trade-offs
- Integrate vector stores with embedding pipelines and metadata stores

## Choosing a Store (Quick Guidance)
- Prototype notebooks: `Chroma` for simplicity
- Local large corpora: `FAISS` with HNSW or IVF+PQ
- Managed production: `Pinecone` for ease and scaling
- Open-source production: `Milvus` or `Weaviate` for rich features
- Part of broader DB ecosystem: `DataStax/Astra DB`

## Quick Start
Install dependencies (inside your conda/venv):

```powershell
pip install chromadb sentence-transformers faiss-cpu
```

Minimal Chroma pattern:

```python
from langchain.embeddings import HuggingFaceEmbeddings
from chromadb.config import Settings
import chromadb

client = chromadb.Client(Settings())
collection = client.create_collection("my_docs")
emb = HuggingFaceEmbeddings()
texts = ["text1", "text2"]
vectors = emb.embed_documents(texts)
collection.add(documents=texts, embeddings=vectors, metadatas=[{"source":"x"}])
```

Minimal FAISS pattern:

```python
import faiss
import numpy as np

d = 768  # embedding dimensionality
index = faiss.IndexFlatIP(d)  # or IndexFlatL2 if not normalized
vectors = np.random.randn(100, d).astype('float32')
faiss.normalize_L2(vectors)
index.add(vectors)
D, I = index.search(vectors[:1], 5)
```

See notebooks for complete examples and parameter explanations.

## Configuration Cheatsheet
- FAISS
  - `IndexFlatL2`/`IndexFlatIP` for simplicity; normalize for IP
  - IVF: choose `nlist` (clusters), tune `nprobe` for recall vs latency
  - PQ: compress vectors; tune `m` and `nbits` per subvector
- HNSW (Milvus/Weaviate)
  - `M` (graph degree), `efConstruction` (build), `efSearch` (query)
  - Increase `efSearch` for higher recall at the cost of latency
- Pinecone
  - `metric`: cosine/dotproduct/euclidean; match to embedding assumptions
  - Pod size/replicas for capacity and HA
- Chroma
  - `persist_directory` for local persistence; use metadata filters during queries

## Best Practices
- Persist metadata with each vector (source, chunk id, timestamp)
- Batch embeddings to avoid rate limits and reduce overhead
- Snapshot or export indexes; reindex when embedding model or chunking changes
- Combine sparse retrieval (BM25) with dense retrieval for better recall

## Security Notes
- Never commit API keys into notebooks; use environment variables (e.g., `.env`) and add `.env` to `.gitignore`
- If using managed services (Pinecone, Weaviate), rotate keys and store them securely

## Navigation
- Related: Section 6 (Embeddings) — `Section 6 - Vector Embedding and vector Data Bases/README.md`
- Back to root overview — `README.md`

