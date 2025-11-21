Supporting Slides : https://drive.google.com/file/d/1qpNFqwqAxoT4GlagkSzypOahW1EL3niZ/view?usp=drive_link

Supporting Video : https://www.loom.com/share/ec4364888ef8479a8fc4afa7918c5857

# PSTB Bootcamp - Hackathon 2 - 20/21 November 2025

## Team: YC Dynamics (Yacine Fares, Clément Philbert)

---

## 🚀 Project Name

📄 AI-Powered Document Search & Summarization System

---

## 📝 Summary of the Project

> **Objective**: Build an AI-driven tool to ingest documents, perform semantic search, and generate concise summaries of relevant sections

This project was developed during a 2-day hackathon by the **YC Dynamics** team (Yacine Fares, Clément Philbert).

The goal was to build a **Retrieval-Augmented Generation (RAG)** system capable of supporting the main features described in the next section.

**To challenge ourselves** we decided to go beyond the provided instructions and implemented an LLM output on top of the baseline BART model. This allowed us to research and select a relevant model that would work locally on CPU and have a deeper understanding of parameters fine-tuning.

---

## ✅ Main Features

-   Upload multiple documents (PDF, TXT, DOCX)
-   Extract and clean text
-   Split documents into chunks
-   Generate embeddings and index them in FAISS
-   Perform semantic search
-   Display top retrieved passages with similarity scores
-   Summarize using:
    -   Baseline: BART-base
    -   Advanced: TinyLlama LLM
-   Polished Streamlit UI

---

## 🔄 High-Level Project Workflow

                 ┌──────────────────────────┐
                 │        Upload Files      │
                 └──────────────┬───────────┘
                                ▼
                 ┌──────────────────────────┐
                 │     Text Extraction      │
                 │     (PDF/TXT/DOCX)       │
                 └──────────────┬───────────┘
                                ▼
                 ┌──────────────────────────┐
                 │     Text Preprocessing   │
                 │  (cleaning, splitting)   │
                 └──────────────┬───────────┘
                                ▼
                 ┌──────────────────────────┐
                 │       Embedding          │
                 │ (all-MiniLM-L6-v2 model) │
                 └──────────────┬───────────┘
                                ▼
                 ┌──────────────────────────┐
                 │     Vector Index (FAISS) │
                 └──────────────┬───────────┘
                                ▼
                 ┌──────────────────────────┐
                 │   Semantic Search Query  │
                 └──────────────┬───────────┘
                                ▼
         ┌────────────────────────────────────────────────────┐
         │                                                    │
         │   Summaries (Baseline BART + TinyLlama LLM(bonus)) │
         │                                                    │
         └────────────────────────────────────────────────────┘

---

## 🧰 Tech Stack

| Component      | Technology                               |
| -------------- | ---------------------------------------- |
| UI             | Streamlit                                |
| Extraction     | PyPDF / python-docx                      |
| Embeddings     | all-MiniLM-L6-v2 (Sentence Transformers) |
| Vector Search  | FAISS (CPU)                              |
| Summarization  | BART-base / TinyLlama Open Source LLM    |
| Programming    | Python Version 3.10.13 (via pyenv)       |

---

## 📁 Project Structure

```
hackathon2/
├── README.md
├── requirements.txt
├── .gitignore
├── app.py                     # Main Streamlit app (entry point)
│
├── src/
│   ├── __init__.py
│   ├── config.py              # Global constants (chunk sizes, model names, etc.)
│   │
│   ├── ingestion/
│   │   ├── __init__.py
│   │   ├── extractors.py      # PDF, TXT, DOCX extraction
│   │   └── chunking.py        # Text splitting & cleaning
│   │
│   ├── indexing/
│   │   ├── __init__.py
│   │   ├── embeddings.py      # SentenceTransformer wrapper
│   │   └── vector_store.py    # FAISS index wrapper (add/search)
│   │
│   ├── summarization/
│   │   ├── __init__.py
│   │   ├── baseline_summarizer.py  # BART-base summarizer
│   │   └── llm_summarizer.py       # Open Source LLM QA/summarizer (TinyLlama LLM -> added bonus for the project)
│   │
│   ├── evaluation/
│       ├── __init__.py
│       ├── search_metrics.py   # precision@k, recall@k (functions to compute metrics -> optional for the project)
│       └── summary_metrics.py  # ROUGE etc. (functions to compute metrics -> optional for the project)
│
├── data/
│   ├── examples/               # Example DOCX/TXTs for demos
```

---

## 📦 Environment Setup (Reproducibility)

This project uses Python 3.10.13 and a pinned requirements.txt available in the repository to facilitate the reproducibility of the project.

---

## 🛠️ How to Run the App

### Install the correct Python version via pyenv

    pyenv install 3.10.13
    pyenv local 3.10.13

### Create a virtual environment

    python -m venv .venv
    source .venv/bin/activate

### Install dependencies

    pip install -r requirements.txt

### Run app

    streamlit run app.py

> The app should open in your default browser at: http://localhost:8501

---

## 🎯 General Conclusion

Over the course of this 2-day hackathon, we designed and built a fully functional **Retrieval-Augmented Generation (RAG)** system that works entirely **locally on CPU** and supports multiple document types (DOCX, TXT, PDF).

We successfully implemented the complete pipeline: ingestion, text preprocessing, semantic embeddings, FAISS-based retrieval, and two levels of summarization (baseline BART and an the TinyLlama open-source LLM). The initial "summarization" code was using the Phi-3-mini-4k-instruc model, but we did not used it for the final code due to significant local memory management issues it generated on CPU.

Beyond meeting the original requirements, we challenged ourselves to explore model selection, latency constraints, and parameters testing. By doing so, we delivered a polished, intuitive Streamlit interface and gained hands-on understanding of the trade-offs between **precision, chunking strategy, semantic search, and open-source LLM usage.**

We are proud to present a proof of concept that is:

- **Robust** (handles multi-format files)

- **Explainable** (shows retrieved chunks and similarity scores)

- **Extendable** (ready for reranking or GPU LLMs)

- **User-friendly** (clean UI and reproducible environment setup)

This project demonstrates our ability to build production-ready AI components under tight time constraints and showcases how classical NLP, vector search, and lightweight LLMs can work together to extract meaningful insights from unstructured documents.