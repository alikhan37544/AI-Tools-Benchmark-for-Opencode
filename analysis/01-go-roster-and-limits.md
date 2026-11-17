# 01 — OpenCode Go: Roster, Plans & Limit Mechanics

> **Snapshot: October 1, 2026; refreshed October 13, 16, 25 and November 17, 2026 (plus a Nov 17 late refresh: AA v5.0.1 re-baseline).** Roster, caps and prices were re-verified against the live docs on **Nov 17**. Usage telemetry remains Sep 15–Oct 1 vintage; benchmark figures were refreshed Oct 25.
> Primary sources: [opencode.ai/docs/go](https://opencode.ai/docs/go/) · [opencode.ai/docs/zen](https://opencode.ai/docs/zen/) · [opencode.ai/data](https://opencode.ai/data) · Console Go page (console/go#pricing, console/go#limits) — <b>the pricing and request-estimate tables moved to the Console (console/go#pricing, console/go#limits); docs defer to Console as of Nov 17</b>. The pricing values below are unchanged (verified against the morning docs + the API catalog — they remain the documented prices).
>
> 🆕 **Nov 17 refresh — the new stuff:** **Go hit 34 in the morning listing and settled at 32 — the roster narrative is 29 → 34 → 32 (MiMo-V2.5/-Pro dropped Nov 17).** Added: **Qwen4 Max** ($1.50/$4.50/$0.075, cache write $1.875, $15 cap, ~543 heavy req/mo; AA 43 on the new v5-era board — not comparable with this file's v4.3.2 figures), **Hy4** GA (same prices as preview, $60 cap → ~3,900 req/mo), **Iceman Contributor Free** (**trains on prompts/completions**), **LongCat 2.5 Free** (returned; ZDR, China-hosted, needs Regions=Global), **Hy4 flash Free** (ZDR). **Step 5 is listed as “Step 5 Preview”** again (same $15 cap). **DeepSeek V4.1 Flash's cap rose $80 → $100** (Go Plus $200) → **~52,632 measured req/mo** (~32,258 at the frozen heavy mix) and a **10× face-value multiplier**. A third plan, **Go Teams ($20/member/mo, 2-member minimum — $40/mo)**, adds $5 to each model cap per member, and **Extra Usage** (opt-in) falls back to PAYG credits instead of blocking. Zen gained **MiniMax M3.1 Flash Free** (zero-retention, no training) as a third free twin. **Gemini 4 Argon's 50% discount ends Nov 30** (then $4/$20/$0.20 at a $60 cap — same ~728 req/mo).
> 🆕 **Nov 17 late refresh — the new stuff:** **AA is fully re-baselined to v5.0.1** (v5.0 landed Oct 27, v5.0.1 Nov 3; harder tasks, four 25% categories) — this file's older AA figures are labeled **(v4.3.2, retired scale)** and are never mixed with v5.0.1 numbers in one comparison. v5.0.1 headlines: **Gemini 4 Argon (50) is now the Go ceiling**, **Kimi K3.1 Pro (46)** drops to #2, **Qwen4 Max (43)** is #3. **Hy4 GA ($60 cap) is a separate SKU from Hy4 preview ($30 cap)** — both are listed in the docs at identical token prices ($0.834/$2.501/$0.042). **MiniMax M3 has a >512K price tier** ($0.60/$2.40/$0.12 vs $0.30/$1.20/$0.06 below 512K). **Go Teams is documented**: **$20/member/mo**, each member gets own limits, **+$5 on every model cap**, **Extra Usage on by default**. **DeepSeek ZDR renewed through Nov 30, 2026** (renewed monthly — re-verify). **LongCat 2.5 Free is China-hosted** (needs Regions=Global opt-in). **Iceman Contributor Free trains on data** (Not ZDR).
> 🆕 **Oct 25 refresh — the new stuff (AA scores below are v4.3.2, retired scale; v5.0.1: K3.1 Pro 46, M3.1 Flash 29):** **Kimi K3.1 Pro** (AA 55, the highest intelligence ever listed on Go at the time) and **MiniMax M3.1 Flash** (AA 43 at $0.22/task) joined the roster. **Space Bunny** and **LongCat 2.5 Preview Free** left it. **Step 5 Preview's 4× promo ended** (back to a $15 cap). **Gemini 4 Argon** is now a plain, 50%-off SKU at **$30/mo**, and — importantly — Go's privacy table now documents it as **not used for training, 0-day retention**. The old "Argon trains on your data" warning is **withdrawn**. Go was 29 models then.

---

## 1. The plans

| Plan | Price | What you get |
|---|---|---|
| **Go** | **$10/mo** | Access to all 32 Go models on **one shared allowance** (each per-model monthly limit shows solo-usage coverage) |
| **Go Plus** | **$40/mo** (launched Sep 28, 2026) | Same models, 2–8× the per-model allowance |
| **Go Teams** | **$20/member/mo** — **2-member minimum ($40/month)**; the second seat covers the next member at no extra charge, then $20 per mid-period joiner | Per-member own limits, **+$5/mo on every model cap**, **Extra Usage on by default** |
| **Zen (pay-as-you-go)** | per token | Same gateway, no monthly caps, list prices; overflow for Go |
| **Free tier** | $0 | Free/stealth models remain usable after Go limits are hit |

- Only **one member per workspace** can subscribe to Go/Go Plus.
- **"Use balance" is now called "Extra Usage."** Enable it on the Go page and Go falls back to your Zen pay-as-you-go balance after a model's limit instead of blocking. ([Go docs → Usage beyond limits](https://opencode.ai/docs/go/))
- After limits you can always keep using the **free models** — currently a capable floor: **GLM-5.3-Flash Free, DeepSeek V4.1 Flash Free, Beam Free**, plus Flint 40B and other trial/stealth models.

---

## 2. How usage limits actually work

The docs were rewritten on Nov 17 and are now explicit — the paid models **share one allowance**:

> *"The paid models you use on Go share one allowance. On Go Teams, each member has their own allowance across models. … Switching models draws from the same allowance. … Each model's monthly limit shows how much usage your plan covers if you use only that model over the month. For example, $1.50 of usage on a model with a $15 limit uses 10% of your monthly allowance. So does $6 on a model with a $60 limit. Go responses report how much each request counted in `opencode.allowance`."* — [opencode.ai/docs/go](https://opencode.ai/docs/go/), Nov 17

Sub-limits: **5-hour = 20%** (rolling, starts on first use) · **weekly = 50%** (resets Mon 00:00 UTC) · **monthly = 100%** of the shared allowance.

So the mechanics are **one shared allowance + per-model normalization**: each model's monthly limit (the $15–$100 figures in the table below) is the plan's coverage **if you use only that model** — the "solo-usage" reading — and switching/mixing models draws from the same pool **proportionally** (each request counts as the fraction of that model's limit it consumes). **The pools are NOT additive:** spending on Kimi K3.1 Pro does draw on the same shared allowance that MiniMax M3.1 Flash uses, just normalized by each model's limit. Every "req/mo" figure in this repo is **solo-usage coverage** (which the docs explicitly endorse as the meaning of the per-model limits).

> ⚠️ **Correction (Nov 17 evening):** earlier versions of this repo claimed *"each model has its own caps: spending on Kimi K3.1 Pro does not consume your MiniMax M3.1 Flash allowance"* and a thesis of "34 independent siloed allowances; the multiplier is not transferable." That was our inference from older, ambiguous docs wording ("each model's monthly limit determines how its usage counts toward those allowances" actually meant shared counting) — the current docs say the opposite. The capacity and value tables remain valid **as solo-usage coverage**; just don't add the per-model pools together. The console's single meter set (one 5h/week/month trio) is consistent with the shared reading — see the meter callout in [04](./04-limits-and-burn-rate.md).

### The pricing table (Go, $/1M tokens)

Prices are identical on Go and Go Plus; only the monthly allowances differ. *(Tables moved to Console: console/go#pricing, console/go#limits — docs defer to Console as of Nov 17; the values below are unchanged — verified against the morning docs + the API catalog, they remain the documented prices.)*

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
| Iceman Contributor Free | Free | Free | Free | — | Unlimited (limited time) | Unlimited |
| LongCat 2.5 Free | Free | Free | Free | — | Unlimited (limited time) | Unlimited |
| Hy4 Flash Free | Free | Free | Free | — | Unlimited (limited time) | Unlimited |
| MiMo-V2.6-Flash | $0.14 | $0.28 | $0.0028 | — | $60 | $120 |
| MiMo-V2.6-Pro | $0.435 | $0.87 | $0.003625 | — | **$15** | $60 |
| **MiniMax M3.1 Flash** ✨ | **$0.15** | **$0.60** | **$0.015** | — | **$20** | **$80** |
| MiniMax M3 ≤512K | $0.30 | $1.20 | $0.06 | — | $60 | $180 |
| MiniMax M3 >512K | $0.60 | $2.40 | $0.12 | — | $60 | $180 |
| Muse Spark 1.3 Contributor | $0.10 | $0.20 | $0.002 | — | $60 | $120 |
| Muse Spark 1.2 Contributor | $0.10 | $0.20 | $0.002 | — | $60 | $120 |
| **Qwen4 Max** ✨ | **$1.50** | **$4.50** | **$0.075** | **$1.875** | **$15** | $60 |
| Qwen3.8 Max | $2.00 | $6.00 | $0.25 | $2.50 | **$15** | $60 |
| Qwen3.8 Flash | $0.15 | $0.47 | $0.016 | $0.20 | $30 | $90 |
| Qwen3.7 Plus ≤256K | $0.40 | $1.60 | $0.04 | $0.50 | $60 | $180 |
| Qwen3.7 Plus >256K | $1.20 | $4.80 | $0.12 | $1.50 | $60 | $180 |
| DeepSeek V4.1 Flash (off-peak) | $0.15 | $0.60 | $0.003 | — | **$100** | $200 |
| DeepSeek V4.1 Flash (peak) | $0.30 | $1.20 | $0.006 | — | **$100** | $200 |
| DeepSeek V4 Pro (off-peak) | $0.66 | $1.98 | $0.022 | — | **$15** | $60 |
| DeepSeek V4 Pro (peak) | $1.32 | $3.96 | $0.044 | — | **$15** | $60 |
| Hy4 (GA) ✨ | $0.834 | $2.501 | $0.042 | — | $60 | $240 |
| Hy4 preview (separate SKU) | $0.834 | $2.501 | $0.042 | — | $30 | $120 |
| Hy3 | $0.14 | $0.58 | $0.035 | — | $60 | $240 |
| Grok 4.7 ≤200K | $2.00 | $6.00 | $0.50 | — | **$15** | $60 |
| Grok 4.7 >200K | $4.00 | $12.00 | $1.00 | — | **$15** | $60 |
| GPT 6 Luna ≤272K | $0.10 | $0.50 | $0.01 | $0.125 | **$15** | $60 |
| GPT 6 Luna >272K | $0.20 | $0.75 | $0.02 | $0.25 | **$15** | $60 |
| GPT 5.6 Luna ≤272K | $0.20 | $1.20 | $0.02 | $0.25 | **$15** | $60 |
| GPT 5.6 Luna >272K | $0.40 | $1.80 | $0.04 | $0.50 | **$15** | $60 |
| Claude Haiku 5.5 ≤100K | $0.10 | $0.50 | $0.01 | $0.125 | **$15** | $60 |
| Claude Haiku 5.5 >100K | $0.50 | $2.50 | $0.05 | $0.625 | **$15** | $60 |
| **Gemini 4 Argon (50% off)** | ~~$4.00~~ **$2.00** | ~~$20.00~~ **$10.00** | ~~$0.20~~ **$0.10** | — | ~~$60~~ **$30** | **$120** |

\* **Beam Free** is free for a limited time and is **not available in several regions** (Angola, Belarus, Cambodia, China/HK/Macau, Cuba, DRC, Equatorial Guinea, Iran, Iraq, Laos, Libya, Nigeria, North Korea, Russia, Syria, Turkmenistan, Uzbekistan, Venezuela, and Crimea/Donetsk/Luhansk). 30-day retention, no training. **Gemini 4 Argon's 50% discount runs through November 30, 2026**; the list price returns after that. **Step 5 Preview's 4× promo ended** — it is back at a $15 Go / $60 Plus cap, still at $1.00/$2.70/$0.10 with open weights.

**Go Teams is $20 per member per month with a 2-member minimum ($40/month)** — the second seat covers the next member who joins at no extra charge; after that, mid-period joiners pay $20. It is not shown as a column because it is mechanical: Teams cap = the Go monthly cap + $5 (e.g. $15 → $20, $20 → $25, $60 → $65, DeepSeek $100 → $105; the Argon $30 discounted cap becomes $35). Extra Usage is **on by default** on Teams. Two more fine-print points: **Hy4 (GA) and Hy4 preview are separate SKUs** at identical token prices — GA carries the $60 cap, preview $30 — and **MiniMax M3 pricing is tiered at 512K tokens** (the >512K tier doubles every rate). The three free SKUs at the top of the table are Go free models for a limited time: **Iceman Contributor Free trains on prompts/completions** (never use it on real work), **LongCat 2.5 Free is China-hosted** (requires the Global region opt-in), **Hy4 Flash Free** is ZDR/no-training.

### DeepSeek peak/off-peak

DeepSeek models are 2× more expensive during **peak = 01:00–04:00 and 06:00–10:00 UTC, Monday–Friday** (excluding Chinese holidays). Everything else — including all weekend — is half price. For IST (UTC+5:30) that is roughly **06:30–09:30 and 11:30–15:30 IST**; evenings, nights and weekends are off-peak. Scheduling long autonomous runs off-peak effectively **doubles** your DeepSeek headroom. Source: [DeepSeek pricing docs](https://api-docs.deepseek.com/quick_start/pricing).

---

## 3. The full Go roster (32 SKUs — verified live Nov 17, 2026; Hy4 GA and Hy4 preview count separately; MiMo-V2.5/-Pro dropped Nov 17)

Verified live on November 17, 2026 (originally the Oct 25 cut), from [opencode.ai/docs/go](https://opencode.ai/docs/go/). **AA scores below are v4.3.2 (retired scale)** where marked; v5.0.1 scores — which are NOT comparable — are in the late-refresh delta at the top and in [02](./02-benchmarks.md).

**Frontier / high-intelligence**
- **Kimi K3.1 Pro (NEW since Oct 25)** — AA 55.1 (v4.3.2, retired scale; v5.0.1: **46**), 1M ctx, vision, $2/$10/$0.20, $15 cap. On v5.0.1 it is the #2 Go model; the ceiling is now Argon.
- **Gemini 4 Argon** — AA 53 (v4.3.2, retired; v5.0.1: **50 — the Go ceiling**), 1M ctx, vision; 50% off through Nov 30; **0-day retention / not used for training**.
- **Qwen4 Max (NEW Nov 17)** — **AA 43 on v5.0.1** (scored natively on the new scale; 0902 snapshot), 984K ctx, $1.50/$4.50/$0.075 (cache write $1.875), $15 cap.
- Grok 4.7 (xAI) — 500K ctx, vision, reasoning low→xhigh.
- Kimi K3, Kimi K2.7 Code (Moonshot).
- GLM-5.3, GLM-5.3-Flash, GLM-5.2 (Z.ai / Zhipu).
- Qwen3.8 Max, Qwen3.8 Flash, Qwen3.7 Plus (Alibaba).
- GPT 6 Luna, GPT 5.6 Luna (OpenAI).
- Claude Haiku 5.5 (Anthropic) — fastest Claude, 1M ctx, adjustable effort.

**Workhorses / volume**
- DeepSeek V4.1 Flash, DeepSeek V4 Pro.
- MiMo-V2.6-Pro, MiMo-V2.6-Flash (Xiaomi).
- **MiniMax M3.1 Flash (NEW since Oct 25)** — AA 43 (v4.3.2, retired; v5.0.1: 29), 141.3 tok/s, 1.25s TTFT, $0.15/$0.60/$0.015, $20 cap.
- MiniMax M3 (tiered pricing above 512K tokens).
- LongCat-2.0 (Meituan).
- **Hy4 (GA) (NEW Nov 17)** and Hy4 preview (Tencent) — two separate SKUs at the same token prices, $60 vs $30 caps. Hy3 (Tencent).
- Muse Spark 1.3 Contributor, Muse Spark 1.2 Contributor (Meta).

**Free / limited time**
- **Beam Free** (Reflection AI) — 501B/23B MoE, AA 30 (v4.3.2, retired; v5.0.1: 18), 30-day retention, no training, limited regions.
- **LongCat 2.5 Free (back Nov 17)** — ZDR/no training, **China-hosted (needs Regions=Global)**.
- **Hy4 Flash Free (NEW Nov 17)** — ZDR/no training.
- **Iceman Contributor Free (NEW Nov 17)** — **trains on prompts/completions** (Not ZDR).
- **Step 5 Preview** is paid again ($1/$2.70/$0.10, $15 cap); open weights released Oct 15.

**Removed this cycle:** **Space Bunny** (revealed Oct 19 as an early MiniMax M3.1 Flash; no free SKU remains) and **LongCat 2.5 Preview Free** (free window ended; LongCat-2.0 remains). **History line (Nov 17):** MiMo-V2.5 and MiMo-V2.5-Pro appeared in the Nov 17 morning listing (stale legacy rows at V2.6-identical prices) and were **dropped from the live catalog later the same day** — the roster went 29 → 34 → 32. Previously removed: Grok 4.6, Kimi K2.6, MiniMax M2.7, DeepSeek V4 Flash/Vision Exp, GLM-5.1, Qwen3.7 Max, Qwen3.6 Plus, MiniMax M2.5, Kimi K2.5.

---

## 4. Free and stealth models (important fine print)

Zen/Go free models as of Nov 17, 2026 ([Zen docs](https://opencode.ai/docs/zen/), [Go docs](https://opencode.ai/docs/go/)):

| Model | Notes |
|---|---|
| **DeepSeek V4.1 Flash Free** | Free on Zen for a limited time; provider follows **zero-retention, no training**. AA 39 (v4.3.2, retired scale). The free twin of the daily driver. |
| **GLM-5.3-Flash Free** | Free on Zen for a limited time; **zero-retention, no training**. AA 42 (v4.3.2, retired; the model scores 28 on v5.0.1) — the best free zero-retention model on the platform. |
| **LongCat 2.5 Free** | **Back on Go (Nov 17).** Free for a limited time; **zero-retention, no training**. ⚠ **China-hosted — needs the Regions=Global opt-in.** Not on AA. |
| **Hy4 Flash Free** | **NEW (Nov 17), on Go.** Free for a limited time; **zero-retention, no training**. Not on AA. |
| **Iceman Contributor Free** | **NEW (Nov 17), on Go.** Free for a limited time but **TRAINS on prompts/completions** (Not ZDR) — non-sensitive exploration only, never client work. Not on AA. |
| **Beam Free** | Reflection AI Beam (501B/23B MoE, AA 30 v4.3.2 retired / 18 on v5.0.1, Apache-2.0 weights). Free, limited regions, **30-day retention, no training**. |
| **Flint 40B Free** | **NEW.** 40B-class free model; **30-day retention and data may be used to improve the model**. Non-sensitive exploration only. |
| **MiMo-V2.6-Flash Free** | Xiaomi free period; data may be used for training. Open-source/non-sensitive work only. |
| **Nemotron 3.5 Super VL Free / Nemotron 3 Ultra / 3.5 Lightning Free** | NVIDIA trial endpoints; data logged, **do not submit personal/confidential data**. |
| **Big Pickle** | Zen stealth; **data may be used to improve the model**. Identity unknown (GLM-family audit); high-variance reliability. |
| **Jev 1.13 Free** | TypeSafe structured-decision model (not a chat model). |

**Removed from the free list this cycle:** Space Bunny Free (paid/removed), LongCat 2.5 Preview Free (window ended), LL Alpha Free, Muse Spark 1.3 Contributor Free, Exo Free.

**The only paid "Contributor" SKUs left on Go are Muse Spark 1.3/1.2 — they still train on your prompts/completions** (and the free **Iceman Contributor Free** trains too). Gemini 4 Argon is **not** a Contributor SKU anymore: Go's table says **"Not used / 0 days"** for Argon. Treat the old Argon-training warning as **withdrawn**, but re-verify before client/PHI work.

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
- **Client support (Go docs, Nov 17):** validated clients are **Hermes, Claude Code, Codex, ZCode, Pi, jcode and Kilo Code CLI**; **DeepSeek Harness, GitHub Copilot Chat, Kimi Code and MiMo Code** are listed with **problematic session support** — prefer a validated client for anything session-heavy.

---

**Next:** [02 — Benchmarks](./02-benchmarks.md) · [03 — Task Playbook](./03-task-playbook.md) · [04 — Limits & Burn Rate](./04-limits-and-burn-rate.md) · [05 — Intelligence per Dollar](./05-intelligence-per-dollar.md)
