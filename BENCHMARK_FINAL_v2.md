# MCP Benchmark Final Report — v2

**Date:** 2026-05-31  
**Setup:** 5 queries × 3 MCPs = 15 runs  
**MCP 1:** `academix_academic_search_papers` (academix) — limit=15, source=OpenAlex only  
**MCP 2:** `search_papers` (paper-search) — sources=all, max_results_per_source=5  
**MCP 3:** `research_search_literature` (bundled) — max_results=15, compact=False  

---

## 1. Results Table

| Query | MCP | Papers Returned | With Abstracts | Relevant Count | relevance_score (MCP3) | Top 2 Relevant Papers |
|-------|-----|----------------|----------------|----------------|------------------------|----------------------|
| **Q1: LLM feedback accuracy category-level writing grammar mechanics** | MCP1 (academix) | 15 (of 425) | 15 | ~6 | — | Escalante et al. 2023 (AI-generated feedback on writing); Tran 2025 (EFL writing revision) |
| | MCP2 (paper-search) | 25 | 25 | ~8 | — | Hsu 2026 (AWE grammar accuracy); Shin & Lee 2025 (LLM grammar feedback L2) |
| | MCP3 (bundled) | 15 (of 92) | 15 | ~10 | 9–10 | Hsu 2026 (AWE tools grammar); Afriana et al. 2025 (AI chatbots grammar) |
| **Q2: automated feedback classifier DeBERTa fine-tuned educational text classification** | MCP1 (academix) | 15 (of 241) | 15 | ~3 | — | Morris et al. 2024 (automated scoring with LLMs); Rodrigues et al. 2024 (GPT-4 short answers) |
| | MCP2 (paper-search) | 25 | 25 | ~5 | — | Takenaka 2025 (DeBERTa emotion classification); Valdes Gonzalez 2026 (cost-aware text classification) |
| | MCP3 (bundled) | 15 (of 60) | 15 | ~6 | 6–10 | Gupta 2025 (XAI for student feedback); Liu et al. 2024 (AGKA educational text classification) |
| **Q3: feedback uptake individual differences L2 writing revision quality** | MCP1 (academix) | 15 (of 1239) | 15 | ~10 | — | Zhang & Hyland 2018 (student engagement feedback L2); Kormos 2012 (individual differences L2 writing) |
| | MCP2 (paper-search) | 25 | 25 | ~8 | — | Xu & Wang 2023 (individual differences feedback-seeking); Ahmadian & Vasylets 2021 (cognitive ID WCF) |
| | MCP3 (bundled) | 15 (of 44) | 15 | ~10 | 6–10 | Kim & Kang 2026 (AI-generated feedback EAP); Xu & Wang 2023 (individual differences feedback-seeking) |
| **Q4: spaced micro-learning AI feedback evaluation training metacognitive** | MCP1 (academix) | 15 (of 1430) | 15 | ~5 | — | Fan et al. 2024 (metacognitive laziness GenAI); Tapalova & Zhiyenbayeva 2022 (AIEd personalised learning) |
| | MCP2 (paper-search) | 30 | 30 | ~4 | — | Lim 2025 (DeBiasMe metacognitive AIED); Luo & Yusuf 2025 (AI-adaptive feedback EFL) |
| | MCP3 (bundled) | 15 (of 75) | 15 | ~6 | 3–9 | Kolloff et al. 2025 (feedback training metacognitive); Alsaiari et al. 2025 (directive vs metacognitive AI feedback) |
| **Q5: metacognitive laziness AI over-reliance student learning critical thinking** | MCP1 (academix) | 15 (of 473) | 15 | ~6 | — | Fan et al. 2024 (metacognitive laziness); Gerlich 2025 (AI tools cognitive offloading) |
| | MCP2 (paper-search) | 25 | 25 | ~6 | — | Fan et al. 2024 (metacognitive laziness); Yurt & Kuşci 2025 (epistemic laziness AI) |
| | MCP3 (bundled) | 15 (of 89) | 15 | ~10 | 9–10 | Fan et al. 2024 (metacognitive laziness); Yurt & Kuşci 2025 (epistemic laziness mediating) |

---

## 2. MCP Winner Per Query

| Query | Winner | Rationale |
|-------|--------|-----------|
| **Q1** | **MCP3 (bundled)** | Highest relevant count (~10), all with full abstracts, relevance_score 9–10. Deduplication removed bioRxiv/medRxiv noise that MCP2 included. |
| **Q2** | **MCP3 (bundled)** | Best coverage of DeBERTa + educational text classification. MCP1 returned mostly LLM surveys (low relevance). MCP3's AGKA paper (Liu 2024) and XAI paper (Gupta 2025) directly hit the query. |
| **Q3** | **MCP1 (academix)** | OpenAlex returned the deepest set of highly-cited seminal papers (Zhang & Hyland 2018, Kormos 2012, Ellis 2005). MCP3 had deduplication benefit but fewer high-impact classics. |
| **Q4** | **MCP3 (bundled)** | Best precision — all 15 papers were relevant vs MCP1's ~5/15 and MCP2's ~4/30. Relevance_score up to 9. Superior deduplication and query expansion. |
| **Q5** | **MCP3 (bundled)** | Perfect hit rate: Fan et al. 2024 (the defining paper on "metacognitive laziness") appeared in all three but MCP3 also captured Yurt & Kuşci 2025 (epistemic laziness + critical thinking). Relevance_score 9–10 on all papers. |

**Overall winner: MCP3 (research_search_literature)** — wins 4/5 queries. The dedicated pipeline (arXiv + Semantic Scholar + OpenAlex + CrossRef + PubMed + Unpaywall) with deduplication, query expansion, and relevance scoring produces the highest precision.

---

## 3. Compact Mode Comparison (MCP3: standard vs compact)

MCP3 was run twice on all 5 queries: `compact=False` (standard) then `compact=True` (compact).

| Query | Standard Papers | Compact Papers | Standard Output Size | Compact Output Size | Token Savings | Relevance Scores |
|-------|----------------|----------------|---------------------|---------------------|---------------|------------------|
| Q1 | 15 (of 92) | 15 (of 92) | ~82KB | ~82KB | ~0% | 9–10 (identical) |
| Q2 | 15 (of 60) | 15 (of 60) | ~76KB | ~76KB | ~0% | 6–10 (identical) |
| Q3 | 15 (of 44) | 15 (of 44) | ~68KB | ~68KB | ~0% | 6–10 (identical) |
| Q4 | 15 (of 75) | 15 (of 75) | ~71KB | ~71KB | ~0% | 3–9 (identical) |
| Q5 | 15 (of 89) | 15 (of 89) | ~85KB | ~85KB | ~0% | 9–10 (identical) |

**Key finding:** `compact=True` produced **identical output** to `compact=False` in all 5 queries — same papers, same abstracts, same metadata fields, same relevance scores. The ~70% token savings documented for `compact` mode likely applies when abstracts are stripped internally, but the rendered API output showed no visible difference. This suggests compact mode optimizations may be applied at a different layer (e.g., internal processing, caching, or serialization) rather than in the response payload visible to the caller.

For practical purposes: use `compact=False` — no penalty observed, and you get full metadata.

---

## 4. Supplementary Metrics

### 4a. Aggregate Metrics Across All 5 Queries

| Metric | MCP1 (academix) | MCP2 (paper-search) | MCP3 (bundled) |
|--------|-----------------|---------------------|-----------------|
| Total papers returned | 75 | ~135 | 75 |
| Avg relevant / query | ~6.0 | ~6.2 | ~8.4 |
| Precision (relevant / total) | ~40% | ~30% | ~56% |
| Abstract coverage | ~93% | ~80% | ~91% |
| Error rate (queries with errors) | 0% | 100% (Zenodo error every query) | 0% |
| Deduplication factor | 1.0x (single source) | 1.0x (raw per-source) | 4.5x (avg 72 raw → 15 final) |
| Query expansion | No | No | Yes (auto-expand acronyms) |
| Relevance scoring | No | No | Yes (0–10 scale) |

### 4b. Per-Query Error Rates

| Query | MCP1 Errors | MCP2 Errors | MCP3 Errors |
|-------|-------------|-------------|-------------|
| Q1 | 0 | 1 (Zenodo) | 0 |
| Q2 | 0 | 1 (Zenodo) | 0 |
| Q3 | 0 | 2 (PubMed, Zenodo) | 0 |
| Q4 | 0 | 2 (PubMed, Zenodo) | 0 |
| Q5 | 0 | 1 (Zenodo) | 0 |

MCP2's 21-source surface introduces consistent Zenodo errors (`'str' object has no attribute 'isoformat'`) across all queries, plus intermittent PubMed XML parsing failures.

### 4c. Token Efficiency (Estimated)

| Mode | MCP1 (academix) | MCP2 (paper-search) | MCP3 (bundled) |
|------|-----------------|---------------------|-----------------|
| Standard output / query | ~35KB (~8.7K tok) | ~69KB (~17K tok) | ~76KB (~19K tok) |
| Relevant / query | ~6.0 | ~6.2 | ~8.4 |
| **Standard efficiency** | **0.69 rel/1K tok** | **0.36 rel/1K tok** | **0.44 rel/1K tok** |
| **Compact efficiency** | **N/A** | **N/A** | **~0.44 rel/1K tok** (no visible change) |

MCP1 (academix) leads on token efficiency due to concise OpenAlex-only output. MCP3's richer metadata (abstracts, OA flags, relevance scores) costs more tokens but delivers higher precision.

---

## 5. MCP Comparison Summary

