# 01 — OpenCode Go: Roster, Plans & Limit Mechanics

> **Snapshot: October 1, 2026; refreshed October 13, 16 and 25, 2026.** Roster, caps and prices were re-verified against the live docs on **Oct 25**. Usage telemetry remains Sep 15–Oct 1 vintage; benchmark figures were refreshed Oct 25.
> Primary sources: [opencode.ai/docs/go](https://opencode.ai/docs/go/) · [opencode.ai/docs/zen](https://opencode.ai/docs/zen/) · [opencode.ai/data](https://opencode.ai/data)
>
> 🆕 **Oct 25 refresh — the new stuff:** **Kimi K3.1 Pro** (AA 55, the highest intelligence ever listed on Go) and **MiniMax M3.1 Flash** (AA 43 at $0.22/task) joined the roster. **Space Bunny** and **LongCat 2.5 Preview Free** left it. **Step 5 Preview's 4× promo ended** (back to a $15 cap). **Gemini 4 Argon** is now a plain, 50%-off SKU at **$30/mo**, and — importantly — Go's privacy table now documents it as **not used for training, 0-day retention**. The old "Argon trains on your data" warning is **withdrawn**. Go is still **29 models**.

---

## 1. The plans

| Plan | Price | What you get |
|---|---|---|
| **Go** | **$10/mo** | Access to all 29 Go models, each with its own monthly dollar allowance |
| **Go Plus** | **$40/mo** (launched Sep 28, 2026) | Same models, 2–8× the per-model allowance |
| **Zen (pay-as-you-go)** | per token | Same gateway, no monthly caps, list prices; overflow for Go |
| **Free tier** | $0 | Free/stealth models remain usable after Go limits are hit |

- Only **one member per workspace** can subscribe to Go/Go Plus.
- **"Use balance" is now called "Extra Usage."** Enable it on the Go page and Go falls back to your Zen pay-as-you-go balance after a model's limit instead of blocking. ([Go docs → Usage beyond limits](https://opencode.ai/docs/go/))
- After limits you can always keep using the **free models** — currently a capable floor: **GLM-5.3-Flash Free, DeepSeek V4.1 Flash Free, Beam Free**, plus Flint 40B and other trial/stealth models.

---

## 2. How usage limits actually work

The docs are explicit:

> *"Usage limits are defined as monthly dollar amounts… Each model has the following usage limits: 5-hour — 20% of the monthly limit; weekly — 50%; and monthly — 100%."* — [opencode.ai/docs/go](https://opencode.ai/docs/go/)

So a model with a **$20/month** allowance gets **$4 per rolling 5 hours**, **$10 per week**, and **$20 per month**. Each model has its **own** caps: spending on Kimi K3.1 Pro does not consume your MiniMax M3.1 Flash allowance. That is why you can be "out" of one model and still have enormous headroom on another.

### The pricing table (Go, $/1M tokens)

Prices are identical on Go and Go Plus; only the monthly allowances differ.

| Model | Input | Output | Cache read | Cache write | Go monthly | Go Plus monthly |
|---|---|---|---|---|---|---|
| GLM-5.3-Flash | $0.15 | $0.50 | $0.03 | — | $60 | $180 |
| GLM-5.3 | $1.40 | $4.40 | $0.26 | — | **$15** | $120 |
| GLM-5.2 (legacy) | $1.40 | $4.40 | $0.26 | — | $60 | $180 |
| **Kimi K3.1 Pro** ✨ | **$2.00** | **$10.00** | **$0.20** | **$2.00** | **$15** | **$60** |
| Kimi K3 | $3.00 | $15.00 | $0.30 | $3.00 | **$15** | $60 |
| Kimi K2.7 Code | $0.95 | $4.00 | $0.19 | — | $60 | $180 |
| LongCat-2.0 | $0.30 | $1.20 | $0.006 | — | $60 | $240 |
| Step 5 Preview | $1.00 | $2.70 | $0.10 | — | **$15** (promo ended) | $60 |
| Beam Free | Free | Free | Free | — | **Unlimited\*** | Unlimited\* |
| MiMo-V2.6-Flash | $0.14 | $0.28 | $0.0028 | — | $60 | $120 |
| MiMo-V2.6-Pro | $0.435 | $0.87 | $0.003625 | — | **$15** | $60 |
| MiMo-V2.5 | $0.14 | $0.28 | $0.0028 | — | $60 | $120 |
| MiMo-V2.5-Pro | $0.435 | $0.87 | $0.003625 | — | **$15** | $60 |
| **MiniMax M3.1 Flash** ✨ | **$0.15** | **$0.60** | **$0.015** | — | **$20** | **$80** |
| MiniMax M3 | $0.30 | $1.20 | $0.06 | — | $60 | $180 |
| Muse Spark 1.3 Contributor | $0.10 | $0.20 | $0.002 | — | $60 | $120 |
| Muse Spark 1.2 Contributor | $0.10 | $0.20 | $0.002 | — | $60 | $120 |
| Qwen3.8 Max | $2.00 | $6.00 | $0.25 | $2.50 | **$15** | $60 |
| Qwen3.8 Flash | $0.15 | $0.47 | $0.016 | $0.20 | $30 | $90 |
| Qwen3.7 Plus ≤256K | $0.40 | $1.60 | $0.04 | $0.50 | $60 | $180 |
| Qwen3.7 Plus >256K | $1.20 | $4.80 | $0.12 | $1.50 | $60 | $180 |
| DeepSeek V4.1 Flash (off-peak) | $0.15 | $0.60 | $0.003 | — | $80 | $160 |
| DeepSeek V4.1 Flash (peak) | $0.30 | $1.20 | $0.006 | — | $80 | $160 |
| DeepSeek V4 Pro (off-peak) | $0.66 | $1.98 | $0.022 | — | **$15** | $60 |
| DeepSeek V4 Pro (peak) | $1.32 | $3.96 | $0.044 | — | **$15** | $60 |
| Hy4 preview | $0.834 | $2.501 | $0.042 | — | $30 | $120 |
| Hy3 | $0.14 | $0.58 | $0.035 | — | $60 | $240 |
| Grok 4.7 ≤200K | $2.00 | $6.00 | $0.50 | — | **$15** | $60 |
| Grok 4.7 >200K | $4.00 | $12.00 | $1.00 | — | **$15** | $60 |
| GPT 6 Luna ≤272K | $0.10 | $0.50 | $0.01 | $0.125 | **$15** | $60 |
| GPT 6 Luna >272K | $0.20 | $0.75 | $0.02 | $0.25 | **$15** | $60 |
| GPT 5.6 Luna ≤272K | $0.20 | $1.20 | $0.02 | $0.25 | **$15** | $60 |
| GPT 5.6 Luna >272K | $0.40 | $1.80 | $0.04 | $0.50 | **$15** | $60 |
| Claude Haiku 5.5 ≤100K | $0.10 | $0.50 | $0.01 | $0.125 | **$15** | $60 |
| Claude Haiku 5.5 >100K | $0.50 | $2.50 | $0.05 | $0.625 | **$15** | $60 |
| **Gemini 4 Argon (50% off)** | ~~$4.00~~ **$2.00** | ~~$20.00~~ **$10.00** | ~~$0.20~~ **$0.10** | — | ~~$60~~ **$30** | ~~$120~~ **$120** |

\* **Beam Free** is free for a limited time and is **not available in several regions** (Angola, Belarus, Cambodia, China/HK/Macau, Cuba, DRC, Equatorial Guinea, Iran, Iraq, Laos, Libya, Nigeria, North Korea, Russia, Syria, Turkmenistan, Uzbekistan, Venezuela, and Crimea/Donetsk/Luhansk). 30-day retention, no training. **Gemini 4 Argon's 50% discount runs through November 30, 2026**; the list price returns after that. **Step 5 Preview's 4× promo ended** — it is back at a $15 Go / $60 Plus cap, still at $1.00/$2.70/$0.10 with open weights.

### DeepSeek peak/off-peak

DeepSeek models are 2× more expensive during **peak = 01:00–04:00 and 06:00–10:00 UTC, Monday–Friday** (excluding Chinese holidays). Everything else — including all weekend — is half price. For IST (UTC+5:30) that is roughly **06:30–09:30 and 11:30–15:30 IST**; evenings, nights and weekends are off-peak. Scheduling long autonomous runs off-peak effectively **doubles** your DeepSeek headroom. Source: [DeepSeek pricing docs](https://api-docs.deepseek.com/quick_start/pricing).

---

## 3. The full Go roster (29 models)

Verified live on Oct 25, 2026, from [opencode.ai/docs/go](https://opencode.ai/docs/go/):

**Frontier / high-intelligence**
- **Kimi K3.1 Pro (NEW)** — AA 55.1, 1M ctx, vision, $2/$10/$0.20, $15 cap. The highest-AA model on Go.
- **Gemini 4 Argon** — AA 53, 1M ctx, vision; 50% off through Nov 30; **0-day retention / not used for training**.
- Grok 4.7 (xAI) — 500K ctx, vision, reasoning low→xhigh.
- Kimi K3, Kimi K2.7 Code (Moonshot).
- GLM-5.3, GLM-5.3-Flash, GLM-5.2 (Z.ai / Zhipu).
- Qwen3.8 Max, Qwen3.8 Flash, Qwen3.7 Plus (Alibaba).
- GPT 6 Luna, GPT 5.6 Luna (OpenAI).
- Claude Haiku 5.5 (Anthropic) — fastest Claude, 1M ctx, adjustable effort.

**Workhorses / volume**
- DeepSeek V4.1 Flash, DeepSeek V4 Pro.
- MiMo-V2.6-Pro, MiMo-V2.6-Flash, MiMo-V2.5-Pro, MiMo-V2.5 (Xiaomi).
- **MiniMax M3.1 Flash (NEW)** — AA 43, 112.8 tok/s, 1.35s TTFT, $0.15/$0.60/$0.015, $20 cap.
- MiniMax M3.
- LongCat-2.0 (Meituan).
- Hy4 preview, Hy3 (Tencent).
- Muse Spark 1.3 Contributor, Muse Spark 1.2 Contributor (Meta).

**Free / limited time**
- **Beam Free** (Reflection AI) — 501B/23B MoE, AA 30, 30-day retention, no training, limited regions.
- **Step 5 Preview** is paid again ($1/$2.70/$0.10, $15 cap); open weights released Oct 15.

**Removed this cycle:** **Space Bunny** (revealed Oct 19 as an early MiniMax M3.1 Flash; no free SKU remains) and **LongCat 2.5 Preview Free** (free window ended; LongCat-2.0 remains). Previously removed: Grok 4.6, Kimi K2.6, MiniMax M2.7, DeepSeek V4 Flash/Vision Exp, GLM-5.1, Qwen3.7 Max, Qwen3.6 Plus, MiniMax M2.5, Kimi K2.5.

---

## 4. Free and stealth models (important fine print)

Zen/Go free models as of Oct 25, 2026 ([Zen docs](https://opencode.ai/docs/zen/), [Go docs](https://opencode.ai/docs/go/)):

| Model | Notes |
|---|---|
| **DeepSeek V4.1 Flash Free** | Free on Zen for a limited time; provider follows **zero-retention, no training**. AA 39. The free twin of the daily driver. |
| **GLM-5.3-Flash Free** | Free on Zen for a limited time; **zero-retention, no training**. AA 42 — the best free zero-retention model on the platform. |
| **Beam Free** | Reflection AI Beam (501B/23B MoE, AA 30, Apache-2.0 weights). Free, limited regions, **30-day retention, no training**. |
| **Flint 40B Free** | **NEW.** 40B-class free model; **30-day retention and data may be used to improve the model**. Non-sensitive exploration only. |
| **MiMo-V2.6-Flash Free** | Xiaomi free period; data may be used for training. Open-source/non-sensitive work only. |
| **Nemotron 3.5 Super VL Free / Nemotron 3 Ultra / 3.5 Lightning Free** | NVIDIA trial endpoints; data logged, **do not submit personal/confidential data**. |
| **Big Pickle** | Zen stealth; **data may be used to improve the model**. Identity unknown (GLM-family audit); high-variance reliability. |
| **Jev 1.13 Free** | TypeSafe structured-decision model (not a chat model). |

**Removed from the free list this cycle:** Space Bunny Free (paid/removed), LongCat 2.5 Preview Free (window ended), LL Alpha Free, Muse Spark 1.3 Contributor Free, Exo Free.

**The only paid "Contributor" SKUs left on Go are Muse Spark 1.3/1.2 — they still train on your prompts/completions.** Gemini 4 Argon is **not** a Contributor SKU anymore: Go's table says **"Not used / 0 days"** for Argon. Treat the old Argon-training warning as **withdrawn**, but re-verify before client/PHI work.

---

## 5. `opencode.ai/data` — what the whole user base actually runs

From the live telemetry page (7 days ending Oct 25, 2026, tokens):

| # | Model | Weekly tokens | Change |
|---|---|---|---|
| 1 | deepseek-v4.1-flash | **119T** | +39% |
| 2 | **minimax-m3.1-flash** | **37T** | **+92%** |
| 3 | glm-5.3-flash | 8.9T | +69% |
| 4 | muse-spark-1.3-contributor | 7.6T | −76% |
| 5 | mimo-v2.6-flash | 7.2T | −35% |
| 6 | beam (free) | 5.3T | +86% |
| 7 | **deepseek-v4.1-flash-1017** | **1.3T** | **New** |
| 8 | longcat-2.5-preview (free) | 887B | −62% |
| 9 | **iceman (stealth)** | **661B** | **New** |
| 10 | claude-haiku-5-5 | 315B | −6% |

**Takeaway:** DeepSeek V4.1 Flash is still the crowd's undisputed #1, but **MiniMax M3.1 Flash nearly doubled in a week and is now #2** — the new cheap-workhorse signal. Muse Spark's collapse (−76%) lines up with the Contributor-training caveat and the M3.1 Flash launch. The 1017 DeepSeek checkpoint and an unknown stealth ("iceman") are new entries worth watching.

---

## 6. What changed Sep → Oct 2026 (brief history)

| Date | Change |
|---|---|
| Aug 12 | Grok 4.6 added (later removed) |
| Aug 14 | GLM-5.3 added at a $15 allowance |
| Aug 20–26 | "Ox Alpha" stealth revealed as GLM-5.3-Flash; allowance later raised to $60 |
| Sep 2–4 | Muse Spark 1.3 Contributor added |
| Sep 10 | DeepSeek V4.1 Flash added (cap later raised to $80) |
| Sep 21–22 | Grok 4.7, GPT 6 Luna, MiMo-V2.6 Flash/Pro added |
| Sep 28 | Go Plus ($40) launched |
| Oct 7 | Claude Haiku 5.5 added ($15 cap) |
| Oct 8 | Step 5 Preview Free added; DeepSeek cap $60→$80; ZDR through Oct 31 |
| Oct 12 | Beam Free added; Muse Wonder/Wonder Full released (not on Go) |
| Oct 13 | Gemini 4 Argon Contributor added; Grok 4.6/K2.6/M2.7 removed |
| Oct 14–15 | Step 5 free→paid; open weights; Zen free twins (DeepSeek/GLM) |
| **Oct 19–25** | **Space Bunny revealed as early M3.1 Flash → removed; LongCat 2.5 Free removed; Kimi K3.1 Pro + MiniMax M3.1 Flash added; Step 5 promo ended; Argon renamed/50%-off and corrected to ZDR; Flint 40B Free appears on Zen** |

Sources: [opencode.ai/changelog](https://opencode.ai/changelog), [julien.cloud/opencode-go-models](https://julien.cloud/opencode-go-models/), [Go docs](https://opencode.ai/docs/go/), [Zen docs](https://opencode.ai/docs/zen/), [opencode.ai/data](https://opencode.ai/data).

---

## 7. Reliability caveats (community-reported)

- OpenCode's router quality has varied: 429s/503s on hot models during demand spikes, and occasional doc-vs-router mismatches.
- Open GitHub issues about the monthly usage meter not matching spend (anomalyco/opencode #43032) — treat the console meter as approximate and keep a margin.
- Free models are intended for the OpenCode client; some report 403s through other clients.
- **The free tier is high-churn** — Step 5 went paid, Space Bunny disappeared, LongCat 2.5 ended. Keep a fallback lane configured for every free model you rely on.
- Provider quantization varies for OpenRouter, but OpenCode states it does not quantize the Go-served models it validated.

---

**Next:** [02 — Benchmarks](./02-benchmarks.md) · [03 — Task Playbook](./03-task-playbook.md) · [04 — Limits & Burn Rate](./04-limits-and-burn-rate.md) · [05 — Intelligence per Dollar](./05-intelligence-per-dollar.md)
