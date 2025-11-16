# 🧠 Agent RAG Cache — Mini Project (ARC-Inspired)

This project is a **hands-on implementation** inspired by the research paper  
📄 [**“Cache Mechanism for Agent RAG Systems”**](https://arxiv.org/abs/2511.02919) (Lin et al., 2025).  

It demonstrates how **smart caching** can dramatically improve the efficiency of Retrieval-Augmented Generation (RAG) systems for LLM-based agents.

---

## 🚀 Overview

Retrieval-Augmented Generation (RAG) systems combine a **retriever** (for knowledge lookup) and a **generator** (for response).  
However, constantly searching large corpora can be slow and costly.  

The paper proposes **ARC (Agent RAG Cache)** — a method for building and maintaining **small, dynamic caches** for each agent, allowing faster access to the most relevant pieces of knowledge.

This project implements a **mini version** of that idea from scratch in Python.

---

## 🧩 Features

Two cache mechanisms are implemented and compared:

| Cache Type | Description |
|-------------|--------------|
| **Baseline LRU Cache** | Keeps the most recently retrieved documents. Simple but unaware of content relevance. |
| **AURIC Cache (ARC-inspired)** | Query-aware + diversity-seeking cache that learns what each agent cares about. Uses:<br> • Exponential Moving Average (EMA) of past queries<br> • Incremental Gram-Schmidt novelty for diversity |

---

## 🧠 Architecture

### Workflow

1. **Data Loading**  
   Uses the 20 Newsgroups dataset as a sample corpus.

2. **Embeddings**  
   Generates document and query embeddings using `sentence-transformers/all-MiniLM-L6-v2`.

3. **Retrieval Simulation**  
   Each “agent” sends queries drawn from the dataset; results are retrieved and cached.

4. **Caching Strategies**  
   - *Baseline LRU:* replaces least recently used documents.  
   - *AURIC:* updates cache based on query relevance and embedding diversity.

5. **Evaluation**  
   Measures:
   - Hit rate (how often the cache already contains the needed info)
   - Median and 95th percentile retrieval latency

---

## 📊 Results Summary

### 🔹 Key Findings

- ⚡ **Speed:** Cached retrieval was up to **10× faster** than full-corpus retrieval.  
- 🎯 **Accuracy:** AURIC cache achieved **higher hit rates** than plain LRU for the same capacity.  
- 🧩 **Scalability:** Even small caches (≈1–5% of the corpus) retained strong retrieval performance.  

### 🔹 Visualization

The notebook generates two plots:

1. **Hit Rate vs Cache Capacity**  
   Shows how AURIC consistently outperforms LRU as cache size increases.

2. **Median Latency (ms)**  
   Demonstrates the speed advantage of cache-based retrieval vs. full search.

---

## 🧰 Tech Stack

| Component | Tool |
|------------|------|
| Embeddings | [sentence-transformers](https://www.sbert.net/) |
| Similarity Search | FAISS / NumPy (interchangeable) |
| Dataset | `sklearn.datasets.fetch_20newsgroups` |
| Visualization | `matplotlib`, `pandas` |
| Environment | Google Colab (Python 3.12) |

---