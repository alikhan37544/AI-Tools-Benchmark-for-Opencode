# 01 — OpenCode Go: Roster, Plans & Limit Mechanics

> **Snapshot: October 1, 2026, refreshed October 13 and October 16, 2026.** Roster, caps, pricing and new-model sections were re-verified against the live docs on Oct 16; benchmark figures and telemetry refreshed Oct 16. Historical usage telemetry remains Sep 15–Oct 1 vintage.
> Primary sources: [opencode.ai/docs/go](https://opencode.ai/docs/go/) · [opencode.ai/v2/docs/console/go](https://opencode.ai/v2/docs/console/go) · [opencode.ai/docs/zen](https://opencode.ai/docs/zen/) · [opencode.ai/data](https://opencode.ai/data)
>
> 🆕 **Oct 16 refresh — the new stuff:** **Gemini 4 Argon Contributor** (AA 53, $60/mo 2× promo, trains on data) and **Beam Free** joined Go; **Step 5 Preview free→paid** ($60/mo 4× promo; open weights out Oct 15); **Grok 4.6 / Kimi K2.6 / MiniMax M2.7 removed**; Zen gained free **DeepSeek V4.1 Flash**, free **GLM-5.3-Flash**, **Space Bunny Free** and stealth **LL Alpha**. Go is now **29 models**.

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
- After limits, you can always keep using the **free models** — now a much stronger floor: **DeepSeek V4.1 Flash Free, GLM-5.3-Flash Free, Beam Free, Space Bunny Free, LongCat 2.5 Preview Free**, plus Zen free models (Oct 16).

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
| Kimi K2.6 (removed from Go docs Oct 16; Zen only) | $0.95 | $4.00 | $0.16 | — | — | — |
| LongCat-2.0 | $0.30 | $1.20 | $0.006 | — | $60 | $240 |
| LongCat 2.5 Preview Free | Free | Free | Free | — | **Unlimited\*** | Unlimited\* |
| Step 5 Preview (was Free) | $1.00 | $2.70 | $0.10 | — | ~~$15~~ **$60** (4× promo) | ~~$60~~ **$240** |
| Beam Free | Free | Free | Free | — | **Unlimited\*** | Unlimited\* |
| MiMo-V2.6-Flash | $0.14 | $0.28 | $0.0028 | — | $60 | $120 |
| MiMo-V2.6-Pro | $0.435 | $0.87 | $0.003625 | — | **$15** | $60 |
| MiMo-V2.5 | $0.14 | $0.28 | $0.0028 | — | $60 | $120 |
| MiMo-V2.5-Pro | $0.435 | $0.87 | $0.003625 | — | **$15** | $60 |
| MiniMax M3 | $0.30 | $1.20 | $0.06 | — | $60 | $180 |
| MiniMax M2.7 (removed from Go docs Oct 16, deprecated; Zen only) | $0.30 | $1.20 | $0.06 | $0.375 | — | — |
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
| Grok 4.6 (removed from Go docs; Zen only) | $2.00 | $6.00 | $0.50 | — | — | — |
| GPT 6 Luna ≤272K | $0.10 | $0.50 | $0.01 | $0.125 | **$15** | $60 |
| GPT 6 Luna >272K | $0.20 | $0.75 | $0.02 | $0.25 | **$15** | $60 |
| GPT 5.6 Luna ≤272K | $0.20 | $1.20 | $0.02 | $0.25 | **$15** | $60 |
| GPT 5.6 Luna >272K | $0.40 | $1.80 | $0.04 | $0.50 | **$15** | $60 |
| Claude Haiku 5.5 ≤100K | $0.10 | $0.50 | $0.01 | $0.125 | **$15** | $60 |
| Claude Haiku 5.5 >100K | $0.50 | $2.50 | $0.05 | $0.625 | **$15** | $60 |
| **Gemini 4 Argon Contributor** | $4.00 | $20.00 | $0.20 | — | ~~$30~~ **$60** (2× promo) | ~~$120~~ **$240** |
| Space Bunny | $0.15 | $0.60 | $0.03 | — | **$30** | $120 |

\* Limited-time free previews. LongCat 2.5's free window was announced as ~2 weeks (to about Oct 10, 2026) but is **still listed free on Oct 16**. **Step 5 Preview's free window ended ~Oct 15** — it is now paid ($1/$2.70/$0.10) with a 4× monthly promo ($60 Go / $240 Plus, limited time); its open weights shipped Oct 15 (BF16 + FP8). **Beam Free** (Reflection AI's Beam) is free for a limited time and **not available in several regions** (incl. China, Russia, Iran, Nigeria); 30-day retention, no training.

### DeepSeek peak/off-peak

DeepSeek models are 2× more expensive during **peak = 01:00–04:00 and 06:00–10:00 UTC, Monday–Friday** (excluding Chinese holidays). Everything else — including all weekend — is half price. For an IST-based schedule (UTC+5:30) that means peak is roughly **06:30–09:30 and 11:30–15:30 IST**; evenings, nights and weekends are off-peak. Scheduling long autonomous runs off-peak effectively **doubles your DeepSeek headroom**.

Source: [DeepSeek pricing docs](https://api-docs.deepseek.com/quick_start/pricing).

---

## 3. The full Go roster (29 models)

Verified live on Oct 16, 2026, from [opencode.ai/docs/go](https://opencode.ai/docs/go/) and the machine's own `/models` list:

**Frontier / high-intelligence**
- Grok 4.7 (xAI) — Grok 4.6 was removed from Go docs (still on Zen)
- Kimi K3, Kimi K2.7 Code (Moonshot) — K2.6 removed from Go docs (Zen only)
- GLM-5.3, GLM-5.3-Flash, GLM-5.2 (Z.ai / Zhipu)
- Qwen3.8 Max, Qwen3.8 Flash, Qwen3.7 Plus (Alibaba)
- GPT 6 Luna, GPT 5.6 Luna (OpenAI)
- Claude Haiku 5.5 (Anthropic) — fastest Claude, 1M ctx, adjustable effort, subagent star
- **Gemini 4 Argon Contributor (Google) — NEW Oct 13: AA 53, Vals #1 of 41, $60/mo 2× promo — ⚠️ trains on your data**

**Workhorses / volume**
- DeepSeek V4.1 Flash, DeepSeek V4 Pro — V4 Flash / Vision Exp fully retired (Zen/legacy only)
- MiMo-V2.6-Pro, MiMo-V2.6-Flash, MiMo-V2.5-Pro, MiMo-V2.5 (Xiaomi)
- MiniMax M3 — M2.7 removed from Go docs (deprecated)
- LongCat-2.0 (Meituan)
- Hy4 preview, Hy3 (Tencent)
- Muse Spark 1.3 Contributor, Muse Spark 1.2 Contributor (Meta)
- Space Bunny (paid $0.15/$0.60, $30/mo)

**Newly paid / free / stealth (limited time)**
- **Step 5 Preview (StepFun) — was free, now paid $1/$2.70/$0.10 with a $60/mo 4× promo; open weights released Oct 15**
- **Beam Free (Reflection AI) — NEW Oct 12: 501B/23B MoE, AA 30, free, 30-day retention (no training), limited regions**
- LongCat 2.5 Preview Free (still free Oct 16, well past its initial ~Oct 10 window)

**Recently removed/deprecated from the roster (Sep–Oct 2026):** Grok 4.6, Kimi K2.6, MiniMax M2.7, DeepSeek V4 Flash/Vision Exp, GLM-5.1, Qwen3.7 Max, Qwen3.6 Plus, MiniMax M2.5, Kimi K2.5, GLM-5. Pipeline churn is real — re-check the docs monthly.

---

## 4. Free and stealth models (important fine print)

Zen/Go free models as of Oct 16, 2026 ([Zen docs](https://opencode.ai/docs/zen/), [Go docs](https://opencode.ai/docs/go/)):

| Model | Notes |
|---|---|
| **DeepSeek V4.1 Flash Free** | **NEW.** Free on Zen for a limited time; provider follows **zero-retention, no training**. The free twin of your daily driver (AA 39) — the best free workhorse ever offered on OpenCode. Use as the bulk floor. |
| **GLM-5.3-Flash Free** | **NEW.** Free on Zen for a limited time; **zero-retention, no training**. AA 42 — the highest-scoring free model OpenCode has offered outside stealths. |
| **Beam Free** | **NEW Oct 12.** Reflection AI's Beam (501B/23B MoE, AA 30, Apache-2.0 weights). Free, limited regions (not in China/Russia/Iran/Nigeria etc.), **30-day retention, no training**. Community nickname "Cat Jam". |
| **Space Bunny Free** | **Back as a Zen stealth free** while the paid Go SKU continues at $30/mo. Zero-retention, no training. Identity unconfirmed (MiniMax-family fingerprint). |
| **LL Alpha Free** | **NEW stealth.** 256K ctx; **30-day retention and data may be used to improve the model** — do not use for sensitive work. |
| **LongCat 2.5 Preview Free** | Still free Oct 16, well past the initial ~Oct 10 estimate. Zero-retention per provider. No public benchmarks or model card. |
| **Nemotron 3.5 Super VL Free** | **NEW.** NVIDIA vision model; trial terms — logged, do not submit personal/confidential data. |
| Big Pickle | Zen stealth; **data may be used to improve the model** — do not use for client/PHI work. |
| MiMo-V2.6-Flash Free / MiMo-V2.5 Free | Data may be used for training during free period. |
| Nemotron 3 Ultra / 3.5 Lightning Free | NVIDIA trial endpoints; data logged, **do not submit personal/confidential data**. |
| Muse Spark 1.3 Contributor Free | Discounted in exchange for permission to train on prompts/completions. |
| Jev 1.13 Free / Exo Free | TypeSafe structured-decision model (not a chat model) / Zen stealth collecting feedback (may train; docs-listed, not in this machine's `/models`). |

**Both paid "Contributor" SKUs on Go (Muse Spark 1.3/1.2, Gemini 4 Argon) train on your data** — they are the cheap contributor tiers. For medical/insurance/client work, use a non-contributor model or a zero-retention provider. The new **free DeepSeek + free GLM** twins are the safest high-capacity free options: zero-retention and strong enough for real (non-critical) work.

---

## 5. `opencode.ai/data` — what the whole user base actually runs

From the live telemetry page (7 days ending Oct 16, 2026, tokens):

| # | Model | Weekly tokens | Change |
|---|---|---|---|
| 1 | deepseek-v4.1-flash | 64T | +64% |
| 2 | muse-spark-1.3-contributor | 38T | −3% |
| 3 | space-bunny | 20T | −55% |
| 4 | mimo-v2.6-flash | 10T | −19% |
| 5 | step-5-preview | 5.6T | **+267%** (free-launch surge) |
| 6 | nemotron-3-ultra (free) | 4T | −4% |
| 7 | deepseek-v4-flash (legacy) | 3.3T | −32% |
| 8 | glm-5.3-flash | 2.5T | +23% |
| 9 | longcat-2.5-preview (free) | 2T | −12% |
| 10 | **beam (NEW, free)** | 990B | **New** |
| 11 | nemotron-3.5-lightning | 853B | +53% |
| 12 | gpt-6-luna | 698B | +2% |
| 13 | deepseek-v4-pro | 477B | 0% |
| 14 | deepseek-v4-flash-vision-exp (legacy) | 466B | −26% |
| 15 | mimo-v2.6-pro | 440B | −6% |
| 16 | muse-spark-1.2-contributor | 336B | −16% |
| 17 | mimo-v2.5 | 330B | −42% |
| 18 | claude-haiku-5-5 | 273B | **+237%** |

Cache ratios (share of input served from cache): space-bunny 96.7%, **deepseek-v4.1-flash 96.2%**, step-5-preview 95.4%, beam 95.3%, muse-spark-1.3 95.1%, mimo-v2.6-flash 93.6%, glm-5.3-flash 93.1%.

**Takeaway:** the crowd's revealed preference is overwhelmingly the cheap, high-cap models — not Kimi K3/Grok. Session costs (Oct 16): Space Bunny Free ≈ $0.0006/session, Step 5 Preview $0.0007, MiMo-V2.6-Flash $0.0023, Muse Spark 1.3 $0.0041, GLM-5.3-Flash $0.0777, DeepSeek V4.1 Flash $0.0435. **DeepSeek V4.1 Flash is now the crowd's undisputed #1 (64T/week, +64%)**, and Beam entered at #10 in its first week — a strong signal for the free model.

---

## 6. What changed Aug → Oct 2026 (brief history)

| Date | Change |
|---|---|
| Aug 12 | Grok 4.6 added (removed from Go docs Oct 16) |
| Aug 14 | GLM-5.3 added — at a $15/mo allowance, prompting user backlash ("1/4 the usage of GLM-5.2") |
| Aug 20–26 | "Ox Alpha" stealth ran free on Go, revealed as **GLM-5.3-Flash**; allowance later raised to $60 |
| Aug 24 | First-month $5 discount discontinued |
| Aug 26–28 | Qwen3.8 Flash and Hy4 preview added |
| Sep 2–4 | Muse Spark 1.3 Contributor added |
| Sep 10 | **DeepSeek V4.1 Flash** added with a 4× usage promo (raised to $80 on Oct 8) |
| Sep 21–22 | **Grok 4.7, GPT 6 Luna, MiMo-V2.6 Flash/Pro** added |
| Sep 23 | Space Bunny free stealth added |
| Sep 25 | LongCat 2.5 Preview Free added |
| **Sep 28** | **Go Plus ($40) launched**; v1.18.33 |
| Sep 30 | v1.18.34; very recent deprecations of GLM-5.1, Qwen3.7 Max, etc. |
| **Oct 7** | **Claude Haiku 5.5 released (Anthropic) and added to Go** ($0.10/$0.50 ≤100K, $15/mo) |
| **Oct 8** | **Step 5 Preview Free added to Go** (StepFun 600B/27B MoE, AA 44); **DeepSeek V4.1 Flash cap raised $60 → $80** (Plus $120 → $160); DeepSeek ZDR renewed through Oct 31 |
| **Early Oct** | **Space Bunny converted from free preview to paid** ($0.15/$0.60/$0.03, $30/mo Go, $120 Plus) |
| **Oct 12** | **Beam Free added** (Reflection AI Beam, 501B/23B MoE, AA 30) — free stealth, community nickname "Cat Jam"; Meta releases Muse Wonder/Wonder Full (AA 52/56, not on Go) |
| **Oct 13** | **Gemini 4 Argon Contributor added to Go** ($4/$20/$0.20, ~~$30~~ $60/mo 2× promo; trains on data); Grok 4.6 / Kimi K2.6 / MiniMax M2.7 removed from docs; MiniMax M2.7 deprecated |
| **Oct 14–15** | **Step 5 Preview free window ends → paid $1/$2.70/$0.10 (4× promo $60/mo)**; **open weights released Oct 15** (BF16 + FP8, HuggingFace/ModelScope); **Zen free-model wave:** DeepSeek V4.1 Flash Free, GLM-5.3-Flash Free, Space Bunny Free, LL Alpha Free, Nemotron 3.5 Super VL Free |
| **Oct 16** | Telemetry: DS V4.1 Flash new #1 (64T/wk); Beam enters #10; docs refresh confirmed 29-model Go roster; v1 1.19.3, v2 2.0.31 |

Sources: [opencode.ai/changelog](https://opencode.ai/changelog), [julien.cloud/opencode-go-models](https://julien.cloud/opencode-go-models/), [Go docs](https://opencode.ai/docs/go/), [Zen docs](https://opencode.ai/docs/zen/), [opencode.ai/data](https://opencode.ai/data).

---

## 7. Reliability caveats (community-reported)

- OpenCode's own router quality has varied: users report 429s/503s on hot models during demand spikes, and occasional doc-vs-router mismatches (a model disappearing while still listed — DeepSeek V4.1 Flash and Hy4 briefly vanished from the Go listing on Oct 14 before being restored).
- There are open GitHub issues about the **monthly usage meter not matching spend** (anomalyco/opencode #43032) — treat the console meter as approximate and keep a margin.
- Free models are intended for the OpenCode client; some report 403s when used through other clients.
- **The free tier is high-churn** — Step 5 Free ended within a week, Space Bunny flipped free→paid→free (stealth), so keep a fallback lane configured for every free model you rely on.
- Provider quantization varies for OpenRouter, but OpenCode states it does not quantize the Go-served models it validated.

---

**Next:** [02 — Benchmarks](./02-benchmarks.md) · [03 — Task Playbook](./03-task-playbook.md) · [04 — Limits & Burn Rate](./04-limits-and-burn-rate.md) · [05 — Intelligence per Dollar](./05-intelligence-per-dollar.md)
