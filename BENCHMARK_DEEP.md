# Research MCP Deep Benchmark v2

**Date:** 2026-05-31 (rerun)
**Method:** 6 queries × 3 MCPs = 18 parallel calls
**Year Filter:** 2018–2026
**Purpose:** Can the bundled MCP replace the other two?

---

## Queries Tested

| # | Query | Focus |
|---|---|---|
| Q1 | `online writing task L2 research validity data quality comparison` | Methodology |
| Q2 | `automated writing evaluation feedback L2 second language` | AWE tools |
| Q3 | `collaborative writing peer review EFL ESL assessment` | Peer review |
| Q4 | `task-based language teaching writing development longitudinal` | TBLT |
| Q5 | `AI chatbot writing assistance academic integrity plagiarism` | GenAI/ethics |
| Q6 | `writing anxiety motivation self-efficacy second language` | Affective factors |

---

## Master Comparison

### Per-Query Results

| Query | MCP | Papers | Abstracts | Relevant | Est. Chars | Precision |
|---|---|---|---|---|---|---|
| Q1 | Academix | 10 | 9 | 3 | ~18k | 30% |
| Q1 | Paper-Search | 20 | 14 | 6 | ~28k | 30% |
| Q1 | Bundled | 10 | 10 | 4 | ~12k | 40% |
| Q2 | Academix | 10 | 7 | 8 | ~16k | 80% |
| Q2 | Paper-Search | 24 | 16 | 3 | ~32k | 13% |
| Q2 | Bundled | 10 | 10 | 8 | ~14k | 80% |
| Q3 | Academix | 10 | 8 | 1 | ~17k | 10% |
| Q3 | Paper-Search | 15 | 10 | 5 | ~20k | 33% |
| Q3 | Bundled | 10 | 10 | 5 | ~13k | 50% |
| Q4 | Academix | 10 | 9 | 2 | ~19k | 20% |
| Q4 | Paper-Search | 15 | 12 | 5 | ~22k | 33% |
| Q4 | Bundled | 10 | 10 | 6 | ~11k | 60% |
| Q5 | Academix | 10 | 9 | 6 | ~17k | 60% |
| Q5 | Paper-Search | 15 | 12 | 6 | ~22k | 40% |
| Q5 | Bundled | 10 | 10 | 4 | ~13k | 40% |
| Q6 | Academix | 10 | 9 | 5 | ~18k | 50% |
| Q6 | Paper-Search | 21 | 16 | 6 | ~28k | 29% |
| Q6 | Bundled | 10 | 10 | 6 | ~14k | 60% |

### Aggregated Stats

| Metric | Academix | Paper-Search | Bundled |
|---|---|---|---|
| **Total papers** | 60 | 100 | 60 |
| **Avg papers/query** | 10.0 | 16.7 | 10.0 |
| **Total with abstracts** | 51 | 80 | 60 |
| **Abstract rate** | 85% | 80% | **100%** |
| **Total relevant** | 25 | 31 | 33 |
| **Avg relevance/query** | 4.2 | 5.2 | **5.5** |
| **Avg precision** | 42% | 30% | **55%** |
| **Est. total chars** | ~105k | ~152k | ~77k |
| **Relevant per k-chars** | 0.24 | 0.20 | **0.43** |

---

## Verdict: Can Bundled Replace Both?

### What Bundled Does Better

| Advantage | Evidence |
|---|---|
| **Highest precision (55%)** | Beats Academix (42%) by 13pts, Paper-Search (30%) by 25pts |
| **Best token efficiency** | 0.43 relevant papers per k-chars vs 0.24 and 0.20 |
| **100% abstract coverage** | Never returns a paper without abstract |
| **Zero duplicates** | Clean deduplication built in |
| **Strongest recall (5.5/query)** | Finds more relevant papers per query than either competitor |
| **Best for TBLT (Q4)** | 60% precision vs 20% and 33% |
| **Best for affective factors (Q6)** | 60% precision vs 50% and 29% |

### What Bundled Still Loses On

| Weakness | Evidence |
|---|---|
| **No rich metadata** | No ORCID, affiliations, or citation counts (Academix excels here) |
| **Lower volume** | 10 papers/query vs Paper-Search's 16.7 |
| **Q5 (GenAI/ethics)** | Tied with Paper-Search at 40%, behind Academix at 60% |
| **Cross-database sweep** | Paper-Search queries arXiv + Semantic + OpenAlex + CrossRef + PubMed simultaneously |

### Head-to-Head: Query by Query

| Query | Winner | Bundled's Score |
|---|---|---|
| Q1 (Methodology) | **Bundled** | 40% vs 30% vs 30% |
| Q2 (AWE) | **Tie: Bundled + Academix** | 80% each |
| Q3 (Peer Review) | **Bundled** | 50% vs 33% vs 10% |
| Q4 (TBLT) | **Bundled** | 60% vs 33% vs 20% |
| Q5 (GenAI/Ethics) | **Academix** | 40% vs 60% vs 40% |
| Q6 (Affective) | **Bundled** | 60% vs 50% vs 29% |

**Bundled wins 4/6 queries outright, ties 1, loses 1.**

---

## Replacement Recommendation

### Can Bundled fully replace both?

**For discovery: YES.** Bundled finds more relevant papers per query with less noise. It wins on precision, recall, and token efficiency across 4 of 6 query types.

**For metadata enrichment: NO.** Academix provides ORCID, affiliations, citation counts, and author IDs that Bundled doesn't return. For any workflow that needs deep metadata, Academix remains necessary.

**For breadth: PARTIALLY.** Paper-Search queries 5 databases simultaneously and occasionally finds papers the others miss (especially from CrossRef niche journals). But its high noise rate (70% irrelevant) means you're paying for breadth with a lot of filtering.

### Optimal Single-MCP Workflow

```
Bundled Research (discovery + relevance filtering)
    ↓
Academix (metadata enrichment on selected papers only)
    ↓
Paper-Search (only if Bundled + Academix miss something)
```

### Can you drop Paper-Search entirely?

**Yes, for most use cases.** Paper-Search's unique contribution is CrossRef journal articles and arXiv preprints. But its 30% precision means you're filtering 70% noise. Bundled's Semantic Scholar integration covers most of the same ground with better filtering.

### Can you drop Academix entirely?

**Only if you don't need metadata.** If your workflow is just "find relevant papers," Bundled alone is sufficient. But for systematic reviews, citation analysis, or author profiling, Academix's OpenAlex metadata is irreplaceable.

---

## Final Ranking

| Rank | MCP | Score | Best For |
|---|---|---|---|
| **#1** | **Bundled Research** | 8.5/10 | Discovery, precision, efficiency |
| **#2** | **Academix** | 7.0/10 | Metadata, AWE queries, high-citation papers |
| **#3** | **Paper-Search** | 5.5/10 | Breadth, niche CrossRef coverage |

### Bottom Line

**Bundled is the clear winner for research discovery.** It can replace both MCPs for the core task of finding relevant papers. The ideal setup is Bundled-first with Academix as a metadata supplement — not three equal tools.
