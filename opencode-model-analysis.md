# OpenCode Model Intelligence Analysis

> **Updated: August 19, 2026** | Cloud models, pricing, benchmarks, OpenCode Go

## TL;DR

| Category | Model | Price (Output/1M) | Intelligence | Notes |
|----------|-------|-------------------|--------------|-------|
| **Most Intelligent** | Claude Opus 5 | $25.00 | 100% (leader) | SWE-bench 96%, AA Index 63 |
| **Best Value (BYOK)** | GPT-5.6 Luna | $1.20 | ~93% of leader | 4% of Opus price |
| **Cheapest Capable** | DeepSeek V4 Pro | $0.87 | ~78% of leader | 34x cheaper than Opus |
| **Best Go Model** | GPT-5.6 Luna | Included in $10/mo | ~93% | ~10,250 req/mo |
| **Fastest** | Gemini 3.7 Flash | $3.75 | ~85% | 374 tok/s |
| **Best Open-Weight** | Qwen3.8 Max | $2.00/$6.00 | ~85% | #8 LMSYS, #3 WebDev |
| **Best New Entrant** | Kimi K3 | $3/$15 | ~98% | #5 BenchLM, open weights |

---

## August 2026 Model Releases (19 models in 19 days)

| Date | Model | Provider | Key Details |
|------|-------|----------|-------------|
| Aug 18 | Ornith 1.5 (3 variants) | Ornith AI | 397B params |
| **Aug 14** | **Qwen3.8-27B** | Alibaba | 27B dense, Apache 2.0, vision-language, #1 HuggingFace trending |
| Aug 14 | GLM-5.3 | Z.ai (Zhipu) | Open-model rankings leader |
| **Aug 13** | **Gemini 3.7 Flash** | Google | Latest Flash, $1.50/$7.50, 1M ctx |
| **Aug 13** | **DeepSeek-V4-Pro-0813** | DeepSeek | Updated Pro variant |
| Aug 12 | Grok 4.6 | xAI | Continuation of Grok 4.x |
| Aug 12 | Seed 2.1 Turbo | ByteDance | LLM |
| Aug 12 | Seed-2.0-Code | ByteDance | Code-specialized |
| Aug 11 | Nemotron 3.5 Lightning 30B | NVIDIA | NVFP4 quantized |
| Aug 10 | GPT-5.6 Cyber | OpenAI | Cybersecurity-focused |
| Aug 10 | Muse Glimmer 30B | Meta | Open agentic model |
| Aug 5 | Muse Spark 1.2 | Meta | Updated Muse |
| **Aug 3** | **Qwen3.8 Max** | Alibaba | 2.4T MoE, ~95B active, 1M ctx |
| Jul 31 | DeepSeek-V4-Flash-0731 | DeepSeek | Retrained, outscores V4-Pro on coding |
| **Jul 27** | **Kimi K3** | Moonshot AI | 2.8T params, open weights, beat Claude Opus 4.8 |
| **Jul 24** | **Claude Opus 5** | Anthropic | 1M ctx, AA Index #1 (63) |
| Jul 21 | Gemini 3.6 Flash | Google | $1.50/$7.50, 1M ctx |
| Jul 9 | GPT-5.6 Sol GA | OpenAI | Generally available, 750 tok/s on Cerebras |
| Jul 8 | Grok 4.5 | xAI | $2/$6, 500K ctx |

---

## OpenCode Go ($10/mo) — 21 Models

### Best Go Models Ranked

| Model | Intelligence | Req/Month | Use Case |
|-------|-------------|-----------|----------|
| **Kimi K3** | ~98% | ~490 | Reserve for critical tasks |
| **Grok 4.5** | ~96% | ~600 | Complex reasoning |
| **GPT 5.6 Luna** | ~93% | ~10,250 | **Daily driver** |
| **Qwen3.8 Max** | ~85% | ~810 | Best open-weight reasoning |
| **MiniMax M3** | ~88% | ~16,000 | High volume coding |
| **GLM-5.3** | ~77% | ~1,080 | Reasoning |
| **GLM-5.2** | ~82% | ~4,300 | Most popular on Go |
| **DeepSeek V4 Pro** | ~78% | ~5,200 | Reasoning tasks |
| **DeepSeek V4 Flash** | ~66% | ~37,800 | Quick fixes |
| **MiMo-V2.5-Pro** | ~55% | ~16,300 | Budget coding |

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
| GPT-5 Nano | $0.05 | $0.40 | — | No |

