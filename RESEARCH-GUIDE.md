# Research Guide for Future Coding Agents

> How this research was conducted and how to update it going forward.

---

## How This Research Was Conducted

### Architecture: 5 Parallel Subagents

Each analysis was built using **5 concurrent research subagents**, each focused on a different domain:

1. **Pricing Agent** — Searches all provider pricing pages, aggregates per-token costs
2. **Benchmark Agent** — Scrapes SWE-bench, Aider, LMSYS Arena, Artificial Analysis, BenchLM
3. **Community Agent** — Searches Reddit, DEV.to, YouTube, GitHub issues for real-world experiences
4. **Value Agent** — Calculates intelligence/$ ratios, identifies sweet spot models
5. **Features Agent** — Context windows, caching, speed, tool use, batch discounts

### Research Process

```
1. User request arrives
2. Identify research domains (pricing, benchmarks, features, community, value)
3. Spin up N subagents in parallel (task tool, subagent_type: "general")
4. Each agent:
   a. Searches web with multiple queries
   b. Fetches authoritative URLs directly
   c. Cross-references multiple sources
   d. Returns structured data with source URLs
5. Compile agent results into unified analysis
6. Generate HTML (interactive) + Markdown (GitHub-friendly) outputs
7. Commit to this repo
```

### Key Search Queries That Work

For **pricing**:
- "LLM pricing 2026", "AI model pricing comparison"
- Direct URLs: `anthropic.com/pricing`, `platform.openai.com/docs/pricing`
- `benchlm.ai/llm-pricing` (aggregator)

For **benchmarks**:
- "SWE-bench leaderboard August 2026"
- Direct: `swebench.com`, `aider.chat/docs/leaderboards/`, `lmarena.ai/leaderboard`
- `artificialanalysis.ai/leaderboards/models`
- `benchlm.ai/coding`

For **community sentiment**:
- "best model for opencode reddit"
- "opencode go review"
- site:dev.to opencode model
- site:youtube.com opencode go review

For **local LLMs**:
- "RTX 5060 Ti llama.cpp benchmark"
- "best local coding LLM 16GB VRAM 2026"
- "ollama coding model recommendation"
- Direct: `ollama.ai/library`

---

## How to Update This Research

### When to Update

| Trigger | What to Update |
|---------|---------------|
| New model release | Add to pricing table, run benchmarks section |
| Price change | Update pricing tables, recalculate value ratios |
| New benchmark scores | Update leaderboard sections |
| OpenCode Go model change | Update Go section |
| New quantization method | Update local LLM section |
| Quarterly (minimum) | Full refresh of all sections |

### Step-by-Step Update Process

#### 1. Check for New Models
```bash
# Search for recent releases
Search: "AI model release [month] [year]"
Search: "new LLM [month] [year]"
Check: https://aireleasetracker.com/latest
```

#### 2. Update Pricing
```bash
# Fetch current pricing from each provider
Fetch: https://www.anthropic.com/pricing
Fetch: https://platform.openai.com/docs/pricing
Fetch: https://opencode.ai/docs/zen/
Fetch: https://opencode.ai/docs/go/
```

#### 3. Update Benchmarks
```bash
# Check each leaderboard
Fetch: https://benchlm.ai/coding
Fetch: https://lmarena.ai/leaderboard
Fetch: https://artificialanalysis.ai/leaderboards/models
Fetch: https://aider.chat/docs/leaderboards/
Fetch: https://swebench.com/
```

#### 4. Recalculate Value Ratios
```
Intelligence/$ = Normalized Score / Output Price per 1M tokens
% of Leader = Model Score / Leader Score * 100
Sweet Spot = Models with >= 80% intelligence at <= 20% price
```

#### 5. Update Local LLM Section
```bash
# Check for new open-source models
Search: "best local coding LLM [year]"
Check: https://ollama.ai/library
Check: https://huggingface.co/spaces/open-llm-leaderboard
# Check for new quantization methods
Search: "llama.cpp new quantization [year]"
# Check GPU benchmarks
Search: "RTX 5060 Ti llama.cpp benchmark [year]"
```

#### 6. Generate Outputs
- Update HTML files (interactive, visual)
- Update Markdown files (GitHub-friendly)
- Update this guide if process changes
- Commit with descriptive message

---

## File Structure

```
AI-Tools-Benchmark-for-Opencode/
├── README.md                          # This repo overview
├── RESEARCH-GUIDE.md                  # This file
├── opencode-model-analysis.md         # Cloud models (Markdown)
├── opencode-model-analysis.html       # Cloud models (HTML)
├── local-llm-for-opencode.md          # Local LLMs (Markdown)
└── local-llm-for-opencode.html        # Local LLMs (HTML)
```

---

## Data Sources Reference

### Pricing Sources
| Source | URL | Update Frequency |
|--------|-----|-----------------|
| Anthropic | anthropic.com/pricing | On release |
| OpenAI | platform.openai.com/docs/pricing | On release |
| OpenCode Zen | opencode.ai/docs/zen | On change |
| OpenCode Go | opencode.ai/docs/go | On change |
| BenchLM | benchlm.ai/llm-pricing | Aggregator |

### Benchmark Sources
| Source | URL | What It Measures |
|--------|-----|-----------------|
| SWE-bench | swebench.com | Real-world software engineering |
| Aider | aider.chat/docs/leaderboards | Multi-language code editing |
| LMSYS Arena | lmarena.ai/leaderboard | Human preference Elo |
| Artificial Analysis | artificialanalysis.ai | Intelligence index + speed |
| BenchLM | benchlm.ai/coding | Composite coding score |

### Community Sources
| Source | URL | What to Search |
|--------|-----|---------------|
| Reddit | reddit.com/r/opencode | Model experiences |
| DEV.to | dev.to | Technical reviews |
| YouTube | youtube.com | Video reviews |
| GitHub | github.com/anomalyco/opencode | Issues, discussions |

### Local LLM Sources
| Source | URL | What It Provides |
|--------|-----|-----------------|
| Ollama | ollama.ai/library | Model catalog |
| HuggingFace | huggingface.co | Model weights, benchmarks |
| llama.cpp | github.com/ggml-org/llama.cpp | Inference engine |
| r/LocalLLaMA | reddit.com/r/LocalLLaMA | Community benchmarks |

---

## Tips for High-Quality Research

1. **Always use multiple subagents in parallel** — different agents find different things
2. **Fetch authoritative URLs directly** — don't rely solely on search snippets
3. **Cross-reference at least 2 sources** for every data point
4. **Include source URLs** in all outputs for verifiability
5. **Distinguish measured vs estimated** data clearly
6. **Note the date** on all data — LLM landscape changes weekly
7. **Search for the negative** — "model X problems" reveals real-world issues
8. **Check community sentiment** — benchmarks don't capture everything
9. **Calculate derived metrics** — intelligence/$ is more useful than raw scores
10. **Always note limitations** — what the data doesn't tell you
