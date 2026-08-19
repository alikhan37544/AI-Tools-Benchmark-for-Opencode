# OpenCode Model Intelligence Analysis

> **Updated: August 19, 2026** | Cloud models, pricing, benchmarks, and OpenCode Go

## TL;DR

| Category | Model | Price (Output/1M) | Intelligence | Notes |
|----------|-------|-------------------|--------------|-------|
| **Most Intelligent** | Claude Opus 5 | $25.00 | 100% (leader) | SWE-bench 96% |
| **Best Value (BYOK)** | GPT-5.6 Luna | $1.20 | ~93% of leader | 4% of Opus price |
| **Cheapest Capable** | DeepSeek V4 Pro | $0.87 | ~78% of leader | 34x cheaper than Opus |
| **Best Go Model** | GPT-5.6 Luna | Included in $10/mo | ~93% | ~10,250 req/mo |
| **Fastest** | Gemini 3.7 Flash | $3.75 | ~85% | 344 tok/s |
| **Sweet Spot** | Grok 4.5 | $6.00 | ~96% | 96% of frontier at 24% price |

---

## OpenCode Go ($10/mo)

20 models included. $60/mo equivalent usage.

### Best Go Models Ranked

| Model | Intelligence | Req/Month | Use Case |
|-------|-------------|-----------|----------|
| **Kimi K3** | ~100% | ~490 | Reserve for critical tasks |
| **Grok 4.5** | ~96% | ~600 | Complex reasoning |
| **GPT 5.6 Luna** | ~93% | ~10,250 | **Daily driver** |
| **MiniMax M3** | ~88% | ~16,000 | High volume coding |
| **Qwen3.8 Max** | ~85% | ~810 | General reasoning |
| **GLM-5.2** | ~82% | ~4,300 | Most popular on Go |
| **DeepSeek V4 Pro** | ~78% | ~5,200 | Reasoning tasks |
| **DeepSeek V4 Flash** | ~66% | ~37,800 | Quick fixes |

### Go Usage Limits

| Window | Limit |
|--------|-------|
| 5-hour rolling | $12 |
| Weekly | $30 |
| Monthly | $60 |