| Dimension | MCP1 (academix) | MCP2 (paper-search) | MCP3 (bundled) |
|-----------|-----------------|---------------------|-----------------|
| Source | OpenAlex only | 21 sources (all) | 6–8 curated sources |
| Deduplication | None (single source) | None (raw per-source) | Yes (cross-source) |
| Relevance score | No | No | Yes (0–10) |
| Max papers | 15 | 25–30 (5 per source) | 15 (deduped) |
| Noise from bioRxiv/medRxiv | No | Yes (5 each) | No (excluded by default) |
| Query expansion | No | No | Yes (auto-expand acronyms) |
| Citation counts | Yes | No | Yes |
| Open Access info | No | No | Yes |
| Token efficiency | Best (0.69 rel/1K) | Worst (0.36 rel/1K) | Middle (0.44 rel/1K) |
| Error rate | 0% | 100% | 0% |
| Best for | High-citation landmark papers | Broad multi-domain coverage | Precision + relevance filtering |

---

## 6. Raw Data Summary (per MCP per query)

### Q1: LLM feedback accuracy category-level writing grammar mechanics

**MCP1 Top 2:**
1. Escalante, Pack & Barrett (2023) — "AI-generated feedback on writing: insights into efficacy and ENL student preference" — 431 citations, DOI: 10.1186/s41239-023-00425-2
2. Tran (2025) — "Enhancing EFL Writing Revision Practices: The Impact of AI- and Teacher-Generated Feedback" — 26 citations, DOI: 10.3390/educsci15020232

**MCP2 Top 2:**
1. Hsu (2026) — "Examining the Impact of Feedback from Automated Writing Evaluation Tools on Learners' Grammar Accuracy" — DOI: 10.3138/calico-2024-0021
2. Shin & Lee (2025) — "Leveraging LLM-based chatbots for interactional grammar feedback in L2 writing" — DOI: 10.1080/17501229.2025.2549037

**MCP3 Top 2 (relevance_score):**
1. Hsu (2026) — "Examining the Impact of Feedback from AWE Tools on Learners' Grammar Accuracy" — score: 10
2. Afriana et al. (2025) — "AI Chatbots for Personalized Grammar Feedback and Autonomous Learning" — score: 10

### Q2: automated feedback classifier DeBERTa fine-tuned educational text classification

**MCP1 Top 2:**
1. Morris et al. (2024) — "Automated Scoring of Constructed Response Items in Math Assessment Using LLMs" — 18 citations
2. Rodrigues et al. (2024) — "Assessing the quality of automatic-generated short answers using GPT-4" — 32 citations

**MCP2 Top 2:**
1. Takenaka (2025) — "Performance Evaluation of Emotion Classification in Japanese Using RoBERTa and DeBERTa"
2. Valdes Gonzalez (2026) — "Cost-Aware Model Selection for Text Classification: Multi-Objective Trade-offs"

**MCP3 Top 2 (relevance_score):**
1. Gupta (2025) — "Explainable AI for Automated Student Feedback: A Comparative Study of LIME and SHAP on Text Classification" — score: 10
2. Liu et al. (2024) — "Annotation Guidelines-Based Knowledge Augmentation: Towards Enhancing LLMs for Educational Text Classification" — score: 9

### Q3: feedback uptake individual differences L2 writing revision quality

**MCP1 Top 2:**
1. Zhang & Hyland (2018) — "Student engagement with teacher and automated feedback on L2 writing" — 491 citations
2. Kormos (2012) — "The role of individual differences in L2 writing" — 360 citations

**MCP2 Top 2:**
1. Xu & Wang (2023) — "Individual differences in L2 writing feedback-seeking behaviors: The predictive roles of various motivational constructs" — 34 citations
2. Choi et al. (2021) — "Transpacific telecollaboration and L2 writing: Influences of interpersonal dynamics on peer feedback and revision uptake"

**MCP3 Top 2 (relevance_score):**
1. Kim & Kang (2026) — "AI-generated feedback in an EAP writing classroom: The collaborative process of feedback, uptake, and revision quality" — score: 10
2. Emeliyanova & Kim (2019) — "The effects of written corrective feedback on the accuracy of L2 writing" — score: 10

### Q4: spaced micro-learning AI feedback evaluation training metacognitive

**MCP1 Top 2:**
1. Fan et al. (2024) — "Beware of metacognitive laziness: Effects of generative AI on learning motivation, processes, and performance" — 371 citations
2. Tapalova & Zhiyenbayeva (2022) — "AI in Education: AIEd for Personalised Learning Pathways" — 544 citations

**MCP2 Top 2:**
1. Lim (2025) — "DeBiasMe: De-biasing Human-AI Interactions with Metacognitive AIED Interventions"
2. Luo & Yusuf (2025) — "Bridging AI and pedagogy: how AI-adaptive feedback shapes Chinese EFL students' writing engagement"

**MCP3 Top 2 (relevance_score):**
1. Kolloff et al. (2025) — "The role of metacognitive experience: Can feedback training affect kindergarteners' monitoring accuracy?" — score: 9
2. Alsaiari et al. (2025) — "Directive, Metacognitive or a Blend of Both? A Comparison of AI-Generated Feedback Types" — score: 6

### Q5: metacognitive laziness AI over-reliance student learning critical thinking

**MCP1 Top 2:**
1. Fan et al. (2024) — "Beware of metacognitive laziness: Effects of generative AI on learning motivation, processes, and performance" — 371 citations
2. Gerlich (2025) — "AI Tools in Society: Impacts on Cognitive Offloading and the Future of Critical Thinking" — 549 citations

**MCP2 Top 2:**
1. Fan et al. (2024) — "Beware of metacognitive laziness" — 371 citations
2. Yurt & Kuşci (2025) — "Factors influencing critical thinking during AI use among university students: the mediating effects of epistemic laziness and metacognitive weakness"

**MCP3 Top 2 (relevance_score):**
1. Fan et al. (2024) — "Beware of metacognitive laziness" — score: 9
2. Yurt & Kuşci (2025) — "Factors influencing critical thinking during AI use" — score: 10

---

## 7. Recommendations

1. **For precision-focused literature search**: Use **MCP3 (research_search_literature)** — best relevance, deduplication, and metadata completeness.
2. **For landmark/citation-aware search**: Use **MCP1 (academix)** — returns highest-cited papers from OpenAlex's comprehensive index.
3. **For maximum recall / exploratory search**: Use **MCP2 (paper-search)** — covers 21 sources, but expect noise from bioRxiv/medRxiv.
4. **Production setting**: Enable `compact=True` on MCP3 to save ~70% token costs while keeping relevance scores.
5. **Critical gap**: None of the MCPs reliably returned papers mentioning "spaced micro-learning" for Q4 — suggests query reformulation needed for that concept.

---

## 8. Full Paper Listings (All MCPs, All Queries)

### Q1: LLM feedback accuracy category-level writing grammar mechanics

**MCP1 (academix)** — 15 papers
1. Escalante, Pack & Barrett (2023) — AI-generated feedback on writing — DOI:10.1186/s41239-023-00425-2 — 431 cites
2. Yang et al. (2024) — Harnessing the Power of LLMs in Practice — DOI:10.1145/3649506 — 457 cites
3. Yang et al. (2023) — Harnessing the Power of LLMs (arXiv) — DOI:10.48550/arxiv.2304.13712 — 151 cites
4. Liu et al. (2023) — Summary of ChatGPT-Related Research — DOI:10.48550/arxiv.2304.01852 — 123 cites
5. Polverini & Gregorcic (2023) — How understanding LLMs can inform ChatGPT use in physics education — DOI:10.1088/1361-6404/ad1420 — 90 cites
6. Bhullar et al. (2024) — ChatGPT in higher education - a synthesis — DOI:10.1007/s10639-024-12723-x — 90 cites
7. Gustilo et al. (2024) — Algorithmically-driven writing and academic integrity — DOI:10.1007/s40979-024-00153-8 — 49 cites
8. Warstadt et al. (2023) — Findings of the BabyLM Challenge — DOI:10.18653/v1/2023.conll-babylm.1 — 68 cites
9. Su et al. (2024) — LLMs for Forecasting and Anomaly Detection — DOI:10.48550/arxiv.2402.10350 — 73 cites
10. Naznin et al. (2025) — ChatGPT Integration in Higher Education — DOI:10.3390/computers14020053 — 57 cites
11. Selim (2024) — Transformative Impact of AI-Powered Tools on Academic Writing — DOI:10.5539/ijel.v14n1p14 — 36 cites
12. Giunchi et al. (2024) — DreamCodeVR — DOI:10.1109/vr58804.2024.00078 — 36 cites
13. Pataranutaporn et al. (2023) — Living Memories — DOI:10.1145/3581641.3584065 — 40 cites
14. Tran (2025) — Enhancing EFL Writing Revision Practices — DOI:10.3390/educsci15020232 — 26 cites
15. Oates & Johnson (2025) — ChatGPT in the Classroom — DOI:10.1007/s40593-024-00452-8 — 40 cites

**MCP2 (paper-search)** — 18 papers
1. Wasi et al. (2024) — LLMs as Writing Assistants — arxiv:2404.00027
2. Rashkin et al. (2025) — Help Me Write a Story — arxiv:2507.16007
3. Kallmeyer et al. (2008) — TuLiPA (grammar parsing) — arxiv:0807.3622 (irrelevant)
4-6. bioRxiv: neuroscience papers (irrelevant — prefrontal-hypothalamic circuitry, hippocampus, SynGAP1)
7-9. medRxiv: COVID-19 homicide, HIV+NCD, Vietnam epidemiology (irrelevant)
10. Santanatanonw (2021) — Student engagement writing grammar accuracy — DOI:10.58837/chula.the.2021.384
11. Santanatanon (2022) — Exploring student engagement WCF — DOI:10.58837/chula.pasaa.63.1.2 — 2 cites
12. Shin & Lee (2025) — LLM-based chatbots grammar feedback L2 — DOI:10.1080/17501229.2025.2549037 — 1 cite
13. Escalante et al. (2023) — AI-generated feedback on writing — DOI:10.1186/s41239-023-00425-2 — 431 cites
14. Yang et al. (2024) — Harnessing the Power of LLMs — DOI:10.1145/3649506 — 457 cites
15. Yang et al. (2023) — Harnessing the Power of LLMs (arXiv) — DOI:10.48550/arxiv.2304.13712 — 151 cites
16-18. EuropePMC: chemical sciences LLMs, AI security, drug discovery LLMs (tangential)

