---
layout: page
title: Advanced Deep Learning & NLP Architectures
description: PyTorch implementations of foundational sequence models: RNNs, LSTMs, Transformers, and RAG pipelines.
img: assets/img/dl_lab_thumbnail.jpg
importance: 2
category: work
---

<style>
    @media (min-width: 1200px) { .container { max-width: 1400px !important; } }
</style>

<div class="row justify-content-center">
    <div class="col-lg-10 col-md-11" markdown="1">

**Status:** Ongoing Research & Implementation Repo | **Stack:** PyTorch, Hugging Face, LangChain, FAISS

### Motivation
Modern NLP relies heavily on abstraction layers. To master the fundamentals of Large Language Models (LLMs), I implemented core deep learning architectures from scratch in **PyTorch**. This project serves as a testbed for benchmarking attention mechanisms, sequence modeling techniques, and retrieval strategies.

---

### 1. Sequence Modeling (RNN & LSTM)
Implemented recurrent architectures to analyze the **Vanishing Gradient Problem** and long-term dependency retention.
* **RNN:** Built a vanilla RNN from scratch to process character-level text generation.
* **LSTM:** Implemented the gate mechanisms (Forget, Input, Output) manually to demonstrate superior gradient flow compared to RNNs.
* **Metric:** Compared Perplexity (PPL) on the Penn Treebank dataset.

### 2. The Transformer & Attention
Replicated the "Attention Is All You Need" architecture without using `nn.Transformer`.
* **Self-Attention:** Implemented Scaled Dot-Product Attention matrices to visualize token relationships.
* **Multi-Head Attention:** Engineered parallel attention heads to capture different linguistic subspaces.
* **Positional Encoding:** Added sinusoidal embeddings to inject sequence order into the permutation-invariant architecture.

### 3. BERT & Transfer Learning
* **Fine-Tuning:** Fine-tuned a pre-trained **BERT-base** model on the GLUE benchmark (SST-2) for sentiment analysis.
* **Optimization:** Utilized AdamW optimizer and linear learning rate schedulers to prevent catastrophic forgetting.

### 4. Retrieval-Augmented Generation (RAG)
Built a modular RAG pipeline to ground LLM responses in external data.
* **Ingestion:** Chunked PDF documents using recursive character splitters.
* **Embedding:** Generated vector embeddings using **OpenAI/HuggingFace** models.
* **Retrieval:** Implemented similarity search using **FAISS** (Facebook AI Similarity Search) to retrieve Top-K relevant contexts for the generator.

    </div>
</div>

<div class="row justify-content-center mt-5 mb-5">
    <div class="col-md-6 text-center">
        <a href="https://github.com/mihir-agarwal0211" target="_blank" class="btn btn-dark btn-lg z-depth-1">
            <i class="fab fa-github mr-2"></i> View Source Code
        </a>
    </div>
</div>