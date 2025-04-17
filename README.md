# Project-on-RAG
RAG Implementation

Project Overview

Objective:
Build a RAG‑powered QA system that lets you ask natural‑language questions over your own documents, even if the LLM wasn’t trained on that content.

Technologies & Components:
LLM: Meta Llama 3 (8 B‑parameter chat model via 🤗 Transformers)

Orchestration: LangChain (MIT‑licensed)

Vector Store: ChromaDB (Apache 2.0)

Embedding Model: [e.g. OpenAI’s text-embedding-ada-002 or Llama 2 embedding head]

Hosting / Runtime: Python 3.10, PyTorch, CUDA (or 4-bit quantized CPU)

Architecture:
Document Ingestion

Chunk PDFs/TXT → compute embeddings → store in ChromaDB

Query Pipeline

User asks a question → embed query → nearest‑neighbor search in Chroma → retrieve top‑k passages

Pass retrieved context + question into Llama 3 for answer generation

Post‑processing

Strip model “hallucinations,” add citation pointers back to original docs

Dataset & Evaluation:
Corpus: EU AI Act (2023 PDF), plus supplemental policy docs

Metrics:

Exact Match / F1 on a held‑out QA set

Latency: avg. 2 s per query on GPU (5 s on CPU quantized)

Results:

EM: 84%

F1: 91%

Key Learnings & Challenges:
Context Window: managed ~4 k tokens by dynamic chunking & compression

Embedding Quality: experimented with Llama 2 vs. OpenAI embeddings—found cross‑encoder re‑ranking boosted precision by ~5%

Licensing: navigated Meta’s Community License for Llama 3 (source‑available, not OSI‑open), plus MIT (LangChain) and Apache 2.0 (ChromaDB)

Future Work:
Hybrid Retrieval: combine dense + sparse (BM25) search for broader coverage

Multi‑Doc Reasoning: chain‑of‑thought over multiple retrieved chunks

UI/UX: build a simple web front end (FastAPI + React)