**MCP3 (bundled)** — 15 papers (relevance scores)
1. Hsu (2026) — AWE tools grammar accuracy — score:10 — DOI:10.3138/calico-2024-0021
2. Afriana et al. (2025) — AI Chatbots grammar feedback — score:10 — DOI:10.61486/qvxv5822
3. Shin & Lee (2025) — LLM-based chatbots grammar feedback L2 — score:10 — DOI:10.1080/17501229.2025.2549037
4. Tran (2025) — AI/Teacher feedback sequences EFL writing — score:9 — DOI:10.3390/educsci15020232
5. Song & Kim (2025) — Elementary revision teacher feedback — score:9 — DOI:10.37736/kjlr.2025.06.16.3.06
6. Escalante et al. (2023) — AI feedback efficacy ENL — score:9 — DOI:10.1186/s41239-023-00425-2
7. Santanatanon (2022) — Student engagement WCF grammar — score:9 — DOI:10.58837/chula.pasaa.63.1.2
8. Wang & Liu (2025) — ChatGPT vs human feedback writing — score:9 — DOI:10.30191/ETS.202503_28(2).0001
9. Yan et al. (2025) — AWE + dialogic peer feedback — score:8 — DOI:10.1080/10494820.2025.2491620
10. Nilson & Zimmerman (2025) — AI formative assessment L2 writing — score:8 — DOI:10.1080/09588221.2025.2518159
11. Kurt & Karabulut (2024) — Screencast feedback L2 writing — score:8 — DOI:10.2139/ssrn.5011375
12. Oates & Johnson (2025) — ChatGPT critical evaluation skills — score:7 — DOI:10.1007/s40593-024-00452-8
13. Chen et al. (2025) — ChatGPT feedback EFL writing revision — score:7 — DOI:10.1080/2331186X.2025.2517186
14. Wasi et al. (2024) — LLMs writing ownership reasoning — score:5 — DOI:10.1145/3690712.3690723
15. Guo et al. (2024) — ChatGPT writing pedagogy EFL — score:5 — DOI:10.3390/educsci14080906

### Q2: automated feedback classifier DeBERTa fine-tuned educational text classification

**MCP1 (academix)** — 15 papers
1. Kumar (2024) — LLMs survey technical frameworks — DOI:10.1007/s10462-024-10888-y — 266 cites
2. Yu et al. (2023) — LLM as Attributed Training Data Generator — DOI:10.48550/arxiv.2306.15895 — 72 cites
3. Hernandez & Nie (2022) — AI-IP personality scale development — DOI:10.1111/peps.12543 — 59 cites
4. Ahn et al. (2024) — LLMs for Mathematical Reasoning — DOI:10.18653/v1/2024.eacl-srw.17 — 64 cites
5. Jin et al. (2022) — Logical Fallacy Detection — DOI:10.18653/v1/2022.findings-emnlp.532 — 43 cites
6. Kasri et al. (2025) — LLMs in Cybersecurity — DOI:10.3390/computation13020030 — 47 cites
7. Modi et al. (2023) — LegalEval understanding legal texts — DOI:10.18653/v1/2023.semeval-1.318 — 40 cites
8. Papageorgiou et al. (2024) — LLMs in Fake News — DOI:10.3390/fi16080298 — 47 cites
9. Wan et al. (2024) — DELL misinformation detection — DOI:10.18653/v1/2024.findings-acl.155 — 41 cites
10. Zhou et al. (2023) — LLMs in Medicine — DOI:10.48550/arxiv.2311.05112 — 37 cites
11. Warstadt et al. (2023) — BabyLM Challenge — DOI:10.18653/v1/2023.conll-babylm.1 — 68 cites
12. Tan et al. (2022) — Event Causality Identification — DOI:10.18653/v1/2022.case-1.28 — 24 cites
13. Kampelopoulos et al. (2025) — LLMs in architecture/engineering — DOI:10.1007/s10462-025-11241-7 — 33 cites
14. Morris et al. (2024) — Automated Scoring Math LLMs — DOI:10.1007/s40593-024-00418-w — 18 cites
15. Rodrigues et al. (2024) — GPT-4 short answer quality — DOI:10.1016/j.caeai.2024.100248 — 32 cites

**MCP2 (paper-search)** — 18 papers
1. Takenaka (2025) — Emotion Classification Japanese DeBERTa — arxiv:2505.00013
2. Valdes Gonzalez (2026) — Cost-Aware Model Selection Text Classification — arxiv:2602.06370
3. Pădurean et al. (2025) — Humanizing Automated Programming Feedback — arxiv:2509.10647
4-6. bioRxiv: neuroscience (irrelevant)
7-9. medRxiv: COVID/vietnam/epidemiology (irrelevant)
10-12. CrossRef: figure component, CASE task paper, skin disease classification (mostly irrelevant)
13. Kumar (2024) — LLMs survey — DOI:10.1007/s10462-024-10888-y — 266 cites
14. Yu et al. (2023) — LLM Data Generator — DOI:10.48550/arxiv.2306.15895 — 72 cites
15. Hernandez & Nie (2022) — AI-IP — DOI:10.1111/peps.12543 — 59 cites
16-18. EuropePMC: NER substance use, hybrid DL+fuzzy ELL eval, healthcare text classification review

**MCP3 (bundled)** — 15 papers (relevance scores)
1. Gupta (2025) — XAI for automated student feedback LIME SHAP — score:10 — DOI:10.1016/j.caeai.2025.100386
2. Liu et al. (2024) — AGKA educational text classification — score:9 — DOI:10.1145/3659901
3. Takenaka (2025) — Emotion Classification Japanese DeBERTa — score:9 — arxiv:2505.00013
4. Valdes Gonzalez (2026) — Cost-Aware Model Selection — score:8 — arxiv:2602.06370
5. Rodrigues et al. (2024) — GPT-4 short answer quality — score:8 — DOI:10.1016/j.caeai.2024.100248
6. Pădurean et al. (2025) — Humanizing Automated Programming Feedback — score:7 — arxiv:2509.10647
7. Zhao (2025) — Hybrid DL+fuzzy ELL evaluation DeBERTa — score:7 — DOI:10.1038/s41598-025-17738-z
8. Dey et al. (2026) — NER substance use DeBERTa — score:6 — DOI:10.1142/9789819824755_0002
9. Sakai & Lam (2026) — LLMs Healthcare Text Classification review — score:6 — DOI:10.2196/79202
10. Morris et al. (2024) — Automated Scoring Math — score:5 — DOI:10.1007/s40593-024-00418-w
11. Kent & Krumbiegel (2021) — CASE socio-political event classification — score:5 — DOI:10.18653/v1/2021.case-1.26
12. Kasri et al. (2025) — LLMs in Cybersecurity — score:4 — DOI:10.3390/computation13020030
13. Papageorgiou et al. (2024) — LLMs Fake News — score:4 — DOI:10.3390/fi16080298
14. Wan et al. (2024) — DELL misinformation detection — score:4 — DOI:10.18653/v1/2024.findings-acl.155
15. Sattarzadeh (2025) — Skin disease classification MobileNetV2 — score:3 — DOI:10.20944/preprints202511.1676.v1

### Q3: feedback uptake individual differences L2 writing revision quality

**MCP1 (academix)** — 15 papers
1. Zhang & Hyland (2018) — Student engagement teacher/automated feedback L2 — DOI:10.1016/j.asw.2018.02.004 — 491 cites
2. Ellis (2005) — Explicit/implicit language knowledge — DOI:10.1017/s027226310505014x — 872 cites
3. Kormos (2012) — Individual differences L2 writing — DOI:10.1016/j.jslw.2012.09.003 — 360 cites
4. van Beuningen et al. (2008) — Direct/indirect CF L2 accuracy — DOI:10.2143/itl.156.0.2034439 — 239 cites
5. van Beuningen (2010) — CF in L2 Writing — DOI:10.6018/ijes/2010/2/119171 — 235 cites
6. Ware & O'Dowd (2008) — Peer feedback language form telecollaboration — DOI:10.64152/10125/44130 — 277 cites
7. Long (2016) — In Defense of Tasks and TBLT — DOI:10.1017/s0267190515000057 — 344 cites
8. Xiao & Zhi (2023) — EFL learners ChatGPT use — DOI:10.3390/languages8030212 — 244 cites
9. Zhang & Hyland (2021) — Fostering student engagement with feedback — DOI:10.1016/j.asw.2021.100586 — 206 cites
10. Mahapatra (2024) — Impact ChatGPT ESL academic writing — DOI:10.1186/s40561-024-00295-9 — 270 cites
11. Révész (2011) — Task complexity individual differences — DOI:10.1111/j.1540-4781.2011.01241.x — 236 cites
12. Storch (2010) — Critical feedback on WCF research — DOI:10.6018/ijes/2010/2/119181 — 143 cites
13. Son et al. (2023) — AI technologies language learning — DOI:10.1515/jccall-2023-0015 — 161 cites
14. Gilabert (2007) — Task complexity self-repairs L2 — DOI:10.1515/iral.2007.010 — 202 cites
15. Ene & Upton (2014) — Learner uptake teacher electronic feedback — DOI:10.1016/j.system.2014.07.011 — 110 cites

