# research-mcp

A bundled MCP server that unifies academic research tools into one compact tool surface. Combines 21+ academic sources, citation graph walking, full-text PDF extraction, and smart query expansion into a single MCP server designed for LLM agents.

## The Problem

LLMs waste tokens and make poor tool selections when drowning in redundant MCP tools. Research from [Wang et al. 2026](https://arxiv.org/abs/2602.18914) (10,831 MCP servers studied) found:

- **73% of MCP servers** have repeated tool names across servers
- **+260% selection probability** when tool descriptions are clear and non-redundant
- **Linear context growth** — each additional MCP server adds ~3,000-5,000 tokens of tool descriptions to the context window

The three upstream academic MCPs (`academix`, `paper-search-mcp`, `paper-distill-mcp`) provide overlapping search capabilities across 43+ combined tools. This bundle merges them into **11 curated tools** — a 75% reduction in tool surface area while preserving full capability.

## What This Bundle Does

| Tool | What It Does | Sources |
|---|---|---|
| `search_literature` | Federated search across 8-21 backends with dedup, query expansion, and auto-citation walking | Academix + Paper Search |
| `paper_lookup` | Paper details by DOI, arXiv ID, OpenAlex ID, or Semantic Scholar ID | Academix + CrossRef |
| `citation_intelligence` | Citing papers, references, related work, or full citation network graph | Academix (Semantic Scholar) |
| `walk_citations` | Multi-hop citation chain walker (follow citation graphs N hops deep) | Academix |
| `author_literature` | Find all papers by a specific author with year filters | Academix |
| `export_bibliography` | BibTeX export with LaTeX-aware escaping and DBLP native lookup | Academix |
| `search_specific_sources` | Direct source control — pick exactly which databases to query | Paper Search |
| `read_paper` | Full-text PDF download + text extraction from 11+ open-access sources | Paper Search |
| `batch_read` | Concurrent full-text extraction for multiple papers | Paper Search |
| `curate_research` | Paper ranking, dedup filtering, review prompt generation | Paper Distill |
| `paper_distill_pipeline` | Session management, topic preferences, Zotero collection, push digests | Paper Distill |

## Architecture

```
┌─────────────────────────────────────────────────┐
│              research_bundle.py                  │
│         Single FastMCP server process            │
├─────────────┬──────────────┬────────────────────┤
│  Academix   │ Paper Search │   Paper Distill    │
│  metadata   │ 21+ sources  │   curation         │
│  citations  │ PDF download │   ranking          │
│  BibTeX     │ text extract │   digests          │
│  networks   │ Sci-Hub/OA   │   Zotero           │
└─────────────┴──────────────┴────────────────────┘
```

The bundle uses `sys.path` injection to import from all three upstream packages in a single Python process. No subprocesses, no IPC — just direct function calls.

## Sources (21+)

| Category | Sources |
|---|---|
| **Preprint servers** | arXiv, bioRxiv, medRxiv, IACR ePrint |
| **Academic databases** | Semantic Scholar, OpenAlex, CrossRef, DBLP, PubMed, PMC, EuropePMC, CORE |
| **Open access** | OpenAIRE, DOAJ, BASE, Unpaywall |
| **Archives** | HAL, Zenodo, SSRN, CiteSeerX |
| **Search engines** | Google Scholar |

## Features

### Smart Search
- **Query expansion**: Automatically expands acronyms (`LLM` → `large language model`, `RAG` → `retrieval augmented generation`, etc.)
- **Cross-source deduplication**: Papers found by multiple sources are ranked higher
- **Auto-citation walking**: Automatically follows citation graphs for top results to discover related work
- **Profile system**: `fast` (8 best sources, ~3s) or `broad` (all 21 sources, ~10s)

### Full-Text Access
- **11 source-specific readers**: arXiv, Semantic Scholar, bioRxiv, medRxiv, IACR, OpenAIRE, CiteSeerX, DOAJ, BASE, Zenodo, HAL
- **Smart fallback cascade**: Tries source-native → OA repositories → Unpaywall → (optional Sci-Hub)
- **PDF text extraction**: Uses `pypdf` for page-by-page extraction

### Citation Analysis
- **Citation intelligence**: Citing papers, references, related work in one call
- **Multi-hop walking**: Follow citation chains N hops deep (forward, backward, or both)
- **Network graphs**: JSON graph format with nodes and edges for visualization

### Curation Pipeline
- **Paper ranking**: 4-factor scoring (relevance, recency, impact, novelty)
- **Topic management**: Configure research interests with weighted keywords
- **Push digests**: Send daily/weekly digests to Telegram, Discord, Feishu, or WeCom
- **Zotero integration**: Collect papers with full metadata enrichment

## Installation

### Option 1: uv tool install (recommended)

```bash
# Install the three upstream servers
uv tool install academix
uv tool install paper-search-mcp
uv tool install paper-distill-mcp

# Clone and install this bundle
git clone https://github.com/chessy795/research-mcp.git
cd research-mcp
pip install -e .
```

### Option 2: Direct download

```bash
# Install dependencies
pip install academix paper-search-mcp paper-distill-mcp fastmcp

# Download research_bundle.py and place it anywhere
```

## Configuration

### opencode

Add to your `opencode.json`:

```json
{
  "mcp": {
    "research": {
      "type": "local",
      "command": ["python", "/path/to/research_bundle.py"],
      "env": {
        "UNPAYWALL_EMAIL": "your@email.com",
        "SEMANTIC_SCHOLAR_API_KEY": "optional"
      },
      "enabled": true
    }
  }
}
```

### Claude Desktop

Add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "research": {
      "command": "python",
      "args": ["/path/to/research_bundle.py"],
      "env": {
        "UNPAYWALL_EMAIL": "your@email.com"
      }
    }
  }
}
```

### Any MCP Client

The server runs on stdio transport. Point your MCP client at:

```bash
python /path/to/research_bundle.py
```

## Environment Variables

| Variable | Required | Description |
|---|---|---|
| `UNPAYWALL_EMAIL` | Recommended | Email for Unpaywall OA resolution. Use your institutional email for better access to paywalled papers. |
| `SEMANTIC_SCHOLAR_API_KEY` | Optional | Higher rate limits for Semantic Scholar (free key at [api.semanticscholar.org](https://api.semanticscholar.org/)) |

## Usage Examples

### Basic literature search

The model will call `search_literature` automatically. Key parameters:

```
query: "retrieval augmented generation"
profile: "fast"           # 8 sources, fast
expand_queries: true      # auto-expand "RAG" → "retrieval augmented generation"
auto_cite_walk: true      # follow citation graph for top 3 results
```

### Find papers by author

```
author_literature(author_name="Yann LeCun", year_from=2020)
```

### Read a paper's full text

```
read_paper(paper_id="2305.14283")  # arXiv ID auto-detected
read_paper(paper_id="10.1038/s41586-020-2649-2", source="auto")  # DOI
```

### Walk citation chains

```
walk_citations(
    paper_id="2305.14283",
    direction="forward",    # who cited this paper?
    depth=2,                # 2 hops deep
    max_papers_per_hop=10
)
```

### Export BibTeX

```
export_bibliography(paper_ids=["2305.14283", "10.1038/s41586-020-2649-2"])
```

## Tool Comparison

| Capability | Separate MCPs (3 servers) | This Bundle (1 server) |
|---|---|---|
| Tool count | 43+ tools | 11 tools |
| Context tokens | ~15,000 | ~4,000 |
| Search sources | 21+ | 21+ (same) |
| Cross-source dedup | Manual | Automatic |
| Citation walking | Manual (separate calls) | Auto (built into search) |
| Query expansion | None | Built-in |
| Process count | 3 | 1 |
| Tool selection accuracy | Lower (redundant names) | Higher (unique names) |

## Research Basis

This bundle design is informed by:

- **Wang et al. 2026** — ["From Docs to Descriptions"](https://arxiv.org/abs/2602.18914) — MCP description quality study of 10,831 servers. Found that 73% have repeated tool names and clear descriptions give +260% selection probability.
- **Dunkel 2026** — [DADL](https://arxiv.org/abs/2605.05247) — Progressive tool disclosure for token efficiency. Demonstrated linear context growth with tool count.
- **Hou et al. 2026** — ["MCP Landscape"](https://arxiv.org/abs/2504.14947) — Security threats and future directions for MCP. Identified 16 threat scenarios across 4 categories.

## Upstream Packages

| Package | What It Provides | License |
|---|---|---|
| [academix](https://pypi.org/project/academix/) | Metadata, citations, BibTeX, citation networks | MIT |
| [paper-search-mcp](https://pypi.org/project/paper-search-mcp/) | 21+ source search, PDF download, text extraction | MIT |
| [paper-distill-mcp](https://pypi.org/project/paper-distill-mcp/) | Curation, ranking, digests, Zotero integration | MIT |

## Contributing

Contributions welcome. The bundle is intentionally thin (~740 lines) — it delegates to upstream packages. Changes should keep the tool surface compact.

## License

MIT
