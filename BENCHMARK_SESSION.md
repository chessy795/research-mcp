# Research MCP Benchmark Session

**Date:** 2026-05-31
**Query:** `online writing task L2 research validity data quality comparison`
**Year Filter:** 2018–2026

---

## Comparison Table

| Metric | Academix (OpenAlex) | Paper-Search (Multi-Source) | Bundled Research |
|---|---|---|---|
| **Papers Returned** | 10 | 15 | 10 |
| **Sources Queried** | OpenAlex only | arxiv, semantic, openalex, crossref, pubmed | arXiv, Semantic Scholar, OpenAlex, CrossRef, PubMed, Unpaywall |
| **Papers with Abstracts** | 9 / 10 (90%) | 12 / 15 (80%) | 10 / 10 (100%) |
| **Relevant to L2 Writing Research** | 3 / 10 (30%) | 7 / 15 (47%) | 4 / 10 (40%) |
| **Duplicates Across Sources** | N/A (single source) | 2 peer-review entries + 2 arXiv duplicates from OpenAlex | 0 |
| **Unique L2 Writing Papers** | 3 | 5 | 4 |
| **Includes Citations** | Yes (725, 2224, etc.) | Yes (mixed) | Yes (6, 1, 17) |
| **Includes DOI** | Yes (all) | Yes (most) | Yes (most) |
| **Includes PDF URL** | Yes (all) | Yes (most) | Yes (all) |

---

## Detailed Results per MCP

### 1. Academix (`academix_academic_search_papers`)

**Strengths:**
- Clean structured output with full metadata (ORCID, affiliations, citation counts)
- Single-source consistency (OpenAlex) means no cross-source deduplication noise
- Rich author metadata (ORCID, affiliations, author IDs)

**Weaknesses:**
- Query returned many off-topic papers (PINNs, reading rate meta-analysis, data leakage in ML)
- Semantic keyword matching is weak — "data quality" and "comparison" triggered broad results
- Only 3/10 papers actually relevant to L2 writing research methodology

**Relevant Papers Found:**
1. Zhang & Hyland (2018) — Student engagement with teacher and automated feedback on L2 writing
2. Song & Song (2023) — ChatGPT efficacy for EFL writing skills
3. Imran & Almusharraf (2023) — ChatGPT as writing assistant at higher education level

**Off-topic Noise:** Physics-Informed Neural Networks, reading rate meta-analysis, ML reproducibility crisis, dark energy constraints

---

### 2. Paper-Search (`paper-search_search_papers`)

**Strengths:**
- Multi-source aggregation covers more ground (5 sources)
- CrossRef yielded highly relevant L2 writing papers (Byrnes, Nitta & Baba, Charoenchaikorn)
- Semantic Scholar returned zero results for this query (gap)

**Weaknesses:**
- 5 arXiv papers were completely irrelevant (remote sensing, Byzantine fault tolerance, dark energy)
- 2 CrossRef entries were peer-review records (no content)
- High noise from non-CS/non-education sources bleeding in
- Semantic Scholar returned 0 results (API issue or query mismatch)

**Relevant Papers Found:**
1. Borg (2003) — Teacher cognition in language teaching [via OpenAlex]
2. Norris & Ortega (2000) — Effectiveness of L2 Instruction: meta-analysis [via OpenAlex]
3. Ellis (2005) — Measuring Implicit and Explicit Knowledge of L2 [via OpenAlex]
4. Byrnes (2014) — Theorizing language development at intersection of task and L2 writing [via CrossRef]
5. Nitta & Baba (2014) — Task repetition and L2 writing development [via CrossRef]
6. Charoenchaikorn (2022) — Effects of Post-Task Anticipation during Online Collaborative Writing in L2 [via CrossRef]

**Note:** Many OpenAlex results in this MCP overlap with what Academix would return (same underlying database).

---

### 3. Bundled Research (`research_search_literature`)

**Strengths:**
- 100% abstract coverage (10/10)
- Better semantic relevance — most papers touch L2 writing or related methodology
- Deduplication across sources is clean (0 duplicates in output)
- Auto-expansion of queries helps find relevant work
- Citation walk feature available (not triggered in benchmark)

**Weaknesses:**
- Still returned 3 irrelevant papers (TerraGen, Alzheimer's handwriting, Small Data Explainer)
- Some papers are very recent (2024-2025) with low citation counts — may lack validation
- No raw source attribution per paper (hard to tell which database each came from)

**Relevant Papers Found:**
1. Yan, Jia & Tian (2025) — Automated feedback + peer feedback for L2 writers
2. Curado Fuentes (2025) — GenAI and BDDL for academic L2 writing in tourism
3. Wang & Shen (2024) — QSRLWS questionnaire for EFL learners
4. Mei, Ma, Tang & Zou (2024) — Collaborative writing in online distance learning

---

## Relevance Ranking (L2 Writing Research Methodology Focus)

| Rank | Paper | Source MCP | Year |
|---|---|---|---|
| 1 | Yan, Jia & Tian — Automated feedback + peer feedback | Bundled | 2025 |
| 2 | Wang & Shen — QSRLWS validation | Bundled | 2024 |
| 3 | Zhang & Hyland — Student engagement with feedback on L2 writing | Academix | 2018 |
| 4 | Mei et al. — Collaborative writing in online distance learning | Bundled | 2024 |
| 5 | Charoenchaikorn — Post-task anticipation in online collaborative writing | Paper-Search | 2022 |
| 6 | Song & Song — ChatGPT for EFL writing skills | Academix | 2023 |
| 7 | Imran & Almusharraf — ChatGPT as writing assistant | Academix | 2023 |
| 8 | Curado Fuentes — GenAI + BDDL for L2 writing | Bundled | 2025 |
| 9 | Nitta & Baba — Task repetition and L2 writing | Paper-Search | 2014 |
| 10 | Norris & Ortega — Effectiveness of L2 instruction (meta-analysis) | Paper-Search | 2000 |

---

## Verdict

| Category | Winner | Notes |
|---|---|---|
| **Raw Volume** | Paper-Search | 15 papers, but highest noise |
| **Abstract Coverage** | Bundled Research | 100% abstracts |
| **Relevance Precision** | Bundled Research | 40% relevant, cleanest output |
| **Relevance Recall** | Paper-Search | Found 7 relevant papers (highest count) |
| **Metadata Richness** | Academix | ORCID, affiliations, citation counts per paper |
| **Cross-Source Coverage** | Paper-Search | 5 sources queried (but Semantic returned 0) |
| **Deduplication Quality** | Bundled Research | Zero duplicates in output |
| **Overall Best for This Query** | **Bundled Research** | Best precision-to-noise ratio; Academix is best for metadata depth |

### Recommendation
- Use **Bundled Research** for initial literature discovery (best relevance, cleanest output)
- Use **Academix** for deep metadata enrichment (author info, citation networks)
- Use **Paper-Search** for broad cross-database sweeps (accept higher noise)
- Best workflow: Bundled Research → Academix metadata → Paper-Search for gap-filling