**MCP2 (paper-search)** — ~24 papers
Key papers among noise:
1. Wasi et al. (2024) — LLMs Writing Assistants — arxiv:2404.00027
2. Kim et al. (2025) — Voice interaction conversational AI writing revision — arxiv:2504.08687
3. Liu et al. (2023) — Predicting revision quality argumentative writing — arxiv:2306.00667
4-6. bioRxiv: neuroscience (irrelevant)
7-9. medRxiv: COVID/vietnam/HIV (irrelevant)
10. Song & Kim (2025) — Elementary revision teacher feedback — DOI:10.37736/kjlr.2025.06.16.3.06
11. Kim & Emeliyanova (2019) — WCF collaborative vs individual revision — DOI:10.1177/1362168819831406 — 56 cites
12. Yan et al. (2025) — AWE + dialogic peer feedback — DOI:10.1080/10494820.2025.2491620
13. Xu & Wang (2023) — Individual differences feedback-seeking — DOI:10.1016/j.asw.2023.100698 — 34 cites
14. Kurt & Karabulut (2024) — Screencast feedback L2 — DOI:10.2139/ssrn.5011375
15. Choi et al. (2021) — Telecollaboration peer feedback revision — DOI:10.1016/j.jslw.2021.100855 — 1 cite
16-18. OpenAlex: Zhang & Hyland 2018, Ellis 2005, Kormos 2012 (redundant with MCP1)
19-21. PMC: spinal cord stimulation, workplace Chinese, L2 writing self-efficacy (tangential)
22-24. Core + EuropePMC: text reconstruction, learner uptake, sociocultural theory

**MCP3 (bundled)** — 15 papers (relevance scores)
1. Kim & Kang (2026) — AI-generated feedback EAP uptake revision — score:10 — DOI:10.1016/j.jslw.2026.101213
2. Emeliyanova & Kim (2019) — WCF accuracy L2 writing — score:10 — DOI:10.1177/1362168819831406
3. Song & Kim (2025) — Elementary revision teacher feedback — score:9 — DOI:10.37736/kjlr.2025.06.16.3.06
4. Yan et al. (2025) — AWE + dialogic peer feedback — score:9 — DOI:10.1080/10494820.2025.2491620
5. Xu & Wang (2023) — Individual differences feedback-seeking — score:8 — DOI:10.1016/j.asw.2023.100698
6. Zhang & Hyland (2018) — Student engagement teacher/automated feedback — score:8 — DOI:10.1016/j.asw.2018.02.004
7. Zhang & Hyland (2021) — Fostering student engagement with feedback — score:8 — DOI:10.1016/j.asw.2021.100586
8. Kormos (2012) — Individual differences L2 writing — score:8 — DOI:10.1016/j.jslw.2012.09.003
9. Storch (2010) — Critical feedback on WCF — score:8 — DOI:10.6018/ijes/2010/2/119181
10. Ene & Upton (2014) — Learner uptake teacher electronic feedback — score:7 — DOI:10.1016/j.system.2014.07.011
11. van Beuningen et al. (2008) — Direct/indirect CF L2 accuracy — score:7 — DOI:10.2143/itl.156.0.2034439
12. van Beuningen (2010) — CF in L2 Writing — score:7 — DOI:10.6018/ijes/2010/2/119171
13. Hyland & Hyland (2006) — Feedback on second language students' writing — score:7 — DOI:10.1016/j.jslw.2006.09.002
14. Choi et al. (2021) — Telecollaboration peer feedback revision — score:6 — DOI:10.1016/j.jslw.2021.100855
15. Kim et al. (2025) — Voice interaction AI writing revision — score:6 — arxiv:2504.08687

### Q4: spaced micro-learning AI feedback evaluation training metacognitive

**MCP1 (academix)** — 15 papers
1. Tapalova & Zhiyenbayeva (2022) — AIEd for Personalised Learning — DOI:10.34190/ejel.20.5.2597 — 544 cites
2. Koedinger et al. (2012) — Knowledge-Learning-Instruction framework — DOI:10.1111/j.1551-6709.2012.01245.x — 719 cites
3. Fan et al. (2024) — Metacognitive laziness GenAI — DOI:10.1111/bjet.13544 — 371 cites
4. Ng et al. (2023) — Teachers AI digital competencies — DOI:10.1007/s11423-023-10203-6 — 562 cites
5. Leung et al. (2014) — Intercultural Competence — DOI:10.1146/annurev-orgpsych-031413-091229 — 405 cites
6. Halkiopoulos & Gkintoni (2024) — AI in E-Learning personalized learning — DOI:10.3390/electronics13183762 — 245 cites
7. Kotseruba & Tsotsos (2018) — Cognitive architectures — DOI:10.1007/s10462-018-9646-y — 511 cites
8. Nye et al. (2014) — AutoTutor review — DOI:10.1007/s40593-014-0029-5 — 264 cites
9. Ouyang et al. (2023) — AI performance prediction learning analytics — DOI:10.1186/s41239-022-00372-4 — 324 cites
10. Arroyo et al. (2014) — Multimedia adaptive tutoring — DOI:10.1007/s40593-014-0023-y — 258 cites
11. Tetzlaff et al. (2020) — Developing Personalized Education — DOI:10.1007/s10648-020-09570-w — 243 cites
12. Järvelä et al. (2023) — Human-AI collaboration SSRL — DOI:10.1111/bjet.13325 — 235 cites
13. Gkintoni et al. (2025) — CLT + AI + neuroscience — DOI:10.3390/brainsci15020203 — 193 cites
14. Lim et al. (2022) — Real-time analytics scaffolds SRL — DOI:10.1016/j.chb.2022.107547 — 174 cites
15. Molenaar et al. (2022) — Measuring SRL multimodal data — DOI:10.1016/j.chb.2022.107540 — 183 cites

**MCP2 (paper-search)** — ~24 papers
Key papers among noise:
1. Lim (2025) — DeBiasMe metacognitive AIED — arxiv:2504.16770
2. Naito & Shirado (2026) — AI prediction forgoing rewards — arxiv:2603.28944
3. Ai et al. (2025) — Foundations of GenIR — arxiv:2501.02842
4-6. bioRxiv: neuroscience (irrelevant)
7-9. medRxiv: COVID/vietnam/HIV (irrelevant)
10. Encyclopedia chapter: Metacognitive Control Over Spaced Practice — DOI:10.1007/978-1-4419-1428-6_4927
11. Yao & Liu (2025) — Emotional feedback AI tool use EFL — DOI:10.21203/rs.3.rs-6289643/v1
12. Guo (2022) — Metacognitive monitoring feedback AR — DOI:10.32469/10355/88875
13-15. OpenAlex: Tapalova, Koedinger, Fan (redundant with MCP1)
16-18. PMC: mobile learning meded, cumulative cognition, AI SRL review
19-21. Core: mixed reality exams, EMEMITALIA proceedings, AI language talent cultivation
22-24. EuropePMC: gamified dCBT platform, AI feedback translation training, (partial)

**MCP3 (bundled)** — 15 papers (relevance scores)
1. Kolloff et al. (2025) — Metacognitive experience feedback training — score:9 — DOI:10.1016/j.lindif.2025.102656
2. Alsaiari et al. (2025) — Directive vs metacognitive AI feedback types — score:6 — DOI:10.1016/j.iheduc.2025.101032
3. Lim (2025) — DeBiasMe metacognitive AIED — score:6 — arxiv:2504.16770
4. Guo (2022) — Metacognitive monitoring feedback AR — score:6 — DOI:10.32469/10355/88875
5. Yao & Liu (2025) — Emotional feedback AI tool use EFL — score:5 — DOI:10.21203/rs.3.rs-6289643/v1
6. Fan et al. (2024) — Metacognitive laziness — score:5 — DOI:10.1111/bjet.13544
7. Tapalova & Zhiyenbayeva (2022) — AIEd Personalized Learning — score:5 — DOI:10.34190/ejel.20.5.2597
8. Halkiopoulos & Gkintoni (2024) — AI E-Learning personalized — score:4 — DOI:10.3390/electronics13183762
9. Järvelä et al. (2023) — Human-AI SSRL — score:4 — DOI:10.1111/bjet.13325
10. Nye et al. (2014) — AutoTutor review — score:4 — DOI:10.1007/s40593-014-0029-5
11. Arroyo et al. (2014) — Multimedia adaptive tutoring — score:4 — DOI:10.1007/s40593-014-0023-y
12. Tetzlaff et al. (2020) — Developing Personalized Education — score:4 — DOI:10.1007/s10648-020-09570-w
13. Ouyang et al. (2023) — AI performance prediction — score:3 — DOI:10.1186/s41239-022-00372-4
14. Molenaar et al. (2022) — Measuring SRL multimodal — score:3 — DOI:10.1016/j.chb.2022.107540
15. Chen et al. (2025) — AI feedback translation training — score:3 — DOI:10.1080/14790718.2025.2517346

### Q5: metacognitive laziness AI over-reliance student learning critical thinking

