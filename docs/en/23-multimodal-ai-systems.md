# Multimodal AI Systems

[中文版本](../zh-CN/23-multimodal-ai-systems.md)

Modern AI applications increasingly combine text, images, documents, audio, video, and structured data. Multimodal engineering is not only “send an image to a model”; it requires modality-specific preprocessing, evaluation, latency/cost choices, and failure handling.

## Multimodal pipeline

```mermaid
flowchart LR
    I[Image / PDF / Audio / Video / Text] --> P[Parse / preprocess]
    P --> M[Multimodal model or specialist model]
    M --> S[Structured intermediate representation]
    S --> R[Reason / retrieve / tools]
    R --> O[Output]
    O --> E[Multimodal eval]
```

## 1. Documents are multimodal

PDFs may contain:

- text layers;
- tables;
- charts;
- scanned pages;
- images;
- layout information;
- headers/footnotes.

A text-only parser can silently destroy information. Learn when to use layout-aware parsing, OCR, vision models, table extraction, or a hybrid pipeline.

## 2. OCR and document extraction

Evaluate OCR separately from downstream reasoning.

Failure categories:

- missed text;
- incorrect characters/numbers;
- wrong reading order;
- table cell misalignment;
- lost page/section boundaries;
- image/chart content omitted.

If OCR is wrong, prompt tuning will not fix the missing evidence.

## 3. Vision-language models

Use vision-language models for tasks such as:

- image understanding;
- screenshot/UI interpretation;
- document page reasoning;
- chart interpretation;
- visual inspection.

Still prefer deterministic computer-vision or specialist models when they offer better accuracy, speed, or explainability for a narrow task.

## 4. Audio and speech

Typical pipeline:

`audio → speech-to-text → reasoning/tools → text/speech response`

or an end-to-end realtime multimodal model.

Engineering concerns:

- streaming and partial transcripts;
- voice activity detection;
- interruption/barge-in;
- speaker attribution;
- background noise;
- latency to first response;
- transcript privacy;
- text-to-speech quality.

## 5. Video

Video adds temporal structure and large input volume.

Common strategies:

- sample frames;
- detect scenes/shots;
- transcribe audio;
- extract metadata;
- retrieve relevant temporal segments;
- reason over selected evidence rather than the entire video.

## 6. Structured intermediate representations

For production reliability, convert multimodal inputs into typed intermediate data where possible.

Example invoice pipeline:

```text
PDF/image
→ OCR/layout extraction
→ typed invoice schema
→ deterministic validation
→ business logic / LLM reasoning
```

This is easier to test than keeping the whole workflow as opaque vision prompting.

## 7. Multimodal grounding

Grounding may combine:

- image regions;
- page coordinates;
- transcript timestamps;
- table cells;
- text chunks;
- structured records.

Citations should point to the evidence form users can verify: page, region, timestamp, source record, or document section.

## 8. Multimodal evals

Create modality-specific criteria.

Examples:

### Document extraction
- field accuracy;
- numeric exactness;
- table reconstruction;
- page attribution.

### Vision QA
- object/attribute correctness;
- spatial reasoning;
- unsupported claims.

### Speech/voice
- transcription quality;
- task completion;
- interruption handling;
- end-to-end latency.

Evaluate both intermediate stages and end-to-end task success.

## 9. Cost and latency

Images, long PDFs, audio, and video can be expensive.

Measure:

- preprocessing cost;
- model input size;
- inference latency;
- storage/bandwidth;
- cost per successful task.

Consider cascades: cheap parser/model first, expensive multimodal reasoning only when needed.

## 10. Privacy and safety

Multimodal data can contain sensitive information that text filters miss:

- faces;
- IDs;
- signatures;
- screens containing secrets;
- background speech;
- location metadata.

Redaction and retention policies must cover every modality.

## Hands-on project

Build a **Multimodal Document Analyst** that accepts mixed native/scanned PDFs with tables and charts.

Requirements:

- route pages to appropriate parser/OCR/vision path;
- create structured intermediate data;
- preserve page-level provenance;
- answer questions with page citations;
- evaluate extraction and answer quality separately;
- report latency/cost by processing path.

## Definition of Done

You can identify when text-only processing loses information; separate OCR/extraction failures from reasoning failures; design typed intermediate representations; evaluate document/vision/audio stages; preserve multimodal provenance; and make cost/latency/privacy trade-offs.

---

[← AI System Design Patterns](22-ai-system-design-patterns.md) · [AI Governance & Model Risk →](24-ai-governance-model-risk.md)
