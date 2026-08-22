# Grounding、Retrieval 与 RAG

[English version](../en/05-grounding-rag.md)

## 标准 pipeline

```mermaid
flowchart LR
    D[Documents] --> P[Parse]
    P --> C[Chunk]
    C --> E[Embed / index]
    E --> Q[Retrieve]
    Q --> RR[Rerank]
    RR --> X[Construct context]
    X --> L[LLM]
    L --> A[Answer + citations]
```

## Ingestion
生产系统必须处理：

- document identity；
- metadata；
- versioning；
- deduplication；
- timestamp；
- ACL；
- update；
- delete。

**“We indexed the docs once.” 不是 production data strategy。**

## Chunking
需要比较：

- fixed-token；
- paragraph；
- section-aware；
- semantic；
- parent-child chunking。

不要靠网上流传的“500 tokens 最佳”这类经验决定，应该通过 retrieval eval 选择。

## Retrieval
必须掌握：

- dense / vector retrieval；
- sparse / BM25；
- hybrid search；
- metadata filter；
- query rewriting；
- multi-query retrieval。

## Reranking
常见架构：

`retrieve top-N candidates → rerank → select evidence → construct context`

retrieval quality 与 final answer quality 要分层评估。

## 三层 Eval

```mermaid
flowchart TB
    R1[Retrieval eval<br/>Did we find the evidence?]
    R2[Generation eval<br/>Did the model use it correctly?]
    R3[End-to-end eval<br/>Did the user task succeed?]
    R1 --> R2 --> R3
```

指标可以包括：

- Recall@K；
- Precision@K；
- MRR / NDCG；
- correctness；
- faithfulness；
- completeness；
- citation accuracy。

## RAG vs Long Context vs Fine-Tuning

**RAG**：知识动态、private、大规模，需要 citation / ACL。

**Long context**：corpus 不大，一次性分析，整体文档关系很重要。

**Fine-tuning**：主要改变 behavior / style / task pattern，而不是默认拿来“记事实”。

## Security
必须把 retrieved content 当成 **untrusted data**，防：

- prompt injection；
- data leakage；
- cross-tenant exposure；
- ACL bypass。

## Project
实现 Enterprise Knowledge Assistant：

- hybrid retrieval；
- reranker；
- citations；
- incremental indexing；
- ACL filtering；
- tracing；
- 至少 100 条 evaluation questions。

## 如何学习本章

不要采用“看完课程 = 学会了”的方式。使用下面这个工程闭环：

```mermaid
flowchart LR
    A[Learn 学概念] --> B[Implement 做最小实现]
    B --> C[Measure 量化行为]
    C --> D[Break 用 edge cases 主动打坏]
    D --> E[Diagnose 做 failure analysis]
    E --> F[Improve 一次只改关键变量]
    F --> G[Document 记录 trade-offs]
    G --> C
```

判断本章是否学完，不是看你是否“听说过”术语，而是看你能否 **build it, measure it, debug it, and explain the trade-offs**。中文学习过程中务必保留常见英文表达，因为真实代码库、设计文档、面试和工程讨论通常直接使用这些术语。
---

[← Prompt & Context Engineering：提示词与上下文工程](04-prompt-context-engineering.md)  ·  [Agentic Systems Engineering：智能体系统工程 →](06-agentic-systems.md)