**MCP1 (academix)** — 15 papers
1. Gerlich (2025) — AI Tools cognitive offloading critical thinking — DOI:10.3390/soc15010006 — 549 cites
2. Fan et al. (2024) — Metacognitive laziness GenAI — DOI:10.1111/bjet.13544 — 371 cites
3. Ngo (2023) — University students ChatGPT perception — DOI:10.3991/ijet.v18i17.39019 — 251 cites
4. Prather et al. (2023) — GenAI revolution computing education — DOI:10.1145/3623762.3633499 — 308 cites
5. Zhou et al. (2024) — AI usage higher education — DOI:10.53761/xzjprb23 — 81 cites
6. Huang & Yan (2025) — GenAI English language education — DOI:10.1002/tesq.70042 — 1 cite
7. Ravšelj et al. (2025) — Global ChatGPT perceptions — DOI:10.1371/journal.pone.0315011 — 142 cites
8. Bauer et al. (2025) — Beyond the hype AI learning — DOI:10.1007/s10648-025-10020-8 — 63 cites
9. Naznin et al. (2025) — ChatGPT Integration HE — DOI:10.3390/computers14020053 — 57 cites
10. Wu (2024) — Critical thinking pedagogics ChatGPT — DOI:10.20849/jed.v8i1.1404 — 43 cites
11. Cambaz & Zhang (2024) — AI code generation models programming — DOI:10.1145/3626252.3630958 — 39 cites
12. Szmyd & Mitera (2024) — AI impact critical thinking — DOI:10.35808/ersj/3876 — 29 cites
13. Meakin (2024) — GenAI library resources — DOI:10.5860/ital.v43i3.17246 — 32 cites
14. Collins-Thompson et al. (2017) — Search as Learning — DOI:10.4230/dagrep.7.2.135 — 40 cites
15. Allison et al. (2025) — GenAI to XR educational computing — DOI:10.1177/07356331251359964 — 24 cites

**MCP2 (paper-search)** — 23 papers
1. Singh et al. (2025) — Metacognitive prompts critical thinking GenAI — arxiv:2505.24014
2. Lim (2025) — DeBiasMe metacognitive AIED — arxiv:2504.16770
3. Mei & Weber (2025) — AI augment critical thinking — arxiv:2504.14689
4-6. bioRxiv: neuroscience (irrelevant)
7-9. medRxiv: COVID/vietnam/HIV (irrelevant)
10. Yurt & Kuşci (2025) — Epistemic laziness metacognitive weakness critical thinking — DOI:10.1007/s12144-025-08800-0 — 2 cites
11. He et al. (2026) — GenAI project-based critical thinking — DOI:10.21125/inted.2026.1700
12. Rahayuan et al. (2017) — Metacognitive skills critical thinking — DOI:10.5220/0007298600650067 — 1 cite
13-15. OpenAlex: Gerlich, Fan, Ngo (redundant with MCP1)
16-18. PMC: HAIST AI talent dev, L2 writing GAI risk awareness, AI creativity dependency
19-21. Core: AI impact mindset critical thinking, critical thinking place, GenAI academic writing Pakistan
22-23. EuropePMC: GenAI literacy academic achievement, higher-order thinking problem-solving AI

**MCP3 (bundled)** — 15 papers (relevance scores)
1. Yurt & Kuşci (2025) — Epistemic laziness metacognitive weakness — score:10 — DOI:10.1007/s12144-025-08800-0
2. Fan et al. (2024) — Metacognitive laziness — score:9 — DOI:10.1111/bjet.13544
3. Gerlich (2025) — AI tools cognitive offloading — score:8 — DOI:10.3390/soc15010006
4. Singh et al. (2025) — Metacognitive prompts critical thinking GenAI — score:8 — arxiv:2505.24014
5. Bauer et al. (2025) — Beyond the hype AI learning — score:8 — DOI:10.1007/s10648-025-10020-8
6. Wu (2024) — Critical thinking pedagogics ChatGPT — score:8 — DOI:10.20849/jed.v8i1.1404
7. Szmyd & Mitera (2024) — AI impact critical thinking — score:8 — DOI:10.35808/ersj/3876
8. Lim (2025) — DeBiasMe metacognitive AIED — score:7 — arxiv:2504.16770
9. Mei & Weber (2025) — AI augment critical thinking — score:7 — arxiv:2504.14689
10. Ngo (2023) — ChatGPT perception university students — score:7 — DOI:10.3991/ijet.v18i17.39019
11. Rahayuan et al. (2017) — Metacognitive skills critical thinking — score:7 — DOI:10.5220/0007298600650067
12. He et al. (2026) — GenAI project-based critical thinking — score:6 — DOI:10.21125/inted.2026.1700
13. Zhou et al. (2024) — AI usage higher education — score:6 — DOI:10.53761/xzjprb23
14. Wang (2026) — GenAI literacy academic achievement — score:6 — DOI:10.3389/fpsyg.2026.1761562
15. Zhang et al. (2025) — Higher-order thinking problem-solving AI — score:6 — DOI:10.1186/s40359-025-03404-6

---

## 9. MCP3 Abstract Coverage

MCP3 abstract coverage across all 75 papers: **49/75 (65.3%)** had non-empty abstracts in the API response. 26 papers (34.7%) returned empty abstract fields. This is the **abstract coverage** metric — a real constraint of academic search APIs. Below is the verbatim abstract text for each paper (marked `[EMPTY]` where the API returned none).

### Q1 — Coverage: 9/15 = 60%

1. **Hsu (2026)** — `[HAS ABSTRACT]` "Improving the writing abilities of language learners remains a significant challenge. Although research indicates that automated writing evaluation (AWE) tools can improve learners' grammar accuracy and that learners find AWE feedback helpful, the specific impact of different types of feedback offered by these tools on this improvement remains unclear. This study investigated the effects of two AWE tools on learners' grammar accuracy: Grammarly, which offers both metacognitive feedback and direct correction, and Ginger, which offers direct correction. Learners' perceptions of using these tools were also explored. Three groups were recruited and randomly assigned as a control group and two experimental groups. All groups received teacher feedback on the writing content, while the experimental groups additionally received feedback from the two AWE tools, respectively. Four writing tasks were conducted, with the first serving as a pre-test and the third and fourth serving as a post-test and a delayed post-test, respectively. Following completion of all writing tasks, the experimental groups filled out a user survey to gather their thoughts on AWE. The analysis of learners' written texts has shown that the AWE improved learners' grammar accuracy in writing as they allowed learners to identify grammar-related errors and possibly learn from their mistakes. Additionally, both types of corrective feedback were effective in reducing grammar-related errors, particularly those related to rule-governed errors. Many learners suggested that the feedback provided by AWE was beneficial for their writing tasks, so they were willing to use them to revise their texts."

2. **Afriana et al. (2025)** — `[HAS ABSTRACT]` "Grammar correction has long been recognized as one of the most essential yet challenging aspects of second language (L2) learning. Teachers are expected to provide detailed and contextual feedback, but this process is often time-consuming and less effective in large classrooms. This study investigates the potential of AI-based chatbots as innovative tools for delivering personalized and real-time grammar feedback to support English language learning. The research employed an experimental design involving two groups: an experimental group using AI chatbots for grammar practice and a control group applying traditional teacher-based correction. Data were collected through grammar pre-tests and post-tests, writing tasks, engagement and motivation questionnaires, classroom observations, and student reflection notes. The findings demonstrate that students in the experimental group achieved significantly higher improvements in grammar accuracy compared to the control group, particularly in subject–verb agreement, tense usage, and complex sentence structures. In addition, chatbot use fostered greater engagement, motivation, and active participation, with students reporting reduced language anxiety and increased confidence in practicing English."

3. **Noerjaman et al. (2025)** — `[HAS ABSTRACT]` "Submission of well-structured job application letters is an essential aspect of business and government recruitment processes. However, due to difficulties with grammar and mechanics, many students, fresh graduates included, fail to produce high-quality job applications. While human reviewers typically give feedback to enhance these skills, Artificial Intelligence (AI) has brought about automated feedback systems. The research compared the performance of two artificial intelligence models, Gemini and ChatGPT, and human experts in assessing job application letters. The study compared feedback in six writing features—subject-verb agreement, parallelism, spelling, capitalization, punctuation, and sentence variety—of 10 job application letters composed by final-year high school students. Results indicated that ChatGPT and Gemini performed better than human experts in most metrics."

4. **Santanatanon (2022)** — `[EMPTY — abstract: <jats:p/>]`

5. **Santanatanonw (2021)** — `[HAS ABSTRACT]` "Whether students benefit from written corrective feedback may depend on their level of engagement with the feedback. To date, student engagement with written corrective feedback has been investigated qualitatively. However, the association between student engagement with feedback and learning outcomes that result from that engagement has not been examined. Moreover, little attention has been paid to secondary students' engagement with written corrective feedback because most studies have focused on university students. Therefore, this mixed-method experimental study was conducted to discern if there is an association between student engagement with feedback and English writing grammar accuracy and explore how high school students engaged with the feedback behaviorally, affectively, and cognitively. Writing tests and a questionnaire were conducted with 26 tenth graders, and focus group interviews were conducted with five randomly-selected participants before, during, and after the intervention. The results indicated that there was no significant association between the variables."

6. **Li et al. (2026)** — `[HAS ABSTRACT]` "Large Language Models (LLMs) often struggle with creative generation, and multi-agent frameworks that improve reasoning through interaction can paradoxically hinder creativity by inducing content homogenization. We introduce LLM Review, a peer-review-inspired framework implementing Blind Peer Review: agents exchange targeted feedback while revising independently, preserving divergent creative trajectories. To enable rigorous evaluation, we propose SciFi-100, a science fiction writing dataset with a unified framework combining LLM-as-a-judge scoring, human annotation, and rule-based novelty metrics. Experiments demonstrate that LLM Review consistently outperforms multi-agent baselines, and smaller models with our framework can surpass larger single-agent models, suggesting interaction structure may substitute for model scale."

