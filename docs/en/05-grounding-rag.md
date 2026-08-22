# Grounding, Retrieval and RAG

[中文版本](../zh-CN/05-grounding-rag.md)

## Canonical pipeline

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
Handle identity, metadata, versioning, deduplication, timestamps, ACLs, updates and deletes. “We indexed the docs once” is not a production data strategy.

## Chunking
Compare fixed-token, paragraph, section-aware, semantic and parent-child chunking. Choose with retrieval evals rather than folklore.

## Retrieval
Learn dense/vector retrieval, sparse/BM25 retrieval, hybrid search, metadata filters, query rewriting and multi-query retrieval.

## Reranking
A common architecture retrieves a broad candidate set and then reranks it before context assembly. Measure retrieval and downstream answer quality separately.

## Evaluation layers

```mermaid
flowchart TB
    R1[Retrieval eval<br/>Did we find the evidence?]
    R2[Generation eval<br/>Did the model use it correctly?]
    R3[End-to-end eval<br/>Did the user task succeed?]
    R1 --> R2 --> R3
```

Metrics can include Recall@K, Precision@K, MRR/NDCG, correctness, faithfulness, completeness and citation accuracy.

## RAG vs long context vs fine-tuning

Use RAG when knowledge is dynamic/private/large and citations or ACLs matter.

Use long context when the corpus is small enough and global document relationships matter.

Use fine-tuning primarily to alter behavior or task patterns, not as the default method to “store facts.”

## Security
Retrieved content is untrusted data. Design for prompt injection, data leakage, tenant isolation and ACL-aware retrieval.

## Project
Build an Enterprise Knowledge Assistant with hybrid retrieval, reranking, citations, incremental indexing, ACL filtering, traceability and at least 100 evaluation questions.

## How to study this chapter

Use the loop below instead of passive reading:

```mermaid
flowchart LR
    A[Learn the concept] --> B[Implement a minimal version]
    B --> C[Measure behavior]
    C --> D[Break it with edge cases]
    D --> E[Diagnose failures]
    E --> F[Improve one variable]
    F --> G[Document the trade-off]
    G --> C
```

A chapter is **not complete** when you recognize the terminology. It is complete when you can build, measure, debug, and explain the relevant system without hiding behind a framework name.
---

[← Prompt & Context Engineering](04-prompt-context-engineering.md)  ·  [Agentic Systems Engineering →](06-agentic-systems.md)
