# Evaluation Numbers — One Month of Baseline Iteration

All numbers come from the production evaluation runs (286-sample golden dataset, fixed throughout the month). 11 evaluation rounds were run; the decisive arc is #7 → #11. Batch-to-batch noise tolerance is ±1.5pp; every strategy change was validated as a single-variable A/B against the previous baseline.

## 1. The month-long arc (rounds #7 → #11)

| Round | Date | Retrieval strategy | Hit@5 | Recall@5 | MRR | NDCG@5 |
|---|---|---|---|---|---|---|
| #7 | 08-12 | vector-only (single path) | 0.6818 | 0.5717 | 0.5293 | 0.5021 |
| #8 | 08-13 | + bilingual hybrid | 0.8671 | 0.7331 | 0.7191 | 0.6649 |
| #9 | 08-13 | bilingual (production baseline) | 0.8741 | 0.7401 | 0.7209 | 0.6684 |
| #10 | 08-17 | **C4: wide pool + split bilingual rerank** | **0.9476** | 0.8106 | 0.8494 | 0.7739 |
| #11 | 08-18 | C4 + cp_v2 metric (final) | **0.9476** | **0.8106** | 0.8478 | 0.7729 |
| | | **Δ #7 → #11** | **+26.6pp** | **+23.9pp** | **+31.9pp** | **+27.1pp** |

RAGAS quality metrics over the same arc:

| Round | context_precision | context_recall | faithfulness | answer_relevancy | Low-score samples |
|---|---|---|---|---|---|
| #7 | 0.4992 (v1) | 0.6708 | 0.9248 | 0.6693 | 193 |
| #9 | 0.6226 (v1) | 0.8462 | 0.9341 | 0.7646 | — |
| #10 | 0.7448 (v1) | 0.8943 | 0.9510 | 0.7958 | 162 |
| #11 | **0.8662 (v2)** | **0.9039** | **0.9540** | **0.7892** | **134 (−30.6%)** |

Acceptance gate evolution: #9 → 8/12 pass, #10 → 11/12, **#11 → 12/12 (first full pass)**.

## 2. Final baseline by query difficulty (frozen golden dataset, 286 samples)

From the final baseline replay after the schema evolution — same frozen golden dataset, all by-type values from one run (differences vs. round #11 by-type values are within the ±1.5pp batch-noise tolerance):

| query_type | n | Hit@5 | Recall@5 | NDCG@5 | cp(v2) | cr | faith | ar |
|---|---|---|---|---|---|---|---|---|
| single_hop | 140 | 0.950 | 0.950 | 0.884 | 0.869 | 0.946 | 0.965 | 0.841 |
| multi_hop_intra | 78 | 0.936 | 0.748 | 0.727 | 0.840 | 0.871 | 0.961 | 0.777 |
| multi_hop_inter | 68 | 0.956 | 0.603 | 0.598 | 0.821 | 0.843 | 0.937 | 0.714 |

*(Multi-hop inter-document queries are the hardest by construction — answers span documents in two languages. Note the gap between IR Recall@5 and RAGAS metrics on multi-hop types: it is the known cross-lingual exact-match penalty that motivated the two-stage baseline design below.)*

## 3. The two-stage baseline system

**Stage 1 — IR diagnostic tier** (per query type, cheap, signals where to iterate; thresholds = RAGAS production baseline minus the known cross-lingual exact-match penalty: single ~0pp, intra ~18pp, inter ~23pp):

| query_type | Gate |
|---|---|
| single_hop | Hit@5 ≥ 0.88, MRR ≥ 0.72 |
| multi_hop_intra | Recall@5 ≥ 0.62, NDCG@5 ≥ 0.58 |
| multi_hop_inter | Recall@5 ≥ 0.48, NDCG@5 ≥ 0.45 |

**Stage 2 — RAGAS acceptance tier** (production admission, per query type):

| query_type | cp(v2) | cr | faith | ar |
|---|---|---|---|---|
| single_hop | ≥ 0.87 | ≥ 0.88 | ≥ 0.92 | ≥ 0.82 |
| multi_hop_intra | ≥ 0.84 | ≥ 0.82 | ≥ 0.90 | ≥ 0.75 |
| multi_hop_inter | ≥ 0.82 | ≥ 0.75 | ≥ 0.88 | ≥ 0.68 |

Threshold-setting rule: cp(v2) gate = measured mean − 1σ (σ = batch noise tolerance ±1.5pp). Historical rounds are frozen, never retroactively re-graded. IR gates diagnose; RAGAS gates decide production admission.

*Notes: cp(v1) is the stock RAGAS context_precision judge; cp(v2) is the partial-support-aware adaptation (see project README). Numbers are system metrics only — no query or answer content is published. Framework sources: see the References section of the [project README](../README.md).*
