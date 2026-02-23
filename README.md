# Corrective Retrieval Augmented Generation (CRAG) Implementation

This repository implements concepts and techniques from the paper  
**“Corrective Retrieval Augmented Generation”** (*arXiv:2401.15884*) by Shi-Qi Yan, Jia-Chen Gu, Yun Zhu, and Zhen-Hua Ling.:contentReference[oaicite:0]{index=0}

## 🔍 Paper Summary

The CRAG paper proposes enhancements to the standard Retrieval-Augmented Generation (RAG) framework to make it more robust when retrieval goes wrong. The key ideas in the paper include:

1. **Retrieval Quality Evaluation**  
   A lightweight *retrieval evaluator* is trained to assess the relevance of retrieved documents and assign a confidence score.:contentReference[oaicite:1]{index=1}

2. **Corrective Retrieval Actions**  
   Based on evaluator confidence, the system triggers different actions:
   - *Correct* — refine retrieved documents
   - *Incorrect* — discard retrieval and fall back to external sources
   - *Ambiguous* — combine both internal and external knowledge for generation:contentReference[oaicite:2]{index=2}

3. **Web Search as Complementary Knowledge**  
   When retrieval is unreliable, external web search results are incorporated to augment or replace the original retrieval.:contentReference[oaicite:3]{index=3}

4. **Decompose-Then-Recompose Refinement**  
   Retrieved documents are segmented into smaller knowledge strips, scored, filtered, and recomposed to enrich the final context used in generation.:contentReference[oaicite:4]{index=4}

---

## 🧠 What Was Implemented

In this project, the following CRAG concepts were incorporated:

- **Retrieval Confidence Scoring**  
  We implement a lightweight evaluator to determine retrieval quality and decide which corrective action to perform.

- **Corrective Strategies**
  - *Correct Action*: refine the retrieved corpus based on evaluator scores.
  - *Fallback to External Retrieval*: call web search or large corpora when retrieval is judged incorrect.
  - *Combined Strategy*: support ambiguous cases by merging internal and external knowledge.

- **Knowledge Refinement**
  Decompose retrieved documents into smaller factual segments and recombine the most relevant ones for generation.

---

## 🛠 Architecture Overview

```text
Input Query
    ↓
Retriever → Retrieved Docs
    ↓
Retrieval Evaluator
    ↓
Confidence Score ──────────────┐
    ↓                         ↓
Correct  → Knowledge Refinement
                    ↓
Incorrect → External Search → Refined Data
                    ↓
Ambiguous → Combine Internal & External
    ↓
LLM Generator → Output
