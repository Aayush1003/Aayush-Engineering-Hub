# Advanced AI Concepts: Production-Grade RAG

This guide builds on the repository's introduction to retrieval-augmented generation (RAG). It focuses on how to make a retrieval system more reliable, measurable, and safe—not merely how to connect a vector database to a language model.

## 1. RAG as an evidence pipeline

A RAG system has at least two distinct quality problems:

1. **Retrieval:** Did the system find the right evidence?
2. **Generation:** Did the model answer correctly using that evidence?

A fluent response can still be wrong if retrieval missed the relevant source, selected stale content, or returned a misleading passage. Diagnose these stages separately rather than treating every bad answer as a prompt problem.

```text
Question
  → query preparation
  → retrieve candidate passages
  → rank and filter evidence
  → assemble context
  → generate an answer
  → validate support and citations
```

## 2. Hybrid retrieval

Vector search compares semantic representations, which can find paraphrases. Lexical search, such as BM25, is good at exact terms, identifiers, product names, and rare phrases. A **hybrid retriever** combines both signals.

A common design is:

1. Run lexical and vector retrieval independently.
2. Merge their candidate lists with a rank-fusion method, or normalize and combine scores.
3. Keep a manageable candidate set for reranking.

Do not assume raw scores from different search systems are directly comparable. Rank-based fusion can be a robust starting point; tune the approach against representative questions.

**Useful when:** users ask about exact error codes, acronyms, names, or a mix of conceptual and precise facts.

## 3. Reranking

Initial retrieval is optimized for recall: find a broad set of potentially relevant passages. A **reranker** then scores each question–passage pair more precisely and orders the candidates for the model's context.

This two-stage strategy can improve relevance without asking the expensive reranker to search the entire corpus. It also introduces latency and compute cost, so measure whether the gain is worth it.

## 4. Query transformation and decomposition

Users may ask ambiguous, conversational, or multi-part questions. A system can transform a query into one or more focused search queries, but transformations should preserve the original intent.

For a multi-part question, decomposition can retrieve evidence for each sub-question and then combine it. Keep the original question available during synthesis, and verify that every part is answered. Query rewriting is not a substitute for evidence; generated search terms can introduce assumptions or omit important constraints.

## 5. Chunking and context design

Chunk size is a retrieval-quality trade-off:

- **Small chunks** are focused and reduce irrelevant context, but may lose definitions or surrounding qualifications.
- **Large chunks** preserve context, but can dilute relevance and consume more of the model's context window.

Useful strategies include splitting on document structure, attaching headings and source metadata, and retrieving a focused passage together with its parent section when needed. Preserve stable source IDs and version information so that a result can be traced back to its source.

Evaluate chunking choices using the actual question set. There is no universally best chunk size or overlap setting.

## 6. Retrieval evaluation versus answer evaluation

Build a small, reviewed evaluation set before tuning. For each question, record the expected answer and the relevant source passages where possible.

### Retrieval measures

- **Recall@k:** Does the top-k result set contain the required evidence?
- **Precision@k:** How much of the retrieved set is relevant?
- **MRR or nDCG:** Are the most useful results ranked near the top?

### Answer measures

- **Correctness:** Does the answer match trusted references?
- **Groundedness:** Are factual claims supported by retrieved evidence?
- **Citation accuracy:** Do cited passages actually support the associated claims?
- **Abstention behavior:** Does the system say it lacks enough evidence when appropriate?

Automated or model-based graders can help scale checks, but they can also be wrong. Calibrate them against human-reviewed examples, inspect failures, and keep a stable test set separate from tuning examples.

## 7. Confidence and abstention

A high similarity score is not a calibrated probability that an answer is correct. Confidence depends on multiple signals, such as retrieval coverage, source quality, agreement among evidence, and whether the answer is supported.

Define a clear fallback for weak evidence: ask a clarifying question, return a limited answer with uncertainty, or state that the sources do not contain the answer. Test this behavior explicitly; a system that always answers may appear helpful while inventing unsupported details.

## 8. Freshness, provenance, and access control

A dependable knowledge system should track where each passage came from, when it was ingested, and which version it represents. Define how updates, deletions, and conflicting sources are handled. For time-sensitive information, freshness may matter as much as semantic relevance.

Apply authorization **before** exposing retrieved content to the model. Filter by the requesting user's access rights at retrieval time, and avoid relying on the model to enforce permissions. Treat document text as untrusted input: retrieved content can contain prompt-injection attempts and must not override application instructions or tool permissions.

## 9. Common failure patterns

| Symptom | Possible cause | What to inspect |
| --- | --- | --- |
| Correct source is missing | Poor chunk boundaries, weak query match, or ingestion gap | Retrieval recall, metadata filters, and source coverage |
| Relevant source ranks too low | Embedding mismatch or noisy candidate set | Hybrid search and reranking quality |
| Answer mixes unrelated facts | Too many or overlapping passages | Context selection and evidence boundaries |
| Citations exist but do not support claims | Citation generation was not validated | Claim-to-source checks and citation tests |
| Stale or unauthorized answer | Index freshness or access filter failure | Ingestion lifecycle, source versions, and authorization tests |
| Confident answer with no evidence | No abstention rule or weak grounding check | Missing-evidence tests and response policy |

## 10. A practical improvement loop

1. Save representative questions and expected source passages.
2. Measure retrieval quality before changing the generation prompt.
3. Inspect failure examples and categorize the cause: ingestion, chunking, retrieval, ranking, context, or generation.
4. Change one component at a time and rerun the same evaluation set.
5. Track latency, token usage, and cost alongside quality.
6. Add regression tests for privacy filters, prompt injection, stale content, and insufficient evidence.
7. Review a sample of real outcomes while minimizing sensitive logging.

## Advanced notes

- RAG is an application architecture, not a way to update a model's weights. It can provide relevant external evidence at inference time, but it does not guarantee truth.
- Better retrieval cannot fix incorrect or outdated source documents; data quality and provenance are part of system quality.
- More retrieved text is not automatically better. Context selection should maximize useful evidence while limiting distraction and token cost.
- A vector database is one component of the retrieval layer, not a complete knowledge or authorization system.
- For high-impact decisions, keep consequential actions outside model control and require qualified human review.

## Further reading in this repository

- [AI agents and workflows](../agents/README.md) — introductory RAG workflow, tools, safety, and evaluation.
- [AI Engineering](../engineering/README.md) — reproducibility, testing, data, and operations.
- [Transformers explained](../transformers/README.md) — model and context fundamentals.
