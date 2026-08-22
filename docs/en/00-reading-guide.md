# How to Read and Use This Roadmap

[中文版本](../zh-CN/00-reading-guide.md)

This repository is a **production-oriented AI Engineering curriculum**, not a list of GenAI tutorials. It starts from Andrew Ng's 2026 AI Engineering Skills Map and expands it into an execution system for becoming job-ready.

## The target capability

A qualified AI Engineer should be able to own the complete loop:

```mermaid
flowchart LR
    A[Business problem] --> B[Product / technical spec]
    B --> C[Architecture]
    C --> D[LLM / RAG / Agent implementation]
    D --> E[Evals]
    E --> F[Production deployment]
    F --> G[Tracing & monitoring]
    G --> H[Failure analysis]
    H --> I[Iteration]
    I --> E
```

The target is not “I know LangChain” or “I can call an LLM API.” The target is:

> I can turn probabilistic model behavior into a measurable, controllable, secure and maintainable software system.

## Recommended reading order

### Pass 1 — Build the mental model

1. Andrew Ng analysis
2. AI Engineer competency map
3. LLM foundations
4. Prompt & context engineering

### Pass 2 — Build AI systems

5. Grounding and RAG
6. Agentic systems
7. Evaluation-driven development

### Pass 3 — Make them production-grade

8. Production AI / LLMOps
9. ML foundations
10. Software engineering foundations
11. AI security & safety

### Pass 4 — Become an effective engineer

12. Coding agents
13. Shaping the build
14. 24-week execution plan
15. Portfolio projects
16. Interview readiness

Use resources and glossary continuously.

## Suggested weekly allocation

- **30% learning** — papers, official docs, concepts.
- **60% building** — code, experiments, evals.
- **10% writing** — architecture notes, ADRs, failure analysis.

If 80% of your time is videos and tutorials, invert the ratio.

## Three passes through every topic

**Pass A — Recognition:** understand vocabulary and architecture.

**Pass B — Construction:** implement a minimal working system without relying entirely on an orchestration framework.

**Pass C — Productionization:** add evals, observability, security, cost/latency constraints and failure handling.

## Evidence of learning

Every module should produce at least one durable artifact:

- code;
- experiment;
- eval dataset;
- benchmark;
- architecture diagram;
- ADR;
- failure-analysis note;
- deployment;
- postmortem.

## Job-ready definition

You are approaching job-readiness when you can whiteboard and implement:

> “Build an enterprise AI assistant that uses private documents and business tools.”

and proactively cover requirements, model selection, context, retrieval, tools, state, evals, safety, observability, latency, cost, rollout, rollback and feedback loops.
---

  [Andrew Ng's AI Engineering Skills Map — Detailed Analysis →](01-andrew-ng-analysis.md)
