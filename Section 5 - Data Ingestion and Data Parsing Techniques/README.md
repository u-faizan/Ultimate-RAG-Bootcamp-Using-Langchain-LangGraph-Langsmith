# Section 5 — Data Ingestion & Data Parsing Techniques

This section contains practical notebooks and data used to extract and parse different file types for RAG systems. The folder `0-DataIngestParsing` contains the main notebooks and a `data/` folder with examples.

Notebooks (found in `0-DataIngestParsing`)
------------------------------------------
- `1-dataingestion.ipynb` — data ingestion overview and text splitters (there is also a `1-dataingestion notes(text splitters).pdf`).
- `2-dataparsingpdf.ipynb` — parsing PDF files and extracting text.
- `3-dataparsingdoc.ipynb` — parsing Word / doc files.
- `4-csvexcelparsing.ipynb` — parsing CSV and Excel files.
- `5-jsonparsing.ipynb` — parsing JSON and JSONL files.
- `6-databaseparsing.ipynb` — ingesting data from relational databases.
- `rag-architecture-diagram.svg` and `1-langchain-document-components.svg` — helpful diagrams.

Data folder
-----------
- `data/` contains subfolders such as `json_files/`, `pdf/`, `structured_files/`, `text_files/`, and `word_files/`.
  - Important example files: `json_files/company_data.json`, `json_files/events.jsonl`, `structured_files/products.csv`, `text_files/machine_learning.txt`, `text_files/python_intro.txt`, `word_files/proposal.txt`.

How to run the notebooks
------------------------
- Activate your course environment, then open Jupyter or VS Code and run the notebooks in order.
- Example environment commands (PowerShell):

  ```powershell
  conda activate rag-bootcamp
  jupyter notebook "c:\Users\PMYLS\Desktop\Courses\Ultimate RAG Bootcamp\Section 5 - Data Ingestion and Data Parsing Techniques\0-DataIngestParsing\1-dataingestion.ipynb"
  ```

Notes & recommended additions
-----------------------------
- Add a `README-run.md` or a small `requirements.txt` in `0-DataIngestParsing` with precise package versions used by the notebooks.
- For larger files, add notes on chunking parameters and tokenization behavior (useful for later tuning retrieval).
- Keep a quick reference for each loader: API used, critical args, and common errors.

---
This README points to the lab notebooks and data used for parsing content which will later feed your RAG pipelines.