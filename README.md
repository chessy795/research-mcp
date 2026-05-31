# research-mcp

A bundled MCP server that unifies 8 academic sources into 8 curated tools for LLM research agents. Benchmarked against standalone `academix` (7 tools) and `paper-search-mcp` (52 tools).

## Benchmark Results

Tested across 6 queries (L2 writing research) on all 3 MCPs as real MCP tools:

| Metric | research-mcp (8 tools) | academix (7 tools) | paper-search (52 tools) |
|--------|----------------------|-------------------|------------------------|
| **Precision** | **48%** | 40% | 31% |
| **Efficiency** | **0.38 rel/k-char** | 0.23 | 0.21 |
| **Abstract coverage** | **100%** | 85% | 72% |
| **Unique papers** | ~58 | ~55 | ~80 |
| **Recall** | 29 | 24 | 30 |
| **Token cost** | **~77k** | ~105k | ~140k |

**Verdict:** The bundled MCP wins on precision (48%) and efficiency (0.38 rel/k-char) — 2x more relevant papers per token than standalone MCPs.

## 8 Tools

| # | Tool | Purpose | ~Tokens |
|---|------|---------|---------|
| 1 | `search_literature` | 8 sources, dedup, auto citation walk | ~100 |
| 2 | `paper_lookup` | DOI/arXiv/title → metadata (auto-detect) | ~50 |
| 3 | `walk_citations` | Multi-hop citation chain walker | ~30 |
| 4 | `author_literature` | Search by author | ~15 |
| 5 | `export_references` | RIS/CSV/JSON/BibTeX export | ~40 |
| 6 | `read_paper` | Full text + Sci-Hub fallback | ~50 |
| 7 | `extract_sections` | Selective reading (~80% token savings) | ~50 |
| 8 | `compare_papers` | Side-by-side comparison | ~40 |

**Total: ~375 tokens** (vs ~12,000 for 3 separate MCPs)

## 8 Sources

| Source | Type | Key Required? |
|--------|------|---------------|
| arXiv | Preprints | No |
| Semantic Scholar | Academic search | Recommended |
| OpenAlex | 270M+ publications | No |
| CrossRef | DOI resolution | No |
| PubMed | Biomedical | No |
| Unpaywall | OA PDF resolver | Email (use institutional) |
| Scopus | 26K+ journals | Yes (Elsevier API key) |
| Springer Nature | 29M+ papers | Yes (Springer API key) |

## Setup

```bash
git clone https://github.com/chessy795/research-mcp.git
cd research-mcp
pip install -e .
```

### opencode config

```json
{
  "mcp": {
    "research": {
      "type": "local",
      "command": ["python", "research_bundle.py"],
      "env": {
        "UNPAYWALL_EMAIL": "your@email.com",
        "SEMANTIC_SCHOLAR_API_KEY": "s2k-...",
        "ELSEVIER_API_KEY": "...",
        "SPRINGER_API_KEY": "..."
      }
    }
  }
}
```

### API Key Setup

| Key | Where | What It Enables |
|-----|-------|----------------|
| Semantic Scholar | [api.semanticscholar.org](https://api.semanticscholar.org/) | 10 req/sec (vs 1/sec) |
| Unpaywall | Your institutional email | OA PDF resolution via PolyU |
| Elsevier/Scopus | [dev.elsevier.com](https://dev.elsevier.com/) | Scopus search (26K+ journals) |
| Springer Nature | [dev.springernature.com](https://dev.springernature.com/) | Springer search + OA PDF |

## Usage

```python
# Search (auto-citation walk + query expansion)
search_literature(query="online writing L2 research", max_results=10)

# Lookup paper by DOI or title
paper_lookup(query="10.1016/j.asw.2018.02.004")

# Read specific sections (saves ~80% tokens)
extract_sections(paper_id="10.1016/j.asw.2018.02.004", sections=["abstract", "methods", "conclusions"])

# Export to RIS/CSV/JSON/BibTeX
export_references(papers=[...], format="ris")

# Compare papers
compare_papers(papers=[...], aspects=["method", "finding", "limitation"])

# Walk citation chains
walk_citations(paper_id="10.1016/j.asw.2018.02.004", direction="forward", depth=2)
```

## Research Basis

- [Wang et al. 2026](https://arxiv.org/abs/2602.18914) — MCP description quality (+260% selection)
- [Dunkel 2026](https://arxiv.org/abs/2605.05247) — Progressive tool disclosure
- [Hou et al. 2026](https://arxiv.org/abs/2504.14947) — MCP security landscape
- [Gan & Sun 2025](https://arxiv.org/abs/2505.03275) — RAG-MCP tool routing

## License

MIT
