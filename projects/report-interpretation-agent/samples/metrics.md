# Metric Tables — Retrieval Chain & Latency Breakdown

Numbers here come in **two layers**, kept strictly separate:

- **Measured / doc-backed** — recorded in development test runs or design documents during the project's lifetime.
- **Reported production figures** — as reported from production operations. **Not backed by published load-test scripts in this repository; treat as directional.** They are listed separately in the last table and are not used as design claims elsewhere.

## 1. Latency decomposition (measured)

| Path | Latency | Note |
|---|---|---|
| Rule-hit NLU (FlashText short-circuit) | ~380 ms | no LLM call on this path |
| LLM-fallback NLU | ~1.2 s | when rule matching misses |
| Slot routing, before LRU cache | ~1200 ms | extractors rebuilt per request |
| Slot routing, after LRU cache | ~600 ms | extractors cached per report type (−50%) |
| Milvus query, warm collections | ~120 ms | collections loaded in memory |
| Milvus query, cold collections | ~250 ms | collection load on first access |
| Cold start (first request, lazy singletons) | 3–5 s | one-time heavy-resource init |
| Warm path (post-boot) | ~100 ms | config already resident in memory |

*These are point measurements from development runs, not a published benchmark suite. The structural story — rule short-circuit is an order of magnitude cheaper than the LLM path, caching halves slot routing, warm collections are ~2× faster — is the takeaway.*

## 2. Retrieval & architecture numbers

| Mechanism | Value |
|---|---|
| RAG funnel width | 15 candidates (RRF-merged) → **Top-5** after cross-encoder rerank |
| RRF fusion | `1/(rank+k)` scoring, sha256 content dedup |
| Entity linking (metric track) | online candidate recall + cosine re-check, threshold 0.8 |
| Entity linking (chapter track) | startup-precomputed chapter library, cosine match, threshold 0.6 |
| KG subgraph cleanup | three-stage dedup (by kg-id → by kg-id + node type → type-routed formatting), evidence cropped to Top-3 per answer |
| DB recall | exact section match first, chapter-level fallback |
| Guardrail | forbidden words via tokenized O(1) reverse-index lookup |
| Session privacy | chat history kept in Redis with 24 h TTL, not persisted to disk |
| Concurrency | three retrieval sources dispatched via `asyncio.gather`; uvicorn 4 workers, concurrency limit 1000 |
| Connection pools | DB pool 30 + 70 overflow; graph-DB pool 50 |

## 3. Workflow → Agent evolution — test-pass counts

| Milestone | Scope | Tests |
|---|---|---|
| M0 / M1 | Pydantic `AgentContext` unified state model + entry-point factory | 6 / 12 passed |
| P0 (M3) | Executor toolification: `BaseTool`, auto-generated Function-Calling schemas from Pydantic `args_model`, `ToolRegistry`, normalized `ToolResult` | 19 passed |
| P1 | LLM Planner (function calling) behind a feature flag, with planning + execution fallback to the rule pipeline | 30 passed |
| Multi-tenant isolation | cross-tenant access rejection | 4 / 4 passed |

## 4. Reported production figures (directional)

> **The figures below are as reported from production operations (dashboards/ops). They are not backed by published load-test scripts in this repository and should be treated as directional.**

| Metric | Reported value |
|---|---|
| Daily active users (mini-program) | 10k+ |
| Throughput | hundreds of QPS |
| P99 TTFT (time to first token) | 500 ms – 2 s |
| Intent recognition accuracy | 96.3% |
| RAG Top-5 relevance | 92% |

*See the [desensitization statement](README.md) and the main [README](../README.md) for how these figures are framed.*
