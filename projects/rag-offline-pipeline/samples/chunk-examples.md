# Chunk Examples — Heading-Tree Anchoring

Real chunks from the production corpus (public literature only), showing how the three-tier chunker anchors every chunk with its heading-tree path. Field names are as stored in the vector database.

## Example 1 · English (abstract, single section split)

```json
{
  "chapter": "Aging of blood can be tracked by DNA methylation changes at just three CpG sites > Abstract",
  "section": "Aging of blood can be tracked by DNA methylation changes at just three CpG sites > Abstract (part 1)",
  "chunk_size": 837,
  "content_clean": "Background: Human aging is associated with DNA methylation changes at specific sites in the genome. These epigenetic modifications may be used to track donor age for forensic analysis or to estimate biological age. Results: We perform a comprehensive analysis of methylation profiles to narrow down 102 age-related CpG sites in blood. ..."
}
```

**What this shows:** the `chapter` path records the document → section hierarchy (title tree, tier 1 of the chunker). The `section` field records that this chapter was split into parts — the split point was chosen by the LLM semantic splitter (tier 2) or, when that failed, by the rule-based fallback with overlap (tier 3).

## Example 2 · Chinese (review article, subsection heading)

```json
{
  "chapter": "Research progress in DNA methylation and aging > 1. DNA methylation and CpG islands",
  "section": "Research progress in DNA methylation and aging > 1. DNA methylation and CpG islands (part 2)",
  "chunk_size": 644,
  "content_clean": "DNA 甲基化是指生物体在 DNA 甲基转移酶 (DNA methyltransferase, Dnmts) 的催化下……"
}
```

**What this shows:** bilingual corpora are chunked with the same heading-tree scheme; language detection (Chinese-character ratio) and jieba/nltk tokenization keep Chinese and English chunks on separate, correctly-tokenized paths (for BM25) while sharing one retrieval pipeline.

*Both excerpts are from publicly released academic papers.. Only short fragments are shown; no internal documents or reports are part of the published corpus samples.*