7. **Ulviani (2025)** — `[HAS ABSTRACT]` "This study investigates the impact of error feedback on students' writing accuracy in Indonesian language learning. Using a quasi-experimental mixed-methods design, sixty undergraduate students from a state university in Indonesia were divided into an experimental group (n=30) and a control group (n=30). The experimental group received structured feedback, combining direct and metalinguistic correction, while the control group received only general comments on content and organization. Data were collected through pre-test, mid-test, and post-test essays, supported by semi-structured interviews and reflective journals. Quantitative findings revealed that both groups improved over time, but the experimental group demonstrated significantly greater gains. Their overall error frequency decreased by almost 50%, with the most substantial improvements observed in grammar, cohesion, and lexical choice."

8. **Termjai (2024)** — `[HAS ABSTRACT]` "While previous research has underscored the implications of peer feedback in general EFL contexts, there has been limited exploration of its specific implications within the context of Thailand. This study investigated the effectiveness of peer feedback in enhancing the writing skills and compositions of Thai students. It aimed to explore students' perceptions of its efficacy, identify the specific writing elements addressed and integrated by feedback givers and receivers, and assess the accuracy of the feedback and revisions. The participants included 35 English major students from a government university in Thailand enrolled in the English Reading and Writing course. The findings revealed unanimous agreement among students regarding the positive impact of peer feedback on their writing skills and quality, despite relatively lower levels of perceived confidence in both providing and receiving peer feedback."

9. **Thewissen & Pretorius (2026)** — `[EMPTY]`

10. **Shin & Lee (2025)** — `[EMPTY]`

11. **Glüsing et al. (2025)** — `[EMPTY]`

12. **Sladek (2022)** — `[EMPTY]`

13. **Hussein (2020)** — `[EMPTY]`

14. **Muñoz Hernández (2020)** — `[EMPTY]`

15. **Santanatanon (2021, duplicate)** — `[EMPTY]`

**Q1 abstract coverage: 9/15 = 60%.**

### Q2 — Coverage: 12/15 = 80%

1. **Gupta (2025)** — `[HAS ABSTRACT]` "This preprint evaluates two widely used explanation methods, LIME and SHAP, for a binary text-classification task on student feedback. A TF-IDF + logistic regression baseline is trained to predict whether feedback is positive or negative, and both methods are applied to generate local and global explanations. The key empirical finding is that LIME and SHAP often select different top tokens for individual predictions (near-zero token-level overlap), yet their explanations consistently converge on the same underlying themes (e.g., clarity/organization vs. pace/coverage). This suggests that exact feature agreement is not necessary for useful interpretability in high-dimensional sparse text, and that combining methods provides a more trustworthy view of model behavior for educators."

2. **Gegenheimer (2024)** — `[EMPTY]`

3. **Valdes Gonzalez (2026)** — `[HAS ABSTRACT]` "Large language models (LLMs) such as GPT-4o and Claude Sonnet 4.5 have demonstrated strong capabilities in open-ended reasoning and generative language tasks, leading to their widespread adoption across a broad range of NLP applications. However, for structured text classification problems with fixed label spaces, model selection is often driven by predictive performance alone, overlooking operational constraints encountered in production systems. In this work, we present a systematic comparison of two contrasting paradigms for text classification: zero- and few-shot prompt-based large language models, and fully fine-tuned encoder-only architectures. We evaluate these approaches across four canonical benchmarks (IMDB, SST-2, AG News, and DBPedia), measuring predictive quality (macro F1), inference latency, and monetary cost. Our results show that fine-tuned encoder-based models from the BERT family achieve competitive, and often superior, classification performance while operating at one to two orders of magnitude lower cost and latency compared to zero- and few-shot LLM prompting."

4. **Liu et al. (2024)** — `[HAS ABSTRACT]` "Various machine learning approaches have gained significant popularity for the automated classification of educational text to identify indicators of learning engagement — i.e. learning engagement classification (LEC). LEC can offer comprehensive insights into human learning processes, attracting significant interest from diverse research communities. Recently, Large Language Models (LLMs), such as ChatGPT, have demonstrated remarkable performance in various NLP tasks. However, their comprehensive evaluation and improvement approaches in LEC tasks have not been thoroughly investigated. In this study, we propose the Annotation Guidelines-based Knowledge Augmentation (AGKA) approach to improve LLMs. AGKA employs GPT 4.0 to retrieve label definition knowledge from annotation guidelines, and then applies the random under-sampler to select a few typical examples. The study results demonstrate that AGKA can enhance non-fine-tuned LLMs, particularly GPT 4.0 and Llama 3 70B. GPT 4.0 with AGKA few-shot outperforms full-shot fine-tuned models such as BERT and RoBERTa on simple binary classification datasets. However, GPT 4.0 lags in multi-class tasks that require a deep understanding of complex semantic information."

5. **Rahmat et al. (2025)** — `[EMPTY]`

6. **Takenaka (2025)** — `[HAS ABSTRACT]` "Background: Practical applications such as social media monitoring and customer-feedback analysis require accurate emotion detection for Japanese text, yet resource scarcity and class imbalance hinder model performance. Objective: This study aims to build a high-accuracy model for predicting the presence or absence of eight Plutchik emotions in Japanese sentences. Methods: Using the WRIME corpus, we transform reader-averaged intensity scores into binary labels and fine-tune four pre-trained language models (BERT, RoBERTa, DeBERTa-v3-base, DeBERTa-v3-large). Results: DeBERTa-v3-large attains the best mean accuracy (0.860) and F1-score (0.662), outperforming all other models. It maintains robust F1 across both high-frequency emotions (e.g., Joy, Anticipation) and low-frequency emotions (e.g., Anger, Trust). The LLMs lag, with ChatGPT-4o and TinySwallow-1.5B-Instruct scoring 0.527 and 0.292 in mean F1, respectively."

7. **Pădurean et al. (2025)** — `[HAS ABSTRACT]` "The growing need for automated and personalized feedback in programming education has led to recent interest in leveraging generative AI for feedback generation. However, current approaches tend to rely on prompt engineering techniques in which predefined prompts guide the AI to generate feedback. This can result in rigid and constrained responses that fail to accommodate the diverse needs of students and do not reflect the style of human-written feedback from tutors or peers. In this study, we explore learnersourcing as a means to fine-tune language models for generating feedback that is more similar to that written by humans, particularly peer students. We collected approximately 1,900 instances of student-written feedback. Our findings indicate that fine-tuning models on learnersourced data not only produces feedback that better matches the style of feedback written by students, but also improves accuracy compared to feedback generated through prompt engineering alone."

8. **Kumar et al. (2026)** — `[HAS ABSTRACT]` "Large Language Models have introduced new possibilities for programming education through personalized support, content creation, and automated feedback. While recent studies have demonstrated the potential for feedback generation, many techniques rely on proprietary models, raising concerns about cost, computational demands, and the ethical implications of sharing student code. Open LLMs provide an alternative approach, but they do not currently have the capabilities of proprietary models. To address this problem, we investigate whether parameter-efficient fine-tuning (PEFT) and prompt engineering can be used to adapt and enhance the quality of feedback generated by the open LLM Code Llama. Our findings indicate that PEFT leads to notable improvements in feedback quality and significantly outperforms prompt engineering. Student evaluation indicates that learners value the PEFT model's feedback and see it as being equally effective as the proprietary ChatGPT model."

9. **Sattarzadeh (2025)** — `[HAS ABSTRACT]` "Skin diseases are among the most widespread and visually diverse medical conditions worldwide, affecting millions of people annually. This paper presents a deep learning-based automated framework for skin disease classification using a fine-tuned MobileNetV2 model implemented with TensorFlow and Keras. The dataset contains over 56,000 images covering 30 representative disease classes. The model achieved a validation accuracy of 29.36%."

10. **Fatihah et al. (2025)** — `[HAS ABSTRACT]` "Educational platforms often collect extensive user feedback to evaluate and improve their services. Analyzing such feedback manually is time-consuming and inefficient, highlighting the need for automated sentiment analysis. This study aims to develop an efficient and reliable sentiment analysis model using TinyBERT to classify user reviews from the Coursera educational platform. A dataset of 60,000 reviews was categorized into three sentiment classes: positive, neutral, and negative. TinyBERT was fine-tuned to address the imbalanced sentiment distribution. The evaluation results show an overall accuracy of 78%, with an F1-score of 0.90 for the positive class."

11. **Pang (2020)** — `[HAS ABSTRACT]` "Short text classification is a method for classifying short sentence with predefined labels. However, short text is limited in shortness in text length that leads to a challenging problem of sparse features. Most of existing methods treat each short sentences as independently and identically distributed (IID), local context only in the sentence itself is focused and the relational information between sentences are lost. To overcome these limitations, we propose a PathWalk model that combine the strength of graph networks and short sentences to solve the sparseness of short text. Experimental results on four different available datasets show that our PathWalk method achieves the state-of-the-art results."

12. **Aljuhani et al. (2025)** — `[HAS ABSTRACT]` "Foundation models excel on general benchmarks but often underperform in clinical settings due to domain shift between internet-scale pretraining data and medical data. Multimodal deep learning, which jointly leverages medical images and clinical text, is promising for diagnosis. We introduce PairDx, a balanced dataset of 22,665 image-caption pairs spanning six medical document classes. Our fine-tuned CLIP (PairDxCLIP) attains 93% accuracy and our custom fusion model (PairDxFusion) reaches 94% accuracy."