### Recommended Go Config

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "opencode-go/gpt-5.6-luna",
  "small_model": "opencode-go/deepseek-v4-flash",
  "agent": {
    "build": { "model": "opencode-go/gpt-5.6-luna" },
    "plan": { "model": "opencode-go/kimi-k3" }
  }
}
```

---

## Full Pricing (Zen Pay-As-You-Go)

### Anthropic — Zen Only
| Model | Input/1M | Output/1M | Context |
|-------|----------|-----------|---------|
| Claude Fable 5 | $10.00 | $50.00 | 1M |
| Claude Opus 5 | $5.00 | $25.00 | 1M |
| Claude Sonnet 5 | $2.00 | $10.00 | 1M |
| Claude Haiku 4.5 | $1.00 | $5.00 | 200K |

### OpenAI — Luna in Go
| Model | Input/1M | Output/1M | Context | In Go? |
|-------|----------|-----------|---------|--------|
| GPT-5.6 Sol | $5.00 | $30.00 | 1.05M | No |
| GPT-5.6 Terra | $2.00 | $12.00 | 1.05M | No |
| **GPT-5.6 Luna** | $0.20 | $1.20 | 1.05M | **Yes** |
| GPT-5.4 Mini | $0.75 | $4.50 | 400K | No |

### Google Gemini — Zen Only
| Model | Input/1M | Output/1M | Context |
|-------|----------|-----------|---------|
| Gemini 3.7 Flash | $1.50 | $7.50 | 1M |
| Gemini 3.5 Flash Lite | $0.30 | $2.50 | 1M |
| Gemini 3.1 Pro | $2.00 | $12.00 | 1M |

### DeepSeek — In Go
| Model | Input (off-peak) | Output (off-peak) | In Go? |
|-------|-----------------|-------------------|--------|
| DeepSeek V4 Pro | $0.66 | $1.98 | **Yes** |
| DeepSeek V4 Flash | $0.22 | $0.66 | **Yes** |

### xAI Grok — 4.5 in Go
| Model | Input/1M | Output/1M | In Go? |
|-------|----------|-----------|--------|
| Grok 4.6 | $2.00 | $6.00 | No |
| **Grok 4.5** | $2.00 | $6.00 | **Yes** |

### GLM — In Go
| Model | Input/1M | Output/1M | In Go? |
|-------|----------|-----------|--------|
| GLM 5.3 | $1.40 | $4.40 | **Yes** |
| GLM 5.2 | $1.40 | $4.40 | **Yes** |
| GLM 5.1 | $1.40 | $4.40 | **Yes** |

### Kimi — In Go
| Model | Input/1M | Output/1M | In Go? |
|-------|----------|-----------|--------|
| Kimi K3 | $3.00 | $15.00 | **Yes** |
| Kimi K2.7 Code | $0.95 | $4.00 | **Yes** |
| Kimi K2.6 | $0.95 | $4.00 | **Yes** |

---

## Benchmarks (August 19, 2026)

### BenchLM Coding Leaderboard

| Rank | Model | Score | SWE-bench | In Go? |
|------|-------|-------|-----------|--------|
| 1 | Claude Mythos 5 | 81.1 | 95.5% | No |
| 2 | Claude Fable 5 | 80.8 | 95.0% | No |
| 3 | GPT-5.6 Sol | 78.8 | 64.6% (Pro) | Zen |
| 4 | Claude Opus 5 | 78.0 | 96.0% | Zen |
| 4 | **Kimi K3** | 78.0 | — | **Go** |
| 6 | **GPT-5.6 Luna** | 73.0 | 62.7% (Pro) | **Go** |
| 9 | Claude Sonnet 5 | 68.5 | 85.2% | Zen |
| 10 | **Qwen3.8 Max** | 66.6 | — | **Go** |
| 11 | Gemini 3.7 Flash | 66.4 | — | Zen |
| 14 | Hy3 | 63.4 | — | Go |
| 15 | Grok 4.6 | 63.6 | — | Zen |
| 18 | DeepSeek V4 Pro | ~61 | — | Go |

### LMSYS Arena — Top 10

| Rank | Model | Elo |
|------|-------|-----|
| 1 | Claude Fable 5 | 1506 |
| 7 | Claude Opus 5 (high) | 1493 |
| 8 | **Qwen3.8 Max** | 1491 |
| 9 | Gemini 3.7 Flash (high) | 1490 |

### WebDev Arena — Top 10

| Rank | Model | Elo | In Go? |
|------|-------|-----|--------|
| 1 | Claude Opus 5 (max) | 1692 | Zen |
| 2 | **Kimi K3 (max)** | 1674 | **Go** |
| 3 | **Qwen3.8 Max** | 1667 | **Go** |
| 9 | **GLM-5.2 (max)** | 1585 | **Go** |
| 10 | **DeepSeek V4 Pro (high)** | 1584 | **Go** |

### Artificial Analysis Intelligence Index

| Rank | Model | Intelligence | Cost/Task | Speed |
|------|-------|-------------|-----------|-------|
| 1 | Claude Opus 5 (max) | 63 | $2.34 | 55 tok/s |
| 5 | GPT-5.6 Sol (max) | 61 | $1.23 | 65 tok/s |
| 7 | **Kimi K3 (max)** | 60 | $0.84 | — |
| 8 | **GLM-5.3 (max)** | 60 | $0.68 | — |
| 11 | Gemini 3.7 Flash (high) | 56 | $0.40 | 344 tok/s |
| 13 | DeepSeek V4 Pro 0813 | 53 | $0.25 | 75 tok/s |

---

## Value Analysis

### Intelligence/$ Ratio

| Model | Output/1M | % of Leader | Intelligence/$ |
|-------|-----------|-------------|----------------|
| DeepSeek V4 Pro | $0.87 | ~78% | 70.3 |
| MiniMax M3 | $1.20 | ~88% | 57.3 |
| GPT-5.6 Luna | $1.20 | ~93% | 56.1 |
| Gemini 3.7 Flash | $3.75 | ~85% | 16.4 |
| Grok 4.5 | $6.00 | ~96% | 12.6 |
| Claude Sonnet 5 | $10.00 | ~87% | 6.5 |
| Claude Opus 5 | $25.00 | 100% | 3.3 |

### The Sweet Spot Models

Models achieving **80%+ of frontier intelligence** at **20% or less of frontier pricing**:

| Model | Output/1M | % of Leader | % of Leader Price |
|-------|-----------|-------------|-------------------|
| DeepSeek V4 Pro | $0.87 | ~78% | 3.5% |
| GPT-5.6 Luna | $1.20 | ~93% | 4% |
| MiniMax M3 | $1.20 | ~88% | 4.8% |
| Gemini 3.7 Flash | $3.75 | ~85% | 15% |
| Grok 4.5 | $6.00 | ~96% | 24% |

---

## Feature Comparison

### Context Windows

| Model | Context | In Go? |
|-------|---------|--------|
| GPT-5.6 Sol/Terra/Luna | 1.05M | Luna: Yes |
| Claude Opus 5 / Sonnet 5 | 1M | No |
| Gemini 3.x Flash | 1M | No |
| DeepSeek V4 Pro/Flash | 1M | Yes |
| Kimi K3 | 1.05M | Yes |
| Qwen3.8 Max | 1M | Yes |
| Grok 4.5/4.6 | 500K | 4.5: Yes |

### Caching Savings

| Provider | Cache Read Savings | TTL |
|----------|-------------------|-----|
| Anthropic | 90% off | 5min / 1hr |
| OpenAI | 90% off | 30min |
| DeepSeek | Free (disk) | Hours-days |

### Batch Discounts

| Provider | Discount |
|----------|----------|
| Anthropic | 50% off |
| OpenAI | 50% off |
| Mistral | 50% off |

---

## Recommended Configs

### Go Subscriber ($10/mo)
```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "opencode-go/gpt-5.6-luna",
  "small_model": "opencode-go/deepseek-v4-flash",
  "agent": {
    "build": { "model": "opencode-go/gpt-5.6-luna" },
    "plan": { "model": "opencode-go/kimi-k3" }
  }
}
```

### Zen / BYOK
```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "anthropic/claude-sonnet-5",
  "small_model": "opencode/deepseek-v4-flash",
  "agent": {
    "build": { "model": "anthropic/claude-sonnet-5" },
    "plan": { "model": "anthropic/claude-opus-5" }
  }
}
```

---

## Sources

- [opencode.ai/docs/go](https://opencode.ai/docs/go/) — Go subscription
- [opencode.ai/docs/zen](https://opencode.ai/docs/zen/) — Zen model catalog
- [benchlm.ai/coding](https://benchlm.ai/coding) — Coding leaderboard
- [lmarena.ai/leaderboard](https://lmarena.ai/leaderboard) — LMSYS Arena
- [artificialanalysis.ai](https://artificialanalysis.ai/leaderboards/models) — Intelligence Index
- [aider.chat/docs/leaderboards](https://aider.chat/docs/leaderboards/) — Aider benchmarks
- [swebench.com](https://swebench.com/) — SWE-bench
