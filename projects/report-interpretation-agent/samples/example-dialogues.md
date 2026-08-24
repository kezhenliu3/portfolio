# Example Dialogues — Illustrative Transcripts

> **These transcripts are rewritten illustrations of the system's documented behavior branches**, produced for sanitization and clarity. They are **not real user conversations** and **not verbatim system output**. Every question, value, and metric is fictional or simplified; paper titles cited are real publications that illustrate the citation format.

---

### Branch 1 · `metric_explain` — normal path (KG retrieval)

**Question (illustrative):** "My blood-clock report says my serum albumin is on the low side — what does that mean?"

**Pipeline:** rule-based slot extraction matches the metric and a report section → intent `metric_explain` → entity linking resolves "albumin" to a knowledge-graph node → the DM plans a KG query → the subgraph is recalled, three-stage deduplicated, and evidence cropped to the Top-3 sources → NLG streams the answer with forced source traces.

**Answer excerpt (rewritten):**

> Albumin reflects liver synthesis capacity and nutritional status. Your value sits in the lower part of the reference range. In the context of your report, the system-level picture (liver and inflammation status) is the more informative signal — single markers are read together with it.
>
> Clinical significance: … / Interventions: … / Reference range: …

**Sources shown:** paper titles with links (e.g., the CSPPT folic-acid study — *JAMA*, 2015), plus the report chapter the analysis drew from.

---

### Branch 2 · `no_metric_explain` — honest fallback (anti-hallucination)

**Question (illustrative):** "My report mentions serum trefoil factor 3 — should I worry?"

**Pipeline:** the rule layer matches a metric name, but entity linking finds **no knowledge-graph node** for it → the intent converges `metric_explain` → `no_metric_explain` *before any generation*. This is the architectural answer to "don't know, say so" — it happens in intent handling, not in a prompt.

**Answer excerpt (rewritten):**

> This marker isn't covered by our knowledge base yet, so I can't offer a sourced explanation for it. I can explain the organ system it relates to, or you may bring this up with your physician.

**Sources shown:** none. The system reports that it found nothing instead of inventing a reference.

---

### Branch 3 · `report_summary` (DB chapter recall)

**Question (illustrative):** "Summarize my report."

**Pipeline:** intent `report_summary` → the DB executor recalls the structured report content by section (exact section match first, chapter-level fallback second) → NLG composes a summary anchored to chapters.

**Answer excerpt (rewritten):**

> Your biological age is 26.7 years against a calendar age of 24 — aging slightly faster than peers. By system: immune status is relatively stronger (81st percentile), liver function is at the lower end… A full breakdown follows by chapter.

**Sources shown:** report chapter names (e.g., "Health management — healthy diet").

---

### Branch 4 · `clarification` — asking instead of guessing

**Question (illustrative):** "Is my value high?" — no report attached, no metric named.

**Pipeline:** slot sufficiency fails (no kg-id, no chapter/section) → the DM returns a clarification action → no retrieval, no generation happens.

**Answer excerpt (rewritten):**

> Which metric would you like me to check? Attaching your report also lets me compare values against your own reference ranges.

---

### Branch 5 · guest mode (report-state convergence)

**Question (illustrative, visitor without a report):** "How accurate is the blood clock?"

**Pipeline:** no `report_id` → the intent converges to a product-knowledge popularization intent → retrieval is RAG-only within guest scope → the answer carries a scope-limitation note.

**Answer excerpt (rewritten):**

> The blood clock estimates biological age from routine blood markers using an algorithm that integrates hematology, biochemistry, and immune data… This is general product information — attach your report for a personal interpretation.

**Sources shown:** knowledge-base document IDs.

---

*Each branch above corresponds to a documented code path; the texts are rewritten for illustration and contain no real user data.*
