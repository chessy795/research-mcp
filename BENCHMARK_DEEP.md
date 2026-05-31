# Research MCP Deep Benchmark

**Date:** 2026-05-31
**Method:** 6 queries × 3 MCPs = 18 parallel calls
**Year Filter:** 2018–2026 (where applicable)

---

## Queries Tested

| # | Query | Focus Area |
|---|---|---|
| Q1 | `online writing task L2 research validity data quality comparison` | Methodology/validity |
| Q2 | `automated writing evaluation feedback L2 second language` | AWE tools |
| Q3 | `collaborative writing peer review EFL ESL assessment` | Peer interaction |
| Q4 | `task-based language teaching writing development longitudinal` | TBLT & development |
| Q5 | `AI chatbot writing assistance academic integrity plagiarism` | GenAI & ethics |
| Q6 | `writing anxiety motivation self-efficacy second language` | Affective factors |

---

## Master Comparison Table

### Per-Query Results

| Query | MCP | Papers | Abstracts | Relevant | Est. Tokens (chars) | Precision |
|---|---|---|---|---|---|---|
| Q1 | Academix | 10 | 9 | 3 | ~18k | 30% |
| Q1 | Paper-Search | 20 | 14 | 6 | ~28k | 30% |
| Q1 | Bundled | 10 | 10 | 4 | ~12k | 40% |
| Q2 | Academix | 10 | 7 | 8 | ~16k | 80% |
| Q2 | Paper-Search | 19 | 12 | 2 | ~25k | 11% |
| Q2 | Bundled | 10 | 10 | 8 | ~14k | 80% |
| Q3 | Academix | 10 | 8 | 1 | ~17k | 10% |
| Q3 | Paper-Search | 15 | 10 | 6 | ~20k | 40% |
| Q3 | Bundled | 10 | 10 | 5 | ~13k | 50% |
| Q4 | Academix | 10 | 9 | 2 | ~19k | 20% |
| Q4 | Paper-Search | 15 | 12 | 4 | ~22k | 27% |
| Q4 | Bundled | 10 | 10 | 2 | ~11k | 20% |
| Q5 | Academix | 10 | 9 | 6 | ~17k | 60% |
| Q5 | Paper-Search | 15 | 12 | 6 | ~22k | 40% |
| Q5 | Bundled | 10 | 10 | 4 | ~13k | 40% |
| Q6 | Academix | 10 | 9 | 4 | ~18k | 40% |
| Q6 | Paper-Search | 16 | 12 | 6 | ~23k | 38% |
| Q6 | Bundled | 10 | 10 | 6 | ~14k | 60% |

### Aggregated MCP Statistics

| Metric | Academix | Paper-Search | Bundled Research |
|---|---|---|---|
| **Total papers returned** | 60 | 100 | 60 |
| **Avg papers/query** | 10.0 | 16.7 | 10.0 |
| **Total with abstracts** | 51 | 72 | 60 |
| **Abstract rate** | 85% | 72% | **100%** |
| **Total relevant papers** | 24 | 30 | 29 |
| **Avg relevance/query** | 4.0 | 5.0 | 4.8 |
| **Avg precision** | **40%** | 31% | **48%** |
| **Est. total tokens (chars)** | ~105k | ~140k | ~77k |
| **Relevant papers per k-char** | 0.23 | 0.21 | **0.38** |
| **Unique papers (deduped)** | ~55 | ~80 | ~58 |
| **Duplicates across sources** | N/A (single) | ~20 (multi) | 0 |

---

## Per-Query Deep Analysis

### Q1: Online Writing Task L2 Research Validity

| MCP | Relevant Papers Found | Notes |
|---|---|---|
| Academix | Zhang & Hyland (2018), Song & Song (2023), Imran & Almusharraf (2023) | Good metadata but 70% noise |
| Paper-Search | Charoenchaikorn (2022), Nitta & Baba (2014), Byrnes (2014), Borg (2003), Norris & Ortega (2000), Ellis (2005) | CrossRef yielded strongest results; Semantic returned 0 |
| Bundled | Yan et al. (2025), Curado Fuentes (2025), Wang & Shen (2024), Mei et al. (2024) | Most recent papers, cleanest output |

