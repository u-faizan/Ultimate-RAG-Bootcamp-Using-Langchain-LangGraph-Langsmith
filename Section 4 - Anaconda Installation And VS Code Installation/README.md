# Section 4 — Anaconda & VS Code Installation

This section covers environment setup. The content below summarizes the instructor notes in `Section 4 - Anaconda Installation And VS Code Installation.txt` and adds quick commands and tips for reproducing the environment.

Summary from lecture
--------------------
- Anaconda simplifies environment and package management for Python/data science projects.
- Install Anaconda, optionally add it to PATH (recommended if you want to run `conda` from PowerShell).
- Use Anaconda Navigator to manage environments and launch Jupyter.
- Install VS Code and use it as your primary editor; you can open VS Code in a folder from the command line.
- Google Colab can be used as an alternative if local setup is difficult.

Quick reproducible steps (PowerShell on Windows)
-----------------------------------------------
1. Download & install Anaconda from the official site and follow installer steps.
2. Open PowerShell and verify conda is available:

   ```powershell
   conda --version
   ```

3. Create a dedicated environment for the course (example):

   ```powershell
   conda create -n rag-bootcamp python=3.11 -y
   conda activate rag-bootcamp
   pip install -r "c:\Users\PMYLS\Desktop\Courses\Ultimate RAG Bootcamp\requirements.txt"
   ```

4. Install VS Code from https://code.visualstudio.com/ and add the Python extension.
5. To open a folder in VS Code from PowerShell:

   ```powershell
   code "c:\Users\PMYLS\Desktop\Courses\Ultimate RAG Bootcamp"
   ```

Tips
----
- If `conda` isn’t found, either re-run the installer adding Anaconda to PATH or use Anaconda Prompt to run conda commands.
- Keep a small `environment.yml` or `requirements.txt` for reproducibility.
- If you prefer not to install locally, follow along in Google Colab (store notebooks in this repo or copy code snippets there).

Files in this folder
--------------------
- `Section 4 - Anaconda Installation And VS Code Installation.txt` — lecture notes & steps.

---
This README is a short reference to reproduce the environment used in the course.