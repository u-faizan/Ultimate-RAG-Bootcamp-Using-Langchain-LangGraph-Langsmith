# Section 7: Vector Stores and Vector Databases

This section explores vector stores and vector databases used to persist embeddings, perform efficient similarity search, and serve as the retrieval backbone for RAG systems.

## Topics covered

- Introduction to vector stores vs vector databases
- Common vector store implementations: FAISS, Chroma, Milvus, Pinecone, Weaviate
- Managed vs self-hosted trade-offs
- Index types and ANN algorithms (HNSW, IVF, PQ)
- Persistence, metadata storage, and hybrid search (sparse + dense)
- Deployment and scaling considerations

## Hands-on materials

- `1-chromadb.ipynb` — Working with Chroma (local/embedder-backed store)
- `2-faiss.ipynb` — Building and tuning FAISS indexes
- `3-Othervectorstores.ipynb` — Overview of other stores (Weaviate, Milvus, Pinecone)
- `PineconeVectorDB.ipynb` — Pinecone usage examples
- `Datastaxdb+(1).ipynb` — Datastax / vector database example
- `23-+Vector+store+vs+Vector+Databases.pdf` — Instructor slides / comparison

## Learning objectives

- Understand the role of vector stores in retrieval pipelines
- Choose between local and managed vector stores depending on use-case
- Configure and tune index parameters for speed/recall trade-offs
- Integrate vector stores with embedding pipelines and metadata stores

## Quick start (example with Chroma)

Install dependencies (recommended inside your conda/venv):

```powershell
pip install chromadb sentence-transformers faiss-cpu
```

Minimal code pattern:

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

See notebooks in this folder for full examples and parameter explanations.

## Best practices

- Persist metadata with each vector (source, chunk id, timestamp)
- Use batching when creating embeddings to avoid rate limits
- Monitor index size and reindex when embedding model or chunk strategy changes
- Combine sparse retrieval (BM25) with dense retrieval for better recall

## Notes

- Never commit API keys into notebooks. Use environment variables (e.g., `.env`) and add `.env` to `.gitignore`.
- If using managed services (Pinecone, Weaviate), ensure you rotate keys and store them securely.
