# 📖 Project on RAG  
_Retrieval-Augmented Generation (RAG) Implementation_

![Python](https://img.shields.io/badge/python-3.10-blue.svg)  
![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?logo=PyTorch&logoColor=white)  
![LangChain](https://img.shields.io/badge/LangChain-MIT-green)  
![ChromaDB](https://img.shields.io/badge/ChromaDB-Apache%202.0-orange)  
![Meta Llama 3](https://img.shields.io/badge/Meta-Llama%203-9cf)  

---

## 📌 Overview  

This project implements a **Retrieval-Augmented Generation (RAG)** QA system.  
It enables users to ask natural-language questions over custom documents (e.g., PDFs, TXT) even if the LLM was not trained on that content.  

---

## ⚙️ Technologies & Components  

- **LLM**: Meta Llama 3 (8B-parameter chat model via Transformers)  
- **Orchestration**: [LangChain](https://www.langchain.com/) (MIT-licensed)  
- **Vector Store**: [ChromaDB](https://www.trychroma.com/) (Apache 2.0)  
- **Embeddings**: OpenAI `text-embedding-ada-002` *or* Llama 2 embedding head  
- **Runtime**: Python 3.10, PyTorch, CUDA (GPU) or 4-bit quantized CPU  

---

## 🏗️ Architecture  

### 1. Document Ingestion  
- Chunk PDFs/TXT files  
- Compute embeddings  
- Store embeddings in **ChromaDB**  

### 2. Query Pipeline  
1. User submits a natural-language query  
2. Query is embedded  
3. Perform nearest-neighbor search in ChromaDB  
4. Retrieve top-k passages  
5. Context + query passed into **Llama 3** for generation  

### 3. Post-Processing  
- Minimize hallucinations  
- Add citations to original documents  

---

## 📂 Dataset & Evaluation  

- **Corpus**: EU AI Act (2023 PDF) + supplemental policy docs  
- **Metrics**:  
  - Exact Match (EM)  
  - F1 Score  
  - Latency (avg. 2s/query on GPU, ~5s on quantized CPU)  

---

## 📊 Results  

- **Exact Match (EM):** 84%  
- **F1 Score:** 91%  
- **Latency:** ~2s (GPU), ~5s (CPU)  

---

## 🔑 Key Learnings & Challenges  

- **Context Window:** Managed ~4k tokens with dynamic chunking & compression  
- **Embedding Quality:** Cross-encoder re-ranking improved precision by ~5%  
- **Licensing:**  
  - Meta Llama 3 → Community License (source-available, not OSI-open)  
  - LangChain → MIT  
  - ChromaDB → Apache 2.0  

---

## 🚀 Future Work  

- Hybrid Retrieval: Dense + sparse (BM25) search  
- Multi-Doc Reasoning: Chain-of-thought across multiple retrieved chunks  
- UI/UX: Web front end (FastAPI + React)  

---

## 🔧 Installation  

```bash
# Clone the repo
git clone https://github.com/your-username/project-on-rag.git
cd project-on-rag

# Create a virtual environment
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Ingest documents
python ingest.py --docs ./data/eu_ai_act.pdf

# Run query
python query.py --question "What are the obligations of providers under the EU AI Act?"

