# RAG Document Q&A — Hybrid Search Pipeline

A retrieval-augmented generation system built from scratch (no LangChain)
that lets you upload PDFs and ask questions in plain English, with
page-level citations on every answer.

## What makes it different

Most RAG tutorials use pure vector search. This pipeline implements
**hybrid BM25 + vector search** fused with **Reciprocal Rank Fusion (RRF)**
— catching both semantic matches and exact keyword matches that vector
search alone misses.

## Pipeline

**Indexing:**
PDF upload → chunking → embeddings → ChromaDB (persisted)

**Querying:**
User question → BM25 search ──┐
             → vector search ──┴→ RRF merge → Llama 3 → answer + citations


## Features

- Multi-PDF upload and ingestion
- Hybrid BM25 + vector retrieval with RRF re-ranking
- Page-level citations on every answer — filename and page number
- Conversation memory — ask follow-up questions naturally
- Anti-hallucination prompt — says "not found" instead of making things up
- Built without LangChain — pure chromadb, groq, sentence-transformers

## Stack

Python · ChromaDB · Sentence Transformers · Groq (Llama 3.1) · BM25 · pypdf

## Run it yourself

Open in Colab:  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aryan-narang/rag-document-qa/blob/main/rag-document-qa.ipynb)

1. Add your Groq API key (free at console.groq.com)
2. Upload your PDFs
3. Start asking questions