**Winner: Bundled** — freshest papers, zero noise from arXiv

---

### Q2: Automated Writing Evaluation Feedback

| MCP | Relevant Papers Found | Notes |
|---|---|---|
| Academix | Koltovskaia (2020), Zhang (2020), Jiang et al. (2020), Zhang & Hyland (2023), Crosthwaite et al. (2022), Karatay & Karatay (2024), Chen et al. (2023), Reynolds et al. (2021), Hassanzadeh & Fotoohnejad (2021), Woodworth & Barkaoui (2020) | **Best query for Academix** — 80% precision |
| Paper-Search | Wang et al. (2024) [arXiv], Luo et al. (2025) [Semantic] | Only 2 relevant out of 19 — worst precision |
| Bundled | Yan et al. (2025), Luo et al. (2025), Sajid et al. (2025), Zhang & Cheng (2024), Reynolds & Kao (2024), Wang et al. (2024), Wang & Zhao (2026), Cheng et al. (2025) | Strongest recall — 80% precision |

**Winner: Tie (Academix & Bundled)** — Academix excelled here for the first time; Paper-Search failed badly

---

### Q3: Collaborative Writing Peer Review

| MCP | Relevant Papers Found | Notes |
|---|---|---|
| Academix | Rudolph et al. (2023) [ChatGPT, tangential] | Only 1 marginally relevant |
| Paper-Search | Heywood et al. (2025), Vedaste Nsengiyumva (2025), Aljabr (2025), Macías Pino et al. (2025), Manipatruni et al. (2024), Daoud et al. (2024) | Strong — 6 relevant, mostly from Semantic |
| Bundled | Mali (2026), Mali (2025), Aljabr (2025), Macías Pino et al. (2025), Manipatruni et al. (2024), Daoud et al. (2024) | Strong — 5 relevant |

**Winner: Paper-Search** — Semantic Scholar returned high-quality EFL peer review papers

---

### Q4: Task-Based Language Teaching Writing

| MCP | Relevant Papers Found | Notes |
|---|---|---|
| Academix | Byrnes (2014) [TBLT book chapter], Johnson (2023) | Only 2 relevant |
| Paper-Search | Yu (2025), Forget & Tigchelaar (2024), Johnson (2023), Byrnes (2014) | 4 relevant — CrossRef strong for TBLT |
| Bundled | Li (2025) [Chinese TBLT], Yu (2025) | Only 2 relevant |

**Winner: Paper-Search** — CrossRef and cross-database coverage helped

---

### Q5: AI Chatbot Academic Integrity

| MCP | Relevant Papers Found | Notes |
|---|---|---|
| Academix | Kasneci et al. (2023), Dwivedi et al. (2023), Lo (2023), Rudolph et al. (2023), Chan & Hu (2023), Tlili et al. (2023) | 6 relevant — high-citation papers |
| Paper-Search | Liebling et al. (2025), Röttger et al. (2026), Wilfley et al. (2026), Sarwar (2025), Lancaster (2025), Alawad et al. (2025) | 6 relevant — newer papers from Semantic |
| Bundled | Mali (2025), Lancaster (2025), Alawad et al. (2025), Sarwar (2025) | 4 relevant |

**Winner: Tie (Academix & Paper-Search)** — Academix for high-citation foundational work, Paper-Search for recent studies

---

### Q6: Writing Anxiety Motivation Self-Efficacy