### Google Gemini — Zen Only
| Model | Input/1M | Output/1M | Context |
|-------|----------|-----------|---------|
| Gemini 3.7 Flash | $1.50 | $7.50 | 1M |
| Gemini 3.6 Flash | $1.50 | $7.50 | 1M |
| Gemini 3.5 Flash Lite | $0.30 | $2.50 | 1M |
| Gemini 3.1 Pro | $2.00 | $12.00 | 1M |
| Gemini 3 Flash | $0.50 | $3.00 | 1M |

### DeepSeek — In Go
| Model | Input (off-peak) | Output (off-peak) | In Go? |
|-------|-----------------|-------------------|--------|
| DeepSeek V4 Pro | $0.66 | $1.98 | **Yes** |
| DeepSeek V4 Flash | $0.22 | $0.66 | **Yes** |

### xAI Grok — In Go
| Model | Input/1M | Output/1M | In Go? |
|-------|----------|-----------|--------|
| Grok 4.6 | $2.00 | $6.00 | No |
| **Grok 4.5** | $2.00 | $6.00 | **Yes** |

### Qwen (Alibaba) — In Go
| Model | Input/1M | Output/1M | Context | In Go? |
|-------|----------|-----------|---------|--------|
| **Qwen3.8 Max** | $2.00 | $6.00 | 1M | **Yes** |
| Qwen3.7 Max | $2.50 | $7.50 | 1M | Yes |
| Qwen3.7 Plus | $0.40 | $1.60 | — | Yes |
| Qwen3.6 Plus | $0.50 | $3.00 | — | Yes |

### GLM (Zhipu) — In Go
| Model | Input/1M | Output/1M | In Go? |
|-------|----------|-----------|--------|
| GLM 5.3 | $1.40 | $4.40 | **Yes** |
| GLM 5.2 | $1.40 | $4.40 | **Yes** |

### Kimi (Moonshot) — In Go
| Model | Input/1M | Output/1M | In Go? |
|-------|----------|-----------|--------|
| Kimi K3 | $3.00 | $15.00 | **Yes** |
| Kimi K2.7 Code | $0.95 | $4.00 | **Yes** |

### MiniMax — In Go
| Model | Input/1M | Output/1M | In Go? |
|-------|----------|-----------|--------|
| MiniMax M3 | $0.30 | $1.20 | **Yes** |
| MiniMax M2.7 | $0.30 | $1.20 | **Yes** |

### Free Models (7)
Big Pickle, DeepSeek V4 Flash Free, MiMo-V2.5 Free, Hy3 Free, Laguna S 2.1 Free, Nemotron 3 Ultra Free, Nemotron 3.5 Lightning Free

---

## Benchmarks — August 19, 2026

### BenchLM Coding Leaderboard

| Rank | Model | Score | In Go? |
|------|-------|-------|--------|
| 1 | Claude Mythos 5 | 81.2 | No |
| 2 | Claude Fable 5 | 81.0 | No |
| 3 | GPT-5.6 Sol | 78.9 | Zen |
| 4 | Claude Opus 5 | 78.2 | Zen |
| 5 | Kimi K3 | 78.1 | **Go** |
| 6 | GPT-5.6 Luna | 73.2 | **Go** |
| 7 | Claude Opus 4.8 | 71.3 | Zen |
| 8 | GPT-5.5 | 71.1 | Zen |
| 9 | Claude Sonnet 5 | 68.6 | Zen |
| 10 | Claude Opus 4.7 | 67.5 | Zen |
| **11** | **Qwen3.8 Max** | **66.7** | **Go** |
| 12 | Gemini 3.7 Flash | 66.5 | Zen |
| 13 | GPT-5.6 Terra | 65.5 | Zen |
| 17 | GLM-5.2 | 63.9 | **Go** |
| 18 | Grok 4.6 | 63.7 | Zen |
| 20 | Hy3 | 63.5 | **Go** |

