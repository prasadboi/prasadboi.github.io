---
title: "Fine-Tuning Llama 3.2–3B on IPCC Climate Reports"
excerpt: "Finetuning, Pretraining, and building a RAG pipeline using a Llama3.2-3B model on IPCC Climate Reports in a distributed environment"
collection: portfolio
---
**Timeframe:** Feb 2025 – Apr 2025  
**Stack:** PyTorch · Hugging Face (Transformers, PEFT) · Nanotron · vLLM · Milvus · LangChain · Singularity · SLURM · A100 GPUs

## TL;DR

I fine‑tuned LLaMA‑3B on IPCC climate reports with aggressive memory optimizations (QLoRA + BF16 + gradient checkpointing), then scaled training across 2×A100 using data, tensor, and pipeline parallelism. Finally, I benchmarked a RAG system against the fine‑tuned model on climate‑domain queries.

**Highlights**

- 4‑bit quantization + BF16 + LoRA *(r=8, α=32)* with gradient checkpointing enabled micro‑batch **32** on a single A100.
- Distributed training across **2×A100** combined DP/TP/PP to **halve epoch time (337 → 169 min)** and cut per‑GPU memory by **~48%**.
- End‑to‑end packaging: modular Trainer + SLURM workflows for **QLoRA** and **multi‑GPU** runs; evaluated **perplexity** and **RAG time‑per‑request**.

## Problem & Dataset

Climate literature updates faster than general‑purpose LLMs adapt. I curated a corpus of **IPCC reports and recent climate/AI publications (past ~5 years)** from PDFs, extracted/cleaned text, and split 90/10 for train/test. The goal: produce a stronger climate‑domain model and compare it to a retrieval‑augmented setup.

## Approach

### (1) Memory‑Efficient Fine‑Tuning (Single‑GPU)

- **QLoRA**: 4‑bit quantization with LoRA adapters *(r=8, α=32)*
- **Mixed precision**: BF16 for speed/stability
- **Gradient accumulation & checkpointing** to increase effective batch size
- **Outcome**: micro‑batch 32 on a single A100 while maintaining training stability

### (2) Multi‑GPU Scaling (2×A100)

- **Data Parallelism (DP)** to shard batches
- **Tensor Parallelism (TP)** to split large weight matrices
- **Pipeline Parallelism (PP)** to place layer stages on separate GPUs with micro‑batching
- **Outcome**: **~2× throughput** (337 → 169 min per epoch) and **~48%** per‑GPU memory reduction

### (3) Retrieval‑Augmented Generation (RAG)

- **Indexing**: chunked documents (200–400 tokens), embeddings, vector DB (Milvus/FAISS)
- **Retrieval**: top‑k ANN search (HNSW / IVF‑PQ) + optional reranking
- **Generation**: combine retrieved context with the query and pass to LLM
- **Metric**: average **time per request** and qualitative answer comparison vs fine‑tuned LLaMA‑3B

## Results

**Training**

- **Perplexity (QLoRA single‑GPU):** 7.996  
- **Perplexity (multi‑GPU runs):** 14.36–22.97 (early‑stoped comparative runs under heavier parallelism)
- **Epoch time:** 337 → **169** minutes (2×A100, DP+TP+PP)
- **Memory:** **~48%** reduction per GPU from baseline

**Inference (RAG)**

- Lower **time‑per‑request** variance on knowledge‑dense queries
- Improved factual grounding on climate‑specific prompts with explicit citations to retrieved text

## Engineering & Reproducibility

- **Trainer scripts**: modular configs for PEFT/quantization/precision and parallel modes (DP/TP/PP)
- **SLURM jobs**: easy submit templates for single‑GPU QLoRA and multi‑GPU distributed runs
- **Containers**: Singularity images for reproducible environments on HPC
- **Logging/Eval**: perplexity on held‑out 10%; latency collection for RAG vs fine‑tuned

<!-- 
## What I’d Improve Next

- Deeper **TP/PP** partitioning heuristics for transformer blocks to smooth bubbles
- **Reranker** tuning (cross‑encoder) for harder retrieval sets
- Automated **data quality** checks and continual‑learning pipeline

--- -->

## Short Code/Config Sketch (illustrative)

```bash
# Single‑GPU QLoRA
sbatch jobs/qlora_single_a100.SBATCH   --config configs/qlora_llama3b_ipcc.yaml

# 2×A100 DP+TP+PP
sbatch jobs/dist_2x_a100.SBATCH   --config configs/distributed_llama3b_dp_tp_pp.yaml

# RAG
python rag/index.py --conf configs/rag_ipcc.yaml
python rag/serve.py --conf configs/rag_ipcc.yaml
```