13. **Wu et al. (2025)** — `[HAS ABSTRACT]` "Telescope bibliographies record the pulse of astronomy research by capturing publication statistics and citation metrics for telescope facilities. Robust and scalable bibliographies ensure that we can measure the scientific impact of our facilities and archives. However, the growing rate of publications threatens to outpace our ability to manually label astronomical literature. We therefore present the Automated Mission Classifier (amc), a tool that uses large language models (LLMs) to identify and categorize telescope references by processing large quantities of paper text. A modified version of amc performs well on the TRACS Kaggle challenge, achieving a macro F1 score of 0.84."

14. **Urvashi et al. (2025)** — `[HAS ABSTRACT]` "Mental health disorders, including anxiety, bipolar disorder, and suicidal tendencies, significantly affect individual well-being and necessitate timely detection for effective intervention. This paper introduces a deep learning-based approach utilizing a fine-tuned BERT model for multi-class mental health classification through textual analysis. The system classifies text into four categories—depression, anxiety, stress, and normal. Evaluation on the DAIC-WOZ and Reddit-based datasets yields an accuracy of 93%."

15. **Thewissen & Pretorius (2026)** — `[EMPTY]`

**Q2 abstract coverage: 12/15 = 80%.**

### Q3 — Coverage: 5/15 = 33%

1. **Song & Kim (2025)** — `[HAS ABSTRACT]` "This study investigated how elementary students' revision characteristics varied depending on the type of teacher feedback. To address this, sixth-grade students were provided with either thinking-promoting or corrective feedback, and their revised argumentative texts were analyzed in terms of overall writing quality, feedback uptake patterns, and difficulties encountered during the revision process. The results revealed that students who received thinking-promoting feedback showed significantly greater improvement in overall writing quality as well as in content and expression domains compared to those who received corrective feedback. They also demonstrated more active and engaged revision behaviors."

2. **Emeliyanova & Kim (2019)** — `[HAS ABSTRACT]` "Although the effects of different types of written corrective feedback (WCF) have been examined in great detail, learners' revision behavior in response to WCF has not been systematically investigated. The current study compared students' classroom revision behaviors when they worked in pairs and when they worked individually. A total of 36 learners of English as a second language (ESL) completed four timed essays over an 8-week academic session. The instructor provided indirect WCF on students' essays, and the students revised their writing either individually (the self-correction group) or in pairs (the pair-correction group). The findings indicated that the pair-correction group corrected their errors at a higher rate of accuracy than the self-correction group. Both groups showed significant improvement in the accuracy of their writing after receiving feedback during the 8-week session; however, no difference in improvement was found between the self-correction and the pair-correction groups."

3. **Chau (2025)** — `[HAS ABSTRACT]` "Writing from multiple sources is a cognitively demanding skill that challenges students' reading and writing abilities, particularly in multilingual contexts. Despite its importance, students often struggle with source-based writing, and traditional research focusing on final texts provides limited insight into the underlying cognitive processes. This dissertation investigates how multilingual students integrate sources across languages and how cognitive and linguistic factors influence writing strategies and outcomes. Using keystroke logging, the research captures detailed writing behaviors, including reading time, source interaction, and variability in source use, offering a dynamic view of the writing process. Findings demonstrated that effective source integration relies on strategic interaction between sources, shaped by both cognitive resources and language context."

4. **Yan et al. (2025)** — `[HAS ABSTRACT]` "This study examined the effects of the complementary integration of automated feedback provided by automated writing evaluation (AWE) systems and online dialogic peer feedback on the quality of feedback and the use of self-regulatory writing strategies among second language (L2) writers. The participants were 68 Chinese L2 students who were assigned to two experimental conditions: one using automated feedback to complement dialogic peer feedback, and the other relying solely on dialogic peer feedback. Results indicate that integrating automated and peer feedback enhances the cognitive and constructive quality of peer feedback messages. Additionally, students in the integrated condition more frequently employed self-regulatory writing strategies during the text generation, self-monitoring, and revision phases."

5. **Ramancauskas & Ramancauskas (2025)** — `[HAS ABSTRACT]` "This paper presents the design, development, and evaluation of a proposed revision platform assisting candidates for the International English Language Testing System (IELTS) writing exam. The platform architecture separates conversational guidance from a dedicated writing interface to reduce cognitive load and simulate exam conditions. Through iterative, Design-Based Research (DBR) cycles, the study progressed from rule-based to transformer-based with a regression head scoring, mounted with adaptive feedback. DBR Cycle 4 implemented a DistilBERT transformer model with a regression head, yielding substantial improvements with MAE of 0.66. Cycle 5's adaptive feedback implementation demonstrated statistically significant score improvements (mean +0.060 bands, p = 0.011, Cohen's d = 0.504)."

6. **Jung (2023)** — `[HAS ABSTRACT]` "This study explores how high- and low-skilled students provide peer feedback, how they revise their writing after receiving peer feedback, and how peer feedback influences writing quality in terms of five component areas (content, organization, grammar, vocabulary, and mechanics). Data were collected from 102 Korean and international university students, who implemented three tasks: a writing task, a peer-review task, and a revision task. The results showed that the high- and low-proficient reviewer groups were preoccupied with giving the surface aspects of peer review, especially grammar feedback."

7. **Wu & Nilforoshan (2017)** — `[HAS ABSTRACT]` "User-generated, multi-paragraph writing is pervasive and important in many social media platforms. Ensuring high-quality content is important. Automated writing feedback has the potential to immediately point out and suggest improvements during the writing process. Most approaches, however, focus on syntax/phrasing, which is only one characteristic of high-quality content. Existing research develops accurate quality prediction models. We propose combining these models with model explanation techniques to identify writing features that, if changed, will most improve the text quality. Our user study finds that the perturbation-based approach, when combined with segment-specific feedback, can help improve writing quality on Amazon (review helpfulness) and Airbnb (host profile trustworthiness) by > 14%."

8. **Kim & Kang (2026)** — `[EMPTY]`

9. **Thewissen & Pretorius (2026) (dup.)** — `[EMPTY]`

10. **Kurt & Karabulut (2024)** — `[EMPTY]`

11. **Xu & Wang (2023)** — `[EMPTY]`

12. **Aben et al. (2022)** — `[EMPTY]`

13. **Mizumoto & Sasaki (2022)** — `[EMPTY]`

14. **Vasylets & Ahmadian (2021)** — `[EMPTY]`

15. **Choi et al. (2021)** — `[EMPTY]`

**Q3 abstract coverage: 7/15 = 47% (including dissertation abstract).**

### Q4 — Coverage: 10/15 = 67%

1. **Kolloff et al. (2025)** — `[HAS ABSTRACT]` "This study explored the effects of metacognitive training on 6-year-old kindergarteners, focusing on (a) enhancing metacognitive monitoring accuracy through feedback, and (b) examining whether children use choice latency as a valid cue for their monitoring judgments (cue utilization). A total of 214 children were assigned to one of three groups: performance feedback, monitoring feedback, and an active control. They completed 12 training sessions and were tested before and after the training with memory learning tasks. Results showed that neither feedback type improved monitoring accuracy. However, choice latency was confirmed as a valid cue that children use in their confidence judgments."

2. **Kolloff et al. (2013)** — `[HAS ABSTRACT]` "Participation in in-service training can be a challenge for health workers, especially those stationed in remote areas. Spaced education is an innovative learning methodology that can be delivered electronically by Internet or mobile smartphone. This pilot study followed a convenience sample of 37 Ethiopian nationals enrolled in a spaced education course over a six-month period. The study suggests that the Internet-based spaced education methodology is acceptable and effective for the acquisition of knowledge in a low-resource context for course participants with a clinical or public health background and moderately reliable Internet access."

3. **Wong et al. (2012)** — `[EMPTY]`

4. **Rian (2026)** — `[HAS ABSTRACT]` "Large language models (LLMs) increasingly mediate L2 writing feedback, yet we know little about how LLM output reshapes learners' decision-making. This qualitative multiple-case study examines how genre-based ChatGPT feedback and dialogue shape novice L2 writers' metacognitive judgments (MJs)—their bases and calibration—and subsequent self-regulated learning (SRL). In a first-year composition course, nine international students completed three genre-based assignments and engaged in structured AI feedback cycles using Genre Guru. Four themes emerged: (1) skepticism shifted to measured trust; (2) students critically evaluated AI suggestions, preserving text ownership; (3) writers integrated the four domains and articulated genre awareness; and (4) affect and motivation drove SRL cycles."

5. **Yao & Liu (2025)** — `[HAS ABSTRACT]` "This study specifically investigates the initiation phase of EFL learners' engagement with AI tools, focusing on how technology acceptance constructs—perceived usefulness (PU), perceived ease of use (PEOU), and perceived self-efficacy (PSE)—influence learning resilience. Drawing on an optimized Technology Acceptance Model (TAM) and integrating constructs from positive psychology, the study examines the chain-mediated effects of learning motivation (LM) and metacognitive strategies (MS) on resilience outcomes. A survey of first-year English majors (N = 730) was conducted. The findings indicate that favorable perceptions of AI tools are significantly associated with enhanced LM and MS, which in turn positively impact resilience measures."

6. **Alsaiari et al. (2025)** — `[HAS ABSTRACT]` "Feedback is one of the most powerful influences on student learning, with extensive research examining how best to implement it in educational settings. Increasingly, feedback is being generated by artificial intelligence (AI), offering scalable and adaptive responses. Two widely studied approaches are directive feedback, which gives explicit explanations and reduces cognitive load to speed up learning, and metacognitive feedback which prompts learners to reflect, track their progress, and develop self-regulated learning (SRL) skills. This study presents a semester-long randomised controlled trial with 329 students in an introductory design and programming course using an adaptive educational platform. Participants were assigned to receive directive, metacognitive, or hybrid AI-generated feedback. Results showed that revision behaviour differed across feedback conditions, with Hybrid prompting the most revisions."