### LMSYS Arena — Text Elo (Top 10)

| Rank | Model | Elo |
|------|-------|-----|
| 1 | Claude Fable 5 | 1506 |
| 2 | Claude Opus 4.6 (high) | 1505 |
| 3 | Claude Opus 4.7 (high) | 1502 |
| 4 | Muse Spark 1.2 (xHigh) | 1498 |
| 7 | Claude Opus 5 (high) | 1493 |
| **8** | **Qwen3.8 Max** | **1491** |
| 9 | Gemini 3.7 Flash (high) | 1490 |

### WebDev Arena (Top 5)

| Rank | Model | Elo | In Go? |
|------|-------|-----|--------|
| 1 | Claude Opus 5 (max) | 1692 | Zen |
| 2 | Kimi K3 (max) | 1674 | **Go** |
| **3** | **Qwen3.8 Max** | **1667** | **Go** |
| 4 | Claude Opus 5 (high) | 1663 | Zen |
| 5 | Grok 4.6 (high) | 1631 | Zen |

### Artificial Analysis Intelligence Index (Top 15)

| Rank | Model | Intelligence | Cost/Task | Speed |
|------|-------|-------------|-----------|-------|
| 1 | Claude Opus 5 (max) | 63 | $2.34 | 55 tok/s |
| 2 | Claude Opus 5 (xhigh) | 63 | $1.80 | — |
| 3 | Claude Fable 5 | 62 | $3.14 | — |
| 4 | Claude Opus 5 (high) | 61 | $1.23 | 53 tok/s |
| 5 | GPT-5.6 Sol (max) | 61 | $1.23 | 65 tok/s |
| 6 | Grok 4.6 (high) | 61 | $0.84 | 56 tok/s |
| 7 | Kimi K3 (max) | 60 | $0.84 | — |
| 8 | GLM-5.3 (max) | 60 | $0.68 | — |
| **11** | **Qwen3.8 Max** | **58** | **$1.13** | — |
| 12 | Qwen3.8 2.4T A95B | 58 | $1.09 | — |
| 16 | Gemini 3.7 Flash (high) | 56 | $0.40 | 374 tok/s |
| 17 | Grok 4.5 (high) | 56 | $0.36 | — |
| 19 | Claude Sonnet 5 (max) | 55 | $1.72 | 76 tok/s |
| 20 | Gemini 3.7 Flash (medium) | 53 | $0.26 | — |

---

## Value Analysis

### Intelligence/$ Ratio

| Model | Output/1M | % of Leader | Intelligence/$ |
|-------|-----------|-------------|----------------|
| DeepSeek V4 Pro | $0.87 | ~78% | 70.3 |
| MiniMax M3 | $1.20 | ~88% | 57.3 |
| GPT-5.6 Luna | $1.20 | ~93% | 56.1 |
| Qwen3.8 Max | $6.00 | ~85% | 9.7 |
| Gemini 3.7 Flash | $3.75 | ~85% | 16.4 |
| Grok 4.5 | $6.00 | ~96% | 12.6 |
| Kimi K3 | $15.00 | ~98% | 5.2 |
| Claude Sonnet 5 | $10.00 | ~87% | 6.5 |
| Claude Opus 5 | $25.00 | 100% | 3.3 |

### Sweet Spot Models (80%+ intelligence at 20% or less of frontier price)

| Model | Output/1M | % of Leader | % of Leader Price |
|-------|-----------|-------------|-------------------|
| DeepSeek V4 Pro | $0.87 | ~78% | 3.5% |
| GPT-5.6 Luna | $1.20 | ~93% | 4% |
| MiniMax M3 | $1.20 | ~88% | 4.8% |
| Gemini 3.7 Flash | $3.75 | ~85% | 15% |
| Grok 4.5 | $6.00 | ~96% | 24% |

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
- [aireleasetracker.com/latest](https://aireleasetracker.com/latest) — Release tracker
