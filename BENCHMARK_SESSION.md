# Research MCP Benchmark Session

**Query:** `feedback practices in second language writing classrooms`
**Year Filter:** 2018–2026
**Date:** 2026-05-31

---

## MCP 1: `academic_search_papers` (Academix / OpenAlex)

| Metric | Value |
|---|---|
| Papers returned | 10 |
| Papers with abstracts | 9 |
| Relevant to L2 writing feedback | 6 |
| Relevant & within 2018–2026 | 1 |
| Response size (chars) | ~8,400 |
| Primary source | OpenAlex |
| Year filter applied | **NO** — returned papers from 1991–2019 |

### Notes
- No year_from/year_to parameters available on this MCP. Query returned landmark older papers (Hyland 2006, Ferris 2010, Lee 2014) but almost nothing recent.
- One irrelevant result: Elo & Kyngäs (2008) on qualitative content analysis methodology.
- High-quality seminal papers but poor recency due to missing year filter.

### Relevant papers (within 2018–2026)
| # | Title | Year | Authors |
|---|---|---|---|
| 1 | The effect of collaborative writing in an EFL secondary setting | 2019 | Villarreal & Gil-Sarratea |

---

## MCP 2: `search_papers` (Paper-Search, multi-source)

| Metric | Value |
|---|---|
| Papers returned | 19 (deduplicated from 5 sources) |
| Papers with abstracts | 12 |
| Relevant to L2 writing feedback | 10 |
| Relevant & within 2018–2026 | 5 |
| Response size (chars) | ~14,200 |
| Sources used | arxiv (5), semantic (0), openalex (5), crossref (5), pubmed (4) |
| Year filter applied | **NO** — year_from not passed; results span 1970–2025 |

### Notes
- Broadest result set (19 papers) from 5 parallel sources.
- arXiv results were mostly off-topic (LLMs, NLP tools) — only 1 tangentially related.
- Semantic Scholar returned 0 results (API issue or no match).
- Crossref & PubMed contributed the most relevant L2 writing feedback papers.
- Some papers had empty abstracts (Crossref entries).

### Relevant papers (within 2018–2026)
| # | Title | Year | Authors | Source |
|---|---|---|---|---|
| 1 | Chinese teachers' conceptions of writing assessment and feedback practices in second language classrooms | — | Li, G. | crossref |
| 2 | Understanding teachers' written feedback practices in Hong Kong secondary classrooms | 2008 | Lee, I. | crossref |
| 3 | Student reactions to teacher feedback in two Hong Kong secondary classrooms | 2008 | Lee, I. | crossref |
| 4 | From algorithms to annotations: Rethinking feedback practices in academic writing through AI-human comparison | 2025 | Kashiha, H. | crossref |
| 5 | Teacher Written Feedback on EFL Learners' Writing: Examining Native and Nonnative Teachers' Practices | 2021 | Cheng & Zhang | pubmed |

*Note: Many results predate 2018; year filtering not enforced.*

---

## MCP 3: `research_search_literature` (Bundled Research MCP)

| Metric | Value |
|---|---|
| Papers returned | 10 |
| Papers with abstracts | 9 |
| Relevant to L2 writing feedback | 5 |
| Relevant & within 2018–2026 | 5 |
| Response size (chars) | ~9,800 |
| Sources used | Semantic Scholar, OpenAlex, arXiv, CrossRef, PubMed, Unpaywall |
| Year filter applied | **YES** (year_from=2018) |

### Notes
- Only MCP that enforced the year filter — all 10 results are 2018+.
- Highest precision: 5/10 directly relevant (50%), all within year range.
- Deduplication built in (39 raw → 10 after dedupe).
- Some off-topic results: language model training papers (Zucchet 2025, Wasi 2024, Buhnila 2024, Lin 2023, Handa 2023).
- All papers had abstracts except 1.

### Relevant papers (within 2018–2026)
| # | Title | Year | Authors |
|---|---|---|---|
| 1 | Integrated feedback as networked activity: A systematic review of multi-source feedback in ESL/EFL writing through an activity theory lens | 2026 | Guo, Zou & Zou |
| 2 | THE IMPACT OF TEACHER BEHAVIORS ON STUDENTS' WRITING JOURNEYS IN ESL CLASSROOMS | 2025 | Owusu & Debrah |
| 3 | Written corrective feedback in second language writing: A synthesis of naturalistic classroom studies | 2024 | Mao, Lee & Li |
| 4 | Translanguaging as a Mediational Tool in the Process of Feedback in Second Language Writing | 2024 | Wang & Li |
| 5 | Investigating Preparatory Year Saudi Students' Preferences Towards Different Feedback Methods | 2024 | Alhazmi |

---

## Head-to-Head Comparison

| Metric | Academix MCP | Paper-Search MCP | Research MCP |
|---|---|---|---|
| **Papers returned** | 10 | 19 | 10 |
| **With abstracts** | 9 (90%) | 12 (63%) | 9 (90%) |
| **Relevant to L2 writing feedback** | 6 | 10 | 5 |
| **Relevant & 2018–2026** | 1 (10%) | 5 (26%) | 5 (50%) |
| **Year filter enforced** | No | No | Yes |
| **Response size (chars)** | ~8,400 | ~14,200 | ~9,800 |
| **Multi-source** | No (OpenAlex only) | Yes (5 sources) | Yes (6+ sources) |
| **Deduplication** | No | Yes | Yes |
| **Abstract availability** | High | Medium | High |
| **Recency** | Poor (1991–2019) | Mixed (1970–2025) | Good (2023–2026) |
| **Precision (relevant/total)** | 60% | 53% | 50% |

---

## Verdict

| Criterion | Winner |
|---|---|
| **Best for recent literature** | Research MCP (year filter enforced, all results 2018+) |
| **Broadest coverage** | Paper-Search MCP (19 papers, 5 sources) |
| **Best abstract coverage** | Academix & Research MCP (tied at 90%) |
| **Highest relevance precision** | Academix MCP (60%), but mostly pre-2018 |
| **Best overall for this query** | **Research MCP** — only one that respected the year filter; 5/10 papers directly relevant and all within 2018–2026 |

### Key Takeaway
The **Research MCP** (`research_search_literature`) is the most reliable for filtered, recent literature searches because it actually applies the `year_from` parameter. The **Academix MCP** returns high-quality seminal work but cannot filter by year, making it poor for recency-constrained queries. The **Paper-Search MCP** casts the widest net but includes many off-topic results and doesn't enforce year filters either.

**Recommendation:** Use Research MCP as primary for targeted searches; use Academix for landmark/canonical paper discovery; use Paper-Search for breadth and cross-source validation.
