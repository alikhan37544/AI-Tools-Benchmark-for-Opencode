# 01 — OpenCode Go: Roster, Plans & Limit Mechanics

> **Snapshot: October 1, 2026.** Everything here was verified against the live docs on that date.
> Primary sources: [opencode.ai/docs/go](https://opencode.ai/docs/go/) · [opencode.ai/v2/docs/console/go](https://opencode.ai/v2/docs/console/go) · [opencode.ai/docs/zen](https://opencode.ai/docs/zen/) · [opencode.ai/data](https://opencode.ai/data)

---

## 1. The plans

| Plan | Price | What you get |
|---|---|---|
| **Go** | **$10/mo** | Access to all Go models, with a per-model monthly usage allowance (dollar-denominated) |
| **Go Plus** | **$40/mo** (launched Sep 28, 2026) | Same models, roughly 3–8× the per-model allowance |
| **Zen (pay-as-you-go)** | per token | Same gateway, no limits, list prices; can be used as overflow for Go |
| **Free tier** | $0 | Free/stealth models remain usable after Go limits are hit |

- Only **one member per workspace** can subscribe to Go/Go Plus.
- If you have Zen credits, you can enable **Use balance** and Go falls back to your Zen balance after limits instead of blocking requests.
- After limits, you can always keep using the **free models** (Space Bunny, LongCat 2.5 Preview, Zen free models).

---

## 2. How usage limits actually work

The docs are explicit:

> *"Usage limits are defined as monthly dollar amounts… Each model has the following usage limits: 5-hour — 20% of the monthly limit; weekly — 50%; and monthly — 100%."* — [opencode.ai/docs/go](https://opencode.ai/docs/go/)

So for a model with a **$60/month** allowance:

| Window | Cap | Type |
|---|---|---|
| 5-hour rolling | **$12** | Rolling window |
| Weekly | **$30** | Rolling/calendar week |
| Monthly | **$60** | Rolling/calendar month |

Each model has its **own** caps. Spending on Kimi K3 does not consume your DeepSeek allowance. This is why you can be "out" of one model and still have enormous headroom on another.

### The pricing table (Go, $/1M tokens)

Prices are identical on Go and Go Plus; only the monthly allowances differ.

| Model | Input | Output | Cache read | Cache write | Go monthly | Go Plus monthly |
|---|---|---|---|---|---|---|
| GLM-5.3-Flash | $0.15 | $0.50 | $0.03 | — | $60 | $180 |
| GLM-5.3 | $1.40 | $4.40 | $0.26 | — | **$15** | $120 |
| GLM-5.2 | $1.40 | $4.40 | $0.26 | — | $60 | $180 |
| Kimi K3 | $3.00 | $15.00 | $0.30 | — | **$15** | $60 |
| Kimi K2.7 Code | $0.95 | $4.00 | $0.19 | — | $60 | $180 |
| Kimi K2.6 | $0.95 | $4.00 | $0.16 | — | $60 | $240 |
| LongCat-2.0 | $0.30 | $1.20 | $0.006 | — | $60 | $240 |
| LongCat 2.5 Preview Free | Free | Free | Free | — | **Unlimited\*** | Unlimited\* |
| MiMo-V2.6-Flash | $0.14 | $0.28 | $0.0028 | — | $60 | $120 |
| MiMo-V2.6-Pro | $0.435 | $0.87 | $0.003625 | — | **$15** | $60 |
| MiMo-V2.5 | $0.14 | $0.28 | $0.0028 | — | $60 | $120 |
| MiMo-V2.5-Pro | $0.435 | $0.87 | $0.003625 | — | **$15** | $60 |
| MiniMax M3 | $0.30 | $1.20 | $0.06 | — | $60 | $180 |
| MiniMax M2.7 | $0.30 | $1.20 | $0.06 | $0.375 | $60 | $240 |
| Muse Spark 1.3 Contributor | $0.10 | $0.20 | $0.002 | — | $60 | $120 |
| Muse Spark 1.2 Contributor | $0.10 | $0.20 | $0.002 | — | $60 | $120 |
| Qwen3.8 Max | $2.00 | $6.00 | $0.25 | $2.50 | **$15** | $60 |
| Qwen3.8 Flash | $0.15 | $0.47 | $0.016 | $0.20 | $30 | $90 |
| Qwen3.7 Plus ≤256K | $0.40 | $1.60 | $0.04 | $0.50 | $60 | $180 |
| Qwen3.7 Plus >256K | $1.20 | $4.80 | $0.12 | $1.50 | $60 | $180 |
| DeepSeek V4.1 Flash (off-peak) | $0.15 | $0.60 | $0.003 | — | $60 | $120 |
| DeepSeek V4.1 Flash (peak) | $0.30 | $1.20 | $0.006 | — | $60 | $120 |
| DeepSeek V4 Pro (off-peak) | $0.66 | $1.98 | $0.022 | — | **$15** | $60 |
| DeepSeek V4 Pro (peak) | $1.32 | $3.96 | $0.044 | — | **$15** | $60 |
| DeepSeek V4 Flash (off-peak) | $0.15 | $0.60 | $0.003 | — | $30 | $120 |
| DeepSeek V4 Flash (peak) | $0.30 | $1.20 | $0.006 | — | $30 | $120 |
| DeepSeek V4 Flash Vision Exp (off-peak) | $0.15 | $0.60 | $0.003 | — | **$15** | $60 |
| Hy4 preview | $0.834 | $2.501 | $0.042 | — | $30 | $120 |
| Hy3 | $0.14 | $0.58 | $0.035 | — | $60 | $240 |
| Grok 4.7 ≤200K | $2.00 | $6.00 | $0.50 | — | **$15** | $60 |
| Grok 4.7 >200K | $4.00 | $12.00 | $1.00 | — | **$15** | $60 |
| Grok 4.6 ≤200K | $2.00 | $6.00 | $0.50 | — | **$15** | $60 |
| GPT 6 Luna ≤272K | $0.10 | $0.50 | $0.01 | $0.125 | **$15** | $60 |
| GPT 5.6 Luna ≤272K | $0.20 | $1.20 | $0.02 | $0.25 | **$15** | $60 |
| Space Bunny Free | Free | Free | Free | — | **Unlimited\*** | Unlimited\* |

\* Limited-time free previews. LongCat 2.5's free window was announced as ~2 weeks (to about Oct 10, 2026).

### DeepSeek peak/off-peak

DeepSeek models are 2× more expensive during **peak = 01:00–04:00 and 06:00–10:00 UTC, Monday–Friday** (excluding Chinese holidays). Everything else — including all weekend — is half price. For an IST-based schedule (UTC+5:30) that means peak is roughly **06:30–09:30 and 11:30–15:30 IST**; evenings, nights and weekends are off-peak. Scheduling long autonomous runs off-peak effectively **doubles your DeepSeek headroom**.

Source: [DeepSeek pricing docs](https://api-docs.deepseek.com/quick_start/pricing).

---

## 3. The full Go roster (30 models)

Verified live on Oct 1, 2026, from [opencode.ai/docs/go](https://opencode.ai/docs/go/):

**Frontier / high-intelligence**
- Grok 4.7, Grok 4.6 (xAI)
- Kimi K3, Kimi K2.7 Code, Kimi K2.6 (Moonshot)
- GLM-5.3, GLM-5.3-Flash, GLM-5.2 (Z.ai / Zhipu)
- Qwen3.8 Max, Qwen3.8 Flash, Qwen3.7 Plus (Alibaba)
- GPT 6 Luna, GPT 5.6 Luna (OpenAI)

**Workhorses / volume**
- DeepSeek V4.1 Flash, DeepSeek V4 Pro, DeepSeek V4 Flash, DeepSeek V4 Flash Vision Exp
- MiMo-V2.6-Pro, MiMo-V2.6-Flash, MiMo-V2.5-Pro, MiMo-V2.5 (Xiaomi)
- MiniMax M3, MiniMax M2.7
- LongCat-2.0 (Meituan)
- Hy4 preview, Hy3 (Tencent)
- Muse Spark 1.3 Contributor, Muse Spark 1.2 Contributor (Meta)

**Free / stealth (limited time)**
- Space Bunny Free (stealth)
- LongCat 2.5 Preview Free

**Recently removed/deprecated from the roster (Sep 2026):** GLM-5.1, Qwen3.7 Max, Qwen3.6 Plus, MiniMax M2.5, Kimi K2.5, GLM-5. Pipeline churn is real — re-check the docs monthly.

---

## 4. Free and stealth models (important fine print)

Zen/Go free models as of Oct 1, 2026 ([Zen docs](https://opencode.ai/docs/zen/)):

| Model | Notes |
|---|---|
| **Space Bunny Free** | Stealth model, free "limited time", 1M context, vision. OpenCode route: zero-retention, no training. Fingerprint analysis suggests a MiniMax-family model (unconfirmed). Community reports strong web design and speed, but a tool-param wrapping bug (`{item: value}`). |
| **LongCat 2.5 Preview Free** | Free ~2 weeks; provider claims zero-retention. No public benchmarks or model card (as of Oct 1). |
| **Big Pickle** | Zen stealth; **data may be used to improve the model** — do not use for client/PHI work. |
| MiMo-V2.6-Flash Free / MiMo-V2.5 Free | Data may be used for training during free period. |
| Ling 3.0 Flash Fin Free | Training may occur. |
| Nemotron 3 Ultra / 3.5 Lightning Free | NVIDIA trial endpoints; data logged, **do not submit personal/confidential data**. |
| Muse Spark 1.3 Contributor Free | Discounted in exchange for permission to train on prompts/completions. |
| Jev 1.13 Free | TypeSafe AI structured-decision model (not a chat model). |

**Paid Muse Spark 1.3 Contributor on Go also trains on your data** — it is the cheap "contributor" tier. For medical/insurance/client work, use a non-contributor model or a zero-retention provider.

---

## 5. `opencode.ai/data` — what the whole user base actually runs

From the live telemetry page (week ending Oct 1, 2026, tokens):

| # | Model | Weekly tokens |
|---|---|---|
| 1 | space-bunny | 58T |
| 2 | deepseek-v4.1-flash | 34T |
| 3 | muse-spark-1.3-contributor | 33T |
| 4 | mimo-v2.6-flash | 8.9T |
| 5 | deepseek-v4-flash | 6.7T |
| 6 | nemotron-3-ultra (free) | 3.8T |
| 7 | longcat-2.5-preview (free) | 2.3T |
| 8 | glm-5.3-flash | 2.3T |
| 9 | muse-spark-1.2-contributor | 916B |
| 10 | mimo-v2.5 | 839B |
| 11 | deepseek-v4-flash-vision-exp | 722B |
| 12 | gpt-6-luna | 683B |
| 13 | mimo-v2.6-pro | 480B |
| 14 | deepseek-v4-pro | 473B |
| 15 | qwen3.8-flash | 257B |

Cache ratios (share of input served from cache): space-bunny 97%, muse-spark-1.3 97%, **deepseek-v4.1-flash 96%**, deepseek-v4-flash 96%, longcat-2.5 96%, mimo-v2.6-flash 95%, glm-5.3-flash 94%.

**Takeaway:** the crowd's revealed preference is overwhelmingly the cheap, high-cap models — not Kimi K3/Grok. Session costs: Muse Spark 1.3 ≈ $0.0004/session, MiMo-V2.6-Flash $0.0034, DeepSeek V4 Flash $0.032, GLM-5.3-Flash $0.068, DeepSeek V4.1 Flash $0.078.

---

## 6. What changed Aug → Oct 2026 (brief history)

| Date | Change |
|---|---|
| Aug 12 | Grok 4.6 added |
| Aug 14 | GLM-5.3 added — at a $15/mo allowance, prompting user backlash ("1/4 the usage of GLM-5.2") |
| Aug 20–26 | "Ox Alpha" stealth ran free on Go, revealed as **GLM-5.3-Flash**; allowance later raised to $60 |
| Aug 24 | First-month $5 discount discontinued |
| Aug 26–28 | Qwen3.8 Flash and Hy4 preview added |
| Sep 2–4 | Muse Spark 1.3 Contributor added |
| Sep 10 | **DeepSeek V4.1 Flash** added with a 4× usage promo (now permanent $60) |
| Sep 21–22 | **Grok 4.7, GPT 6 Luna, MiMo-V2.6 Flash/Pro** added |
| Sep 23 | Space Bunny free stealth added |
| Sep 25 | LongCat 2.5 Preview Free added |
| **Sep 28** | **Go Plus ($40) launched**; v1.18.33 |
| Sep 30 | v1.18.34; very recent deprecations of GLM-5.1, Qwen3.7 Max, etc. |

Sources: [opencode.ai/changelog](https://opencode.ai/changelog), [julien.cloud/opencode-go-models](https://julien.cloud/opencode-go-models/), [Go docs](https://opencode.ai/docs/go/).

---

## 7. Reliability caveats (community-reported)

- OpenCode's own router quality has varied: users report 429s/503s on hot models (MiMo-v2.5, Grok 4.6) during demand spikes, and occasional doc-vs-router mismatches (a model disappearing while still listed).
- There are open GitHub issues about the **monthly usage meter not matching spend** (anomalyco/opencode #43032) — treat the console meter as approximate and keep a margin.
- Free models are intended for the OpenCode client; some report 403s when used through other clients.
- Provider quantization varies for OpenRouter, but OpenCode states it does not quantize the Go-served models it validated.

---

**Next:** [02 — Benchmarks](./02-benchmarks.md) · [03 — Task Playbook](./03-task-playbook.md) · [04 — Limits & Burn Rate](./04-limits-and-burn-rate.md) · [05 — Intelligence per Dollar](./05-intelligence-per-dollar.md)
