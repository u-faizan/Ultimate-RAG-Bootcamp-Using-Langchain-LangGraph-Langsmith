# Embeddings - Notes

## Overview

Embeddings map textual content into fixed-length numerical vectors that capture semantic meaning. In RAG systems, embeddings are used to index and retrieve relevant document chunks for building context windows for LLM prompts.

## Key Concepts

- Vector space: similar text sits nearby in the vector space
- Dimensionality: common sizes 512, 768, 1024, 1536 — higher dimensions can capture more nuance but cost more memory and compute
- Similarity metrics: cosine similarity and dot product are the most used
- Normalization: L2-normalizing vectors when using cosine similarity can simplify comparison

## Embedding Models

- OpenAI embeddings (production-ready, managed)
- SentenceTransformers (local, many pre-trained models)
- MiniLM, MPNet, and larger transformer models for higher-quality embeddings
- Newer multi-modal or instruction-tuned embedders as needed

## Practical Guidance

1. Preprocessing
   - Clean text, remove long boilerplate, normalize whitespace
   - Decide chunk size before embedding (typically 500–1500 tokens per chunk)

2. Batching and throughput
   - Batch requests to remote APIs to reduce latency
   - For large corpora, embed in parallel and persist intermediate results

3. Storing embeddings
   - Use an efficient vectorstore (FAISS, Chroma, Milvus, Pinecone) with metadata
   - Store original text, chunk ids, source, and offset in metadata

4. Indexing and search
   - For large datasets, use approximate nearest neighbor (ANN) indexes
   - Tune index parameters (ef/construction, nlist, nprobe) for balance of speed and recall

5. Similarity scoring and reranking
   - Retrieve top-K using vector similarity
   - Optionally rerank top candidates with cross-encoders or LLM scoring

## Sample Code (OpenAI embeddings)

```python
from openai import OpenAI
from langchain.embeddings import OpenAIEmbeddings

texts = ["first text chunk", "second chunk"]
embedder = OpenAIEmbeddings(model="text-embedding-3-small")
vectors = embedder.embed_documents(texts)
```

## Notebook summaries

- `embedding.ipynb`: Demonstrates generating embeddings with local transformer models and visualizing vector distances.
- `openaiembeddings.ipynb`: Shows how to call OpenAI's embeddings API, batch requests, and store vectors in a vectorstore.
- `18-Embeddings.pdf`: Instructor slides covering embedding theory and practical recommendations.

## Best Practices

- Recompute embeddings when document content or the embedding model changes
- Keep embeddings and source text synchronized with versioning or timestamps
- Monitor embedding dimensionality, storage cost, and retrieval latency

## Pitfalls

- Mixing embedding models without reindexing
- Using overly large chunks that dilute semantic signal
- Forgetting to preserve metadata required for provenance and display

## Next steps

- Integrate embeddings into your retrieval pipeline (vectorstore + retriever)
- Evaluate embeddings quality using retrieval recall/precision and downstream LLM answer quality
