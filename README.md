# AI Tools Benchmark for OpenCode

> Comprehensive, data-driven analysis of AI models for [opencode](https://opencode.ai) — cloud and local.

**Last updated: August 19, 2026**

---

## What's In Here

| File | What It Covers |
|------|---------------|
| [opencode-model-analysis.md](./opencode-model-analysis.md) | Cloud models, pricing, benchmarks, OpenCode Go |
| [opencode-model-analysis.html](./opencode-model-analysis.html) | Interactive HTML version with visualizations |
| [local-llm-for-opencode.md](./local-llm-for-opencode.md) | Local LLMs for RTX 5060 Ti 16GB + 64GB RAM |
| [local-llm-for-opencode.html](./local-llm-for-opencode.html) | Interactive HTML version with visualizations |
| [RESEARCH-GUIDE.md](./RESEARCH-GUIDE.md) | How this research was conducted + update guide |

---

## Quick Answers

### "What model should I use with OpenCode?"

**If you have OpenCode Go ($10/mo):**
- Daily driver: **GPT-5.6 Luna** (~10,250 req/mo, 93% of frontier)
- Complex tasks: **Kimi K3** (~490 req/mo, frontier quality)
- Quick fixes: **DeepSeek V4 Flash** (~37,800 req/mo)

**If you use your own API keys:**
- Best value: **GPT-5.6 Luna** ($1.20/1M output, 93% of frontier)
- Cheapest capable: **DeepSeek V4 Pro** ($0.87/1M output, 78% of frontier)
- Maximum quality: **Claude Opus 5** ($25/1M output, 100% frontier)

**If you want to run locally (RTX 5060 Ti 16GB):**
- Daily driver: **Qwen 3.6 35B-A3B** (~100 tok/s, ~88% of frontier)
- Autocomplete: **Qwen 2.5 Coder 14B** (~34 tok/s, best FIM)
- Max quality: **Qwen3-Coder 32B** (~22 tok/s, partial offload)

### "What's the sweet spot?"

| Model | Intelligence | Price | Sweet Spot? |
|-------|-------------|-------|-------------|
| GPT-5.6 Luna | 93% | $1.20/1M (or free in Go) | Best overall value |
| DeepSeek V4 Pro | 78% | $0.87/1M (or free in Go) | Cheapest capable |
| Gemini 3.7 Flash | 85% | $3.75/1M | Best speed + value |
| Grok 4.5 | 96% | $6.00/1M (or free in Go) | Near-frontier cheap |

---

## How to Update

See [RESEARCH-GUIDE.md](./RESEARCH-GUIDE.md) for the full process. TL;DR:

1. Spin up 5 parallel subagents (pricing, benchmarks, community, value, features)
2. Each searches the web and fetches authoritative URLs
3. Compile results into unified analysis
4. Update HTML + Markdown files
5. Commit with descriptive message

---

## Sources

- [opencode.ai](https://opencode.ai) — OpenCode docs, Zen, Go
- [benchlm.ai](https://benchlm.ai) — Coding leaderboard
- [lmarena.ai](https://lmarena.ai) — LMSYS Arena
- [artificialanalysis.ai](https://artificialanalysis.ai) — Intelligence Index
- [aider.chat](https://aider.chat) — Aider benchmarks
- [swebench.com](https://swebench.com) — SWE-bench
- [ollama.ai](https://ollama.ai) — Local model library
