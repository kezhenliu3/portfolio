# Chunk 示例 — 标题树锚点

来自生产语料的真实切块（均为公开文献），展示三级降级切分器如何为每个切块锚定标题树路径。字段名与向量库存储一致。

## 示例一 · 英文（摘要章节，同章内分段）

```json
{
  "chapter": "Aging of blood can be tracked by DNA methylation changes at just three CpG sites > Abstract",
  "section": "Aging of blood can be tracked by DNA methylation changes at just three CpG sites > Abstract（第 1 部分）",
  "chunk_size": 837,
  "content_clean": "Background: Human aging is associated with DNA methylation changes at specific sites in the genome. These epigenetic modifications may be used to track donor age for forensic analysis or to estimate biological age. Results: We perform a comprehensive analysis of methylation profiles to narrow down 102 age-related CpG sites in blood. ..."
}
```

**看什么：** `chapter` 路径记录了"文档 → 章节"层级（切分器第一级：标题树）。`section` 字段记录了该章被拆为多个部分——切分点由 LLM 语义切分（第二级）决定；LLM 失败时由带 overlap 的规则兜底（第三级）接住。

## 示例二 · 中文（综述文章，子章节标题）

```json
{
  "chapter": "Research progress in DNA methylation and aging > 1. DNA methylation and CpG islands",
  "section": "Research progress in DNA methylation and aging > 1. DNA methylation and CpG islands（第 2 部分）",
  "chunk_size": 644,
  "content_clean": "DNA 甲基化是指生物体在 DNA 甲基转移酶 (DNA methyltransferase, Dnmts) 的催化下……"
}
```

**看什么：** 中英双语料用同一套标题树方案切分；语言检测（中文字符占比）与 jieba/nltk 分词让中英文切块各走正确的分词路径（服务于 BM25），同时共用一条检索管线。

*两段摘录均出自已发表的学术论文。仅展示短片段；公开的语料样本中不含任何内部文档或报告。*