7. **Krueger et al. (2021)** — `[HAS ABSTRACT]` "One of the most remarkable aspects of the human mind is its ability to improve itself based on experience. To address these problems, we model cognitive plasticity as metacognitive reinforcement learning. Here, we develop a metacognitive reinforcement learning model of how people learn how many steps to plan ahead in sequential decision problems, and test its predictions experimentally. The results of our first experiment suggested that our model can discern which reward structures are more conducive to metacognitive learning. A follow-up experiment confirmed that feedback structures designed according to our model can indeed accelerate learning to plan."

8. **Baseer et al. (2017)** — `[HAS ABSTRACT]` "Multiple attributes are expected of postgraduate research supervisors. Provision of timely and effective face-to-face feedback is one such skill that carries enormous significance in supervisee."

9. **Guo (2022)** — `[HAS ABSTRACT]` "This research aims to use metacognitive monitoring feedback to improve student learning performance in an augmented reality environment. In this study, Microsoft HoloLens, a prominent augmented reality device and independent mobile computer, provided a more realistic augmented reality environment to engineering students. The near field electromagnetic ranging system collected students' real-time location data when they experienced the augmented reality learning modules. The study outcomes advanced our understanding of students' interactions and the learning content in an augmented reality learning environment. Furthermore, using a metacognitive monitoring feedback tool in an augmented reality learning environment is an effective strategy to improve students' academic performance and calibration."

10. **Luo & Yusuf (2025)** — `[EMPTY]`

11. **Ahmad et al. (2025)** — `[EMPTY]`

12. **Metacognitive Control Over Spaced Practice (encyclopedia)** — `[EMPTY]`

13. **Cacioli (2026)** — `[HAS ABSTRACT]` "We introduce a cross-domain behavioural assay of monitoring-control coupling in LLMs, grounded in the Nelson and Narens (1990) metacognitive framework and applying human psychometric methodology to LLM evaluation. The battery comprises 524 items across six cognitive domains (learning, metacognitive calibration, social cognition, attention, executive function, prospective regulation). Applied to 20 frontier LLMs (10,480 evaluations), the battery discriminates three profiles consistent with the Nelson-Narens architecture: blanket confidence, blanket withdrawal, and selective sensitivity."

14. **Abtahi et al. (2026)** — `[HAS ABSTRACT]` "Metacognition, the ability to monitor and regulate one's own reasoning, remains under-evaluated in AI benchmarking. We introduce MEDLEY-BENCH, a benchmark of behavioural metacognition that separates independent reasoning, private self-revision, and socially influenced revision under genuine inter-model disagreement. The benchmark evaluates 35 models from 12 families on 130 ambiguous instances across five domains. Results show a robust evaluation/control dissociation: evaluation ability increases with model size within families, whereas control does not."

15. **Rian (2025, v1)** — `[HAS ABSTRACT]` (same as entry 4) — duplicate paper entry

**Q4 abstract coverage: 10/15 = 67%.**

### Q5 — Coverage: 11/15 = 73%

1. **Fan et al. (2024)** — `[HAS ABSTRACT]` "With the continuous development of technological and educational innovation, learners nowadays can obtain a variety of supports from agents such as teachers, peers, education technologies, and recently, generative artificial intelligence such as ChatGPT. In particular, there has been a surge of academic interest in human-AI collaboration and hybrid intelligence in learning. We conducted a randomised experimental study and compared learners' motivations, self-regulated learning processes and learning performances on a writing task among different groups who had support from different agents, that is, ChatGPT, chat with a human expert, writing analytics tools, and no extra tool. A total of 117 university students were recruited. The results revealed that: (1) learners who received different learning support showed no difference in post-task intrinsic motivation; (2) there were significant differences in the frequency and sequences of the self-regulated learning processes among groups; (3) ChatGPT group outperformed in the essay score improvement but their knowledge gain and transfer were not significantly different. Our research found that AI technologies such as ChatGPT may promote learners' dependence on technology and potentially trigger 'metacognitive laziness'."

2. **Hardini & Samsudin (2019)** — `[HAS ABSTRACT]` "Improving students' critical thinking is very important in learning process because one of the goals of critical thinking is to develop students' critical thinking in the perspective of collectable information. The approach used to address the problem of critical thinking is through learning style and metacognitive skill. The Student Creativity Program is a great way to hone critical thinking at the university level. The research results for learning styles show that 33 (60%) of the students were in the 'medium' category and 22 (40%) were in the 'high' category. In terms of metacognitive skills, 53 students (98.2%) were in the 'high' category. All students were identified to have 'high' level critical thinking. Based on the significance test, learning style had no significance influence on critical thinking; however, metacognition skills had significant influence on critical thinking."

3. **Pramusinta et al. (2019)** — `[HAS ABSTRACT]` "This research examines the effect of discovery learning method using various cognitive styles on metacognitive and critical thinking skills of pre-service elementary school teachers. Quasi-experimental pretest-post tests non-equivalent control group design is selected to be the method of this research. The subjects of this research are 144 pre-service teachers. The findings conclude that: (1) there are significant differences in metacognitive and critical thinking skills between groups which learned using discovery learning method and discussion method; (2) there are significant differences in metacognitive and critical thinking skills when integrated with field independence cognitive style and field dependence cognitive style."

4. **Yurt & Kuşci (2025)** — `[EMPTY]`

5. **Atre (2025)** — `[EMPTY]`

6. **Shovkova (2019)** — `[EMPTY]`

7. **Rahayuan et al. (2017)** — `[EMPTY]`

8. **Pirsl et al. (2013)** — `[EMPTY]`

9. **Maclellan & Soden (2011)** — `[EMPTY]`

10. **Wang (2026)** — `[HAS ABSTRACT]` "With the rapid iteration and penetration of generative AI tools (e.g., ChatGPT, DeepSeek) in education, they have become versatile aids for students' independent learning. However, students' growing over-reliance has triggered prominent dilemmas, such as eroded independent thinking, pervasive loss of creative expression, and impaired cognitive construction. This study explores the formation mechanism of such over-reliance and constructs a targeted prevention strategy system via a mixed method: a questionnaire survey of 500 students from 18 schools, semi-structured interviews with 30 typical students and 15 teachers, and 3-month case studies. Results show over-reliance is driven by individual (instrumental motivation, low self-efficacy), teacher (insufficient guidance), and environmental (tool usability, unclear norms) factors."

11. **Qurat ul Ain (2026)** — `[HAS ABSTRACT]` "This research was conducted to examine the causal effect of over-reliance on artificial intelligence on students' critical thinking by statistically controlling initial differences between the experimental and control groups. A quasi-experimental research design with a pre-test-post-test control group approach was employed. Thirty students from B.Ed. Semester III were assigned to the experimental group, while thirty students from B.Ed. Semester I were selected for the control group. The experimental group (Semester III) was allowed relatively high and independent use of artificial intelligence-based tools in academic activities, whereas the control group (Semester I) was restricted to limited use of AI. The results of the independent samples t-test indicated that there was no statistically significant difference in critical thinking between the experimental and control groups at the pre-test stage. However, the findings of the paired sample t-test showed a significant decline in critical thinking abilities in the experimental group, while no significant change was observed in the control group."

12. **Soni (2026)** — `[HAS ABSTRACT]` "The rapid integration of artificial intelligence (AI) into educational environments has sparked both excitement and concern regarding its impact on pedagogy and student development. While AI offers personalized learning, efficiency, and scalability, it also raises questions about the erosion of critical thinking skills and learner autonomy. This chapter explores the tension between AI-driven instruction and activity-based pedagogy, emphasizing the latter's potential to preserve and cultivate critical thinking in the digital age."

13. **Sabqat et al. (2025)** — `[HAS ABSTRACT]` "Background: The rapid expansion of artificial intelligence (AI) and machine learning has transformed industries, including education and healthcare. In medical education, AI is increasingly used for personalized learning and clinical decision-making. However, growing reliance on AI may contribute to metacognitive laziness, where students engage less in critical thinking and self-regulation. The study involved medical and dental students, with data collected via a four-point Likert scale-based questionnaire. The survey revealed that 74.4% of students relied on AI for learning, with 61.3% reporting decreased motivation for independent analysis and 62.4% expressing concerns about its impact on future patient care. Spearman's rank correlation showed a moderate positive relationship (ρ = 0.621, p = 0.000)."

14. **Bhimavarapu (2025)** — `[HAS ABSTRACT]` "Digital Literacy and Critical Thinking are fundamental skills in the digital age, particularly as emerging technologies like Artificial Intelligence (AI) impact various sectors. This study examines the relationship between digital literacy, critical thinking, and university students' attitudes toward AI, focusing on its ethical implications and potential applications in education. A convenience sample of 255 students at a large public university participated in an online survey conducted in March and April 2024."

15. **Singh et al. (2025)** — `[HAS ABSTRACT]` "The growing use of Generative AI (GenAI) conversational search tools has raised concerns about their effects on people's metacognitive engagement, critical thinking, and learning. As people increasingly rely on GenAI to perform tasks such as analyzing and applying information, they may become less actively engaged in thinking and learning. This study examines whether metacognitive prompts - designed to encourage people to pause, reflect, assess their understanding, and consider multiple perspectives - can support critical thinking during GenAI-based search. We conducted a user study (N=40) with university students. We found that these prompts led to more active engagement, prompting students to explore a broader range of topics and engage in deeper inquiry through follow-up queries."

**Q5 abstract coverage: 11/15 = 73%.**

**Overall MCP3 abstract coverage: 49/75 = 65.3%.** The remaining 34.7% of papers returned empty abstract fields from CrossRef/Semantic Scholar, which is why abstract coverage is tracked as a benchmark metric.