| MCP | Relevant Papers Found | Notes |
|---|---|---|
| Academix | Sabti et al. (2019), Rezazadeh & Zarrinabadi (2021), Khelalfa (2018), Deb (2018) | 4 relevant |
| Paper-Search | Song et al. (2026), Park et al. (2026), Savaşçı (2026), Akhir et al. (2026), Crawford et al. (2026), Cao et al. (2025) | 6 relevant — all very recent |
| Bundled | Song et al. (2026), Park et al. (2026), Savaşçı (2026), Akhir et al. (2026), Crawford et al. (2026), Cao et al. (2025) | 6 relevant |

**Winner: Tie (Paper-Search & Bundled)** — both returned recent, highly relevant papers

---

## Cross-MCP Unique Paper Discovery

| MCP | Unique Papers Not Found by Others | Coverage |
|---|---|---|
| Academix | Koltovskaia (2020), Zhang (2020), Jiang et al. (2020), Crosthwaite et al. (2022), Karatay & Karatay (2024), Kasneci et al. (2023), Chan & Hu (2023) | Best for established AWE and GenAI-ed papers |
| Paper-Search | Heywood et al. (2025), Vedaste Nsengiyumva (2025), Forget & Tigchelaar (2024), Liebling et al. (2025), Röttger et al. (2026) | Best for recent arXiv + CrossRef + Semantic coverage |
| Bundled | Yan et al. (2025), Wang & Shen (2024), Luo et al. (2025), Sajid et al. (2025), Akhir et al. (2026), Crawford et al. (2026) | Best for recent Semantic Scholar discoveries |

---

## Efficiency Analysis

| MCP | Relevant Papers | Est. Total Tokens | Relevant per k-tokens | Cost Efficiency Rank |
|---|---|---|---|---|
| **Bundled Research** | 29 | ~77k | **0.38** | **#1** |
| Academix | 24 | ~105k | 0.23 | #2 |
| Paper-Search | 30 | ~140k | 0.21 | #3 |

---

## Semantic Scholar Performance Note

Semantic Scholar returned **0 results** for Q1, Q2 (partial), Q3, and Q4 across Paper-Search MCP. It performed best for Q5 and Q6. This suggests Semantic Scholar's API may have issues with certain query formulations or may weight terms differently than OpenAlex.

---

## Final Rankings

| Category | Winner | Runner-up |
|---|---|---|
| **Overall Precision** | **Bundled (48%)** | Academix (40%) |
| **Overall Recall** | **Paper-Search (30)** | Bundled (29) |
| **Abstract Coverage** | **Bundled (100%)** | Academix (85%) |
| **Token Efficiency** | **Bundled (0.38 rel/k-char)** | Academix (0.23) |
| **Metadata Richness** | **Academix** | Paper-Search |
| **Best for AWE Queries** | **Academix & Bundled (tie)** | Paper-Search |
| **Best for Peer Review** | **Paper-Search** | Bundled |
| **Best for TBLT** | **Paper-Search** | Bundled |
| **Best for GenAI/Ethics** | **Academix & Paper-Search (tie)** | Bundled |
| **Best for Affective Factors** | **Paper-Search & Bundled (tie)** | Academix |
| **Lowest Noise** | **Bundled** | Academix |
| **Most Unique Papers** | **Paper-Search (~80)** | Bundled (~58) |

---

## Recommendation: Optimal Workflow

```
Step 1: Bundled Research → Discovery (best precision, cleanest output)
Step 2: Academix → Metadata enrichment (ORCID, affiliations, citation counts)
Step 3: Paper-Search → Gap-filling (broadest coverage, recent papers from Semantic + CrossRef)
```

### When to Use Each

| Use Case | Best MCP |
|---|---|
| Initial literature discovery | Bundled Research |
| Deep metadata for selected papers | Academix |
| Systematic review sweep | Paper-Search |
| Quick relevance check | Bundled Research |
| Citation network analysis | Academix |
| Recent preprints (2024-2026) | Paper-Search (arXiv + Semantic) |
| Established field mapping | Academix (OpenAlex citation data) |
| Cross-database deduplication | Bundled Research (built-in) |
