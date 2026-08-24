# Sample Outputs — Desensitization Statement

The RAG offline pipeline generated the samples published in this directory. Unlike a report-style project, this system's outputs are **evaluation metrics and document chunks**, so the published "samples" are: [eval-numbers.md](eval-numbers.md) (production baseline numbers) and [chunk-examples.md](chunk-examples.md) (two chunk structure excerpts). [中文版](README_CN.md)

## Desensitization statement

- **Numbers**: system metrics only (retrieval and judge scores over a frozen golden dataset). No query text, no answer content, no internal documents.
- **Chunk excerpts**: two short fragments from *published academic papers* in the corpus, shown to illustrate the heading-tree anchoring structure. Full chunk contents are not published.
- **No internal materials**: no source code, no configuration files, no internal reports, no company names, no internal tool names, no API keys.
- **Public tech stack only**: all named tools (RAGAS, Milvus, MinerU, Langfuse, jieba/nltk, vLLM, DashScope) are public open-source or commercial services.

## What to look for

1. **The arc #7 → #11** — one month, one frozen dataset, every step a single-variable change with pre-registered judgment criteria
2. **Per-difficulty baselines** — different gates for single-hop vs. multi-hop queries, derived from measured means minus 1σ, not hand-waved
3. **Badcase attribution driving the changes** — 58 zero-score samples were triaged into retrieval failures vs. metric failures *before* any fix was attempted
4. **Chunk structure** — the `chapter`/`section` fields show the heading-tree anchor every chunk carries into retrieval

*These files were produced by the system's own evaluation runs; nothing was hand-written or fabricated for demonstration.*
