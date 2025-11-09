# Ultimate RAG Bootcamp Using LangChain

This repository contains my learning journey and notes from the Ultimate RAG (Retrieval Augmented Generation) Bootcamp course. The course covers everything from basic RAG concepts to advanced implementation techniques using LangChain.

## Course Structure

### Section 1: Introduction
Introduction to the course structure and RAG concepts. See `Section 1 - Intro/notes.md` for detailed notes.

### Section 2: Introduction to RAG
Core RAG concepts including:
- Retriever + Reader pattern
- Chunking and ingestion strategies
- Embedding-based search
- Hybrid retrieval approaches
- Vectorstore selection
See `Section 2 - Introduction to RAG/notes.md` for comprehensive notes and examples.

### Section 3: Core Components in RAG
A consolidated view of the RAG building blocks:
- Document loaders and stores
- Chunking and text splitting strategies
- Embeddings: model choices and tradeoffs
- Vector stores and retrievers (hybrid strategies)
- Prompt templates and orchestration (LangChain, LangGraph)
- Evaluation and metrics
See `Section 3 - Core Components in RAG/notes.md` for details.

### Section 4: Development Environment Setup
Step-by-step guide for setting up the development environment:
- Anaconda installation and configuration
- VS Code setup and extensions
- Environment management
- Troubleshooting guide
See `Section 4 - Anaconda Installation And VS Code Installation/notes.md` for installation instructions and best practices.

### Section 5: Data Ingestion and Parsing
Comprehensive coverage of data handling techniques:
- Text, PDF, and Word document processing
- CSV and Excel file parsing
- JSON and structured data handling
- Database integration
- Best practices for data preprocessing

Practical examples are provided in the `/0-DataIngestParsing` folder with sample data in the `/data` directory.
See `Section 5 - Data Ingestion and Data Parsing Techniques/notes.md` for detailed implementation notes.

### Section 6: Embeddings
Focused coverage of vector embeddings and how to generate and use them in RAG systems:
- Embedding fundamentals and intuition
- OpenAI and local embedding models
- Dimensionality trade-offs and indexing strategies
- Batching, normalization, and performance tips

Hands-on materials: `Section 6 - Vector Embedding and vector Data Bases/embedding.ipynb`, `Section 6 - Vector Embedding and vector Data Bases/openaiembeddings.ipynb`, and `Section 6 - Vector Embedding and vector Data Bases/18-Embeddings.pdf`.
See `Section 6 - Vector Embedding and vector Data Bases/notes.md` for implementation notes and best practices.

### Section 7: Vector Stores and Vector Databases
Vector stores vs vector databases; implementations, trade-offs, and tuning:
- FAISS, Chroma, Milvus, Pinecone, Weaviate, DataStax
- ANN index types (HNSW, IVF, PQ) and parameters
- Persistence, metadata storage, hybrid retrieval
- Hands-on notebooks: Chroma, FAISS, Pinecone, others
See `Section 7 - Vector Stores and Vector Data Bases/notes.md` and `README.md` in that folder.

## Repository Structure

Each section follows a consistent structure:
- `README.md`: Section overview and key concepts
- `notes.md`: Detailed notes and implementation details
- Additional resources (code examples, diagrams, etc.)

## Note Organization

- Each section has its own directory with a focused `notes.md` file
- Code examples and practical implementations are included where relevant
- Reference materials and diagrams are preserved for future use

## Sections Coming Soon
- Additional sections to be added as the course progresses

## Resources

- Sample data files in Section 5's data directory
- Jupyter notebooks with practical examples
- Implementation templates and best practices

---
*Note: This README will be updated as additional sections are completed.*

## Getting Started

- New here? Read the quick recall guide: `notes.md` in the repo root.
- Want details per lecture? Open the section folders (e.g., `Section 1 - Intro/notes.md`, `Section 2 - Introduction to RAG/notes.md`).
