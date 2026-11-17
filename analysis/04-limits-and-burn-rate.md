# 04 — Limits, Requests & Realistic Continuous Programming

> **Snapshot: October 1, 2026; refreshed October 13, 16, 25 and November 17, 2026 (full AA v5.0.1 re-baseline + provider-side measured usage).** Usage history remains **Sep 15–Oct 1** (from the primary machine’s v1 DB) as the frozen calibration (§1); the new **§0** adds **provider-side measured usage (Nov 17, both Go accounts, all machines)** — now the primary basis for capacity math. Caps and prices re-verified live **Nov 17**. No session content or client data is used — only aggregate token counts.
>
> 🆕 **Nov 17 — the new stuff:** new **§0** with provider-side measured usage (**24,160 requests/30d, $46.44 list, DeepSeek $0.00190/req at a 28% peak share — lower than the frozen 40% assumption**) and the **meter discrepancy callout** (console $60 vs docs $100 — plan on $100; bug anomalyco/opencode#43032). Capacity tables now carry **both profiles**: **measured (3,477/768/166k — realistic fleet average, subagent traffic included)** and **heavy (7.8k/1.1k/146k — conservative)**. DeepSeek V4.1 Flash's cap is **$100** (5h $20 / week $50; **10×** face value; **52,632 req/mo measured / 32,258 heavy**). New pricing findings: **MiniMax M3 >512K tier**, **Qwen3.7 Plus >256K tier**, **Haiku >100K tier**, Grok/GPT long-context tiers, and **Hy4 (GA) ≠ Hy4 preview — separate SKUs**. **Go Teams** = $20/member/mo (**2-member minimum — $40/mo**; second seat free for the next member) with +$5 on every model cap; Extra Usage on by default. DeepSeek ZDR is renewed monthly (**through Nov 30, 2026**).
> 🆕 **Oct 25 — the new stuff:** (heavy-mix figures) **K3.1 Pro gives ~269 heavy requests/month** (5h: 54, week: 134). **M3.1 Flash gives ~4,975/month** (5h: 995, week: 2,488). **Argon gives ~728/month** at the 50%-off $30 cap. **Step 5 is back to ~591/month** at $15. The fresh v2 DB (Oct 25) confirmed the frozen profile within ~5%.

---

## 0. Provider-side measured usage (Nov 17 — both Go accounts, all machines; figures as of the Nov 17 pull)

This is the realistic fleet picture straight from the provider's console API (undocumented but verified working with a Go API key), across **both Go accounts and every machine** — not one box's local DB. It is the **primary basis** for value/capacity math in [05](./05-intelligence-per-dollar.md); the frozen heavy profile in §1 stays as the conservative secondary column.

**Accounts:** `alikhan37544` (Go sub, period Oct 24–Nov 24, UPI/INR, **Extra Usage OFF**, $25.00 credit balance) + `frisky.business.now` (second identity; usage records exist but **no active meter returned** — open question).

**30-day usage (combined, per model):**

| Model | Requests | Tokens (in / out / cache-read) | List value | $/req |
|---|---|---|---|---|
| deepseek-v4.1-flash | 19,040 | 66.2M / 14.6M / 3.16B | $36.11 | $0.00190 |
| muse-spark-1.3-contributor | 4,708 | 19.2M / 2.5M / 594M | $3.61 | $0.00077 |
| kimi-k3.1-pro | 118 | 13.3k in / 153k out / 11.5M cache-read + 1.42M cache-write (combined; 0.897M alikhan + 0.519M frisky) | $6.69 | $0.0567 |
| gpt-6-luna | 60 | tiny title-gen style calls, almost no cache | $0.03 | — |
| beam-free | 233 | free | $0 | — |
| iceman-contributor-free | 1 | free | $0 | — |
| **Total** | **24,160** | — | **$46.44 list** | **$0.00192 avg** |

**Measured fleet profile (per request):** **3,477 input / 768 output+reasoning / 165,979 cache-read** (cache-write ≈5k/req only where billed — measured: K3.1 Pro 7,604/req, GPT-6 Luna 3,324/req). It **includes subagent traffic**, so it is the realistic fleet average. Against it, the **frozen heavy profile** (§1): 7,800 / 1,100 / 146,000 → DeepSeek $0.0031/req. DeepSeek's measured **peak share ≈ 28%** ($36.11 billed vs $28.18 off-peak-only) — the freeze assumed **40%**.

**Current Go period (Oct 24 – Nov 24, `alikhan37544`), MTD through Nov 17:** **20,405 requests, $37.75 list value** (all models). Busiest days: **Nov 9 — 6,819 req / $10.33 / 1.16B tokens**, **Nov 11 — 4,413 req / $8.48 / 774M tokens**; also Nov 3 (1,494 req / $1.75) and Oct 28 (1,015 req / $2.21); several zero-usage days (Oct 24/27/31, Nov 4/7/8/13/14). MTD per model: deepseek-v4.1-flash 18,164 · muse-spark-1.3 2,128 · kimi-k3.1-pro 74. 7-day window: deepseek 7,205 req, gpt-6-luna 21 req.

**Console meter status (Nov 17):** 5h **6%** ($0.73/$12) · week **6%** ($1.82/$30) · month **55%** ($33.44/$60) — resets Nov 24.

⚠ **Meter discrepancy — flagged, NOT resolved:** the console's monthly meter shows a **$60** limit while the docs list DeepSeek's cap at **$100** (history: $60 → $80 (Oct 8) → $100 (late Oct)). The **single meter set is exactly what the rewritten docs predict** — "the paid models you use on Go share one allowance" — one pool with 20/50/100 sub-limits; "used" ($33.44) ≈ DeepSeek-only MTD spend and the $60 reading ≈ the pre-Oct-8 DeepSeek cap. Hypotheses: (a) a **stale per-model meter** still showing the pre-Oct-8 value; (b) an account-level pool metered at **allowance** value (docs: each response reports `opencode.allowance`) which under-reports vs list ($37.75 MTD list). Known meter-accuracy bug: **anomalyco/opencode#43032**. → **Plan against the docs' $100**; treat the meter reading as verbatim telemetry with this caveat.

*(Local `opencode stats --all` on this box: 232 sessions · 759 subagents · 2,166 prompts · 43.7k steps · 5.7B tokens · est. $247.02 lifetime · 99.0% tool success · 117 active days. Local cost tables ≠ provider billing — never reconcile directly.)*

---

## 1. Your real usage profile (Sep 15 – Oct 1, 2026)

This is the **frozen calibration** — the basis for the "heavy mix" column throughout the repo (7.8k in / 1.1k out / 146k cache, DeepSeek $0.0031/req). It stays frozen as the conservative secondary basis; §0's measured profile is primary.

| Metric | Value |
|---|---|
| Model | `opencode-go/deepseek-v4.1-flash` @ **max** effort |
| Requests (assistant messages) | **12,973** |
| Input tokens | **101.5M** |
| Output + reasoning tokens | **14.21M** |
| Cache-read tokens | **1,893M** (96% of input!) |
| Cache-write tokens | ~1.3M |
| Recorded cost | $29.43 (DB, Zen-style prices) |
| **Cost at Go peak/off-peak pricing** | **≈ $39.05** |
| Average per request | **7.8k input, 1.1k output+reasoning, 146k cache read** |
| Average cost per request (Go blend) | **$0.0031** (0.31¢) |
| Sessions | 232 (≈ 56 requests/session) |
| Days active | 16 (avg 811 req/day) |

### Oct 25 sanity check (fresh v2 DB, all-time)

The second machine’s v2 DB now has enough history to check the frozen profile:

| Model | Assistant msgs | Avg in / out+reasoning / cache | Avg $/msg |
|---|---|---|---|
| `deepseek-v4.1-flash` | 1,419 | 8.2k / 1.25k / 153k | $0.00244 |
| `gemini-4-argon-contributor` (old SKU/pricing) | 565 | 10.9k / 0.77k / 134k | $0.0857 |
| `kimi-k3.1-pro` | 96 | — | $0.0383 |
| `muse-spark-1.3-contributor` | 4,966 | — | $0.00079 |
| `gpt-5.6-luna` | 3,850 | — | — |
| `deepseek-v4-flash` (retired) | 3,811 | — | — |
| `deepseek-v4-pro` (retired) | 2,506 | — | — |

The paid DeepSeek lane is **8.2k in / 1.25k out / 153k cache** — within ~5% of the frozen 7.8k/1.1k/146k. The Argon row is the old Contributor SKU at the old $0.0857 pricing; the current Go SKU is `gemini-4-argon` at $2/$10/$0.10 with a $30 cap. **The calibration stays frozen**; the v2 DB is a consistency check, not a new baseline.

### Your peak intensity (measured, not estimated)

| Window | Max observed | Cap on DS V4.1 Flash | Headroom used |
|---|---|---|---|
| Requests per hour | **630** | — | — |
| Requests per 5h | **1,953** | ~5,097 ($16) | **38%** |
| Requests per 24h | **3,146** | — | — |
| Requests per 7d | **7,036** | ~12,742 ($40) | **55%** |
| 16-day spend | **$39.05** | $80/month | **49%** |
| Max rolling 5h spend | **$5.99** | $16 | **37%** |
| Max rolling 7d spend | **$24.77** | $40 | **62%** |
| Max rolling 24h spend | **$8.97** | — | — |

**The key insight:** you barely dent the **5-hour** window (peak 37% of the $16 cap) and the weekly peak sits at **62%** of the $40 cap. At your current pace (~$5–8/day recently) you project to **$45–73/month — under the $80 cap in normal months, binding only in crunch months** (caps at the time of this measurement; DeepSeek's cap has since risen to **$100** — 5h $20 / week $50 — so there is even more headroom now).

---

## 2. Why the vendor's "estimated requests" look so much higher than your reality

The vendor estimates assume a light request (e.g. DeepSeek: 410 input / 71,300 cached / 310 output per request; GLM-5.3-Flash 1,000/55,000/200; K3.1 Pro 1,050/76,500/300; Haiku 1,100/55,000/240; MiMo-Flash 830/71,500/295; Muse 620/71,400/300; Qwen4 Max 420/66,000/200). You run far heavier — **3,477 input / 166k cached / 768 output (measured fleet mix)** or 7.8k / 146k / 1.1k (frozen heavy mix). The multiplier:

### The estimate-table multiplier update (Nov 17 — Console values)

**Source: Console Go page estimates (per 5h); week/month derived ×2.5/×5.** The docs no longer publish the tables — they defer to the Console (console/go#pricing, console/go#limits) as of Nov 17.

| Model | Console est. req/month (derived ×5) | **Measured req/mo** | Heavy req/mo | Ratio (console ÷ measured) |
|---|---|---|---|---|
| DeepSeek V4.1 Flash 1017 | 216,500 | **52,632** | 32,258 | 4.1× |
| GLM-5.3-Flash | 31,600 | **10,196** | 9,836 | 3.1× |
| MiMo-V2.6-Flash | 150,500 | **51,433** | 33,171 | 2.9× |
| MiMo-V2.6-Pro | 16,300 | **5,391** | 3,074 | 3.0× |
| Muse Spark 1.3 | 226,500 | **72,007** | 46,440 | 3.1× |
| GPT 6 Luna | 21,150 | **4,973** | 5,376 | 4.3× |
| Claude Haiku 5.5 (≤100K) | 19,250 | **4,973** | 5,376 | 3.9× |
| **Gemini 4 Argon** | 2,830 | **961** | 728 | 2.9× |
| **Kimi K3.1 Pro** | 735 | **259** | 269 | 2.8× |
| **MiniMax M3.1 Flash** | 19,400 | **5,760** | 4,975 | 3.4× |
| **Step 5 Preview** | 2,130 | **677** | 591 | 3.1× |
| **Qwen4 Max** | 2,315 | **492** | 543 | 4.7× |
| **Hy4 (GA)** | 13,550 | **5,088** | 3,899 | 2.7× |
| Kimi K3 | 490 | **173** | 179 | 2.8× |
| Grok 4.7 | 845 | **159** | 158 | 5.3× |
| MiniMax M3 | 16,050 | **5,032** | 4,831 | 3.2× |
| LongCat-2.0 | 57,000 | **20,266** | 13,228 | 2.8× |

So yes — for heavy agentic users, take the vendor's request counts and divide by **2–5×** (measured basis) or **3–7×** (heavy basis). Console Go-page estimates (per 5h; week/month = derived ×2.5/×5): DS 43,300/108,250/216,500 · GLM-5.3-Flash 6,320/15,800/31,600 · K3.1 Pro 147/368/735 · Haiku 3,850/9,625/19,250 · Argon 566/1,415/2,830 · M3.1 Flash 3,880/9,700/19,400 · Qwen4 Max 463/1,158/2,315 · Hy4 2,710/6,775/13,550 · Hy4 preview 1,350/3,375/6,750. *(The docs' own tables are gone — they defer to the Console: console/go#pricing, console/go#limits, as of Nov 17.)*

---

## 3. The definitive capacity table (both profiles — measured & heavy)

Cost per request is shown on the **heavy mix** (7.8k in / 1.1k out+reasoning / 146k cache; DeepSeek at the old ~40% peak blend → $0.0031/req) — the conservative column. The **Req/mo (measured)** column is the realistic fleet average from §0 (3,477/768/166k, subagent traffic included; DeepSeek $0.00190 at the measured 28% peak blend) and is the primary basis in [05](./05-intelligence-per-dollar.md). **Req/5h / Req/week / Sessions / Continuous are heavy-mix numbers** (sub-limits: 5h = 20% of monthly, weekly = 50%). “Sessions” assumes 50 requests per typical session. **Bold** = can sustain your current pace.

| Model | $/req (heavy) | Req/5h | Req/week | Req/mo (heavy) | **Req/mo (measured)** | Sessions/mo | Continuous hours¹ | Sustains your pace? |
|---|---|---|---|---|---|---|---|---|
| **GLM-5.3-Flash Free** | $0 | ∞ | ∞ | **∞** | **∞** | ∞ | ∞ | ✅ (zero-retention) |
| **DeepSeek V4.1 Flash Free** | $0 | ∞ | ∞ | **∞** | **∞** | ∞ | ∞ | ✅ (zero-retention) |
| Beam Free | $0 | ∞ | ∞ | **∞** | **∞** | ∞ | ∞ | ✅ (no training, 30-day) |
| **Muse Spark 1.3 Contrib** | $0.0013 | 9,288 | 23,220 | **46,440** | **72,007** | 929 | ∞ (>24h) | ✅ (trains on data) |
| MiMo-V2.6-Flash | $0.0018 | 6,634 | 16,586 | **33,171** | **51,433** | 663 | ∞ (>24h) | ✅ |
| **DeepSeek V4.1 Flash** | $0.0031 | 6,452 | 16,129 | **32,258** | **52,632** | 645 | ~10.2h | ✅ ($100 cap) |
| LongCat-2.0 | $0.0045 | 2,646 | 6,614 | 13,228 | 20,266 | 265 | ~4.2h | ❌ |
| GLM-5.3-Flash | $0.0061 | 1,967 | 4,918 | 9,836 | 10,196 | 197 | ~3.1h | ❌ (weekly in ~5 heavy days) |
| Hy3 | $0.0068 | 1,754 | 4,386 | 8,772 | 8,900 | 175 | ~2.8h | ❌ |
| Qwen3.8 Flash | $0.0040 | 1,491 | 3,729 | 7,457 | 6,611 | 149 | ~2.4h | ❌ |
| **MiniMax M3.1 Flash** | **$0.0040** | **995** | **2,488** | **4,975** | **5,760** | **99.5** | **~1.6h** | ❌ (paid quality/value lane) |
| MiniMax M3 | $0.0124 | 966 | 2,415 | 4,831 | 5,032 | 97 | ~1.5h | ❌ |
| Claude Haiku 5.5 (≤100K)² | $0.0028 | 1,075 | 2,688 | 5,376 | 4,973 | 108 | ~1.7h | ❌ (subagent use is fine) |
| GPT 6 Luna | $0.0028 | 1,075 | 2,688 | 5,376 | 4,973 | 108 | ~1.7h | ❌ |
| Hy4 (GA) | $0.0154 | 780 | 1,950 | 3,899 | 5,088 | 78 | ~1.2h | ❌ |
| **MiMo-V2.6-Pro** | $0.0049 | 615 | 1,537 | **3,074** | **5,391** | 61 | ~1.0h | ❌ (escalation model) |
| GPT 5.6 Luna | $0.0058 | 517 | 1,293 | 2,586 | 2,425 | 52 | ~0.8h | ❌ |
| Hy4 preview | $0.0154 | 390 | 975 | 1,950 | ≈2,544³ | 39 | ~0.6h | ❌ |
| Kimi K2.7 Code | $0.0395 | 303 | 759 | 1,517 | 1,583 | 30 | ~0.5h | ❌ |
| **Gemini 4 Argon** | **$0.0412** | **146** | **364** | **728** | **961** | **14.6** | **~14 min** | ❌ (best hard-task capacity) |
| **Step 5 Preview** | **$0.0254** | **118** | **296** | **591** | **677** | **11.8** | **~11 min** | ❌ (open weights) |
| GLM-5.3 | $0.0537 | 56 | 140 | **279** | **292** | 5.6 | ~5.3 min | ❌ (ration) |
| **Kimi K3.1 Pro** | **$0.0558** | **54** | **134** | **269** | **259** | **5.4** | **~5.1 min** | ❌ (1M ctx / Max-effort ration) |
| Qwen3.8 Max | $0.0587 | 51 | 128 | **256** | **229** | 5.1 | ~4.9 min | ❌ (ration) |
| Qwen4 Max | $0.0276⁴ | 109 | 272 | **543** | **492** | 10.9 | ~10 min | ❌ (ration) |
| Kimi K3 | $0.0837 | 36 | 90 | **179** | **173** | 3.6 | ~3.4 min | ❌ (ration) |
| Grok 4.7 | $0.0952 | 32 | 79 | **158** | **159** | 3.2 | ~3.0 min | ❌ (ration) |

¹ *Continuous hours at your maximum observed burst rate (630 req/h) before the 5h rolling cap bites. “∞” means even at max burst you can’t fill the 5h cap.*

² **Haiku 100K-tier footnote:** the ≤100K row assumes a prompt of **≤100K tokens**. The measured mix (170k prompt) and the frozen heavy mix are both above that boundary, so Haiku is billed at the **>100K tier** — $0.50 input / $2.50 output / $0.05 cache read per 1M: **$0.01508/req measured → 995 req/mo** (heavy: ~$0.014 → 1,075 req/mo, 5h ~215, week ~538). Keep Haiku on explore/subagent contexts under 100K; above that, DeepSeek V4.1 Flash or MiMo-V2.6-Flash is cheaper and stronger.

³ Derived: Hy4 preview's $30 cap ÷ $0.01179/req (measured). ⁴ Qwen4 Max's heavy $/req is derived from the heavy token mix at $1.50/$4.50/$0.075 (excludes cache-write, like all heavy figures); measured $/req is $0.03049.

**Read it like this:** at your observed intensity, one heavy agent task ≈ 50–150 requests. So (measured-profile capacity):
- **K3.1 Pro** gives you **~2–5 substantial tasks/month** (259 req/mo) — the specialist ration (1M ctx, Max effort).
- **Argon** gives **~6–19 heavy tasks/month** (961) — the ceiling and best top-end value (AA 50).
- **Step 5** gives **~5–13 tasks/month** (677).
- **M3.1 Flash** gives **~38–115 tasks/month** (5,760) — the paid quality/value lane.
- **GLM-5.3** gives **~2–6 tasks/month** (292).
- **DeepSeek V4.1 Flash** gives **~350–1,050 tasks/month** (52,632 requests).
- The **free twins are effectively unlimited** (GLM-5.3-Flash Free AA 28; DeepSeek Free not measured on v5.0.1 — 1017 ckpt = 33; zero-retention).

---

## 4. “How long can I keep programming continuously?”

### On DeepSeek V4.1 Flash (your current model, max effort)

- **5-hour window:** your peak 5h used 1,953 requests ≈ $5.99 = **37% of the $16 cap**. You could roughly **triple** your highest observed intensity before throttling. At your max burst rate (630 req/h) you’d need **~8 hours** of unbroken maximum-intensity agent work to fill a 5h window — and because it’s a rolling window, normal work never gets walled.
- **Daily:** you peaked at 3,146 requests/24h ($8.97). Typical heavy day is 2,500–3,000.
- **Weekly:** your heaviest 7 days cost **$24.77 of $40 (62%)**. A crunch week can still throttle by the weekend, but normal weeks clear it.
- **Monthly:** 16 days cost $39.05 (49% of the then-current $80 cap). At the recent ~$5–8/day pace you land at **$45–73/month — under the cap in normal months, binding only in crunch months** (the cap is now **$100** — 5h $20 / week $50 — so even more headroom; §0 shows the current period at $37.75 MTD list).
- **Verdict:** you can program **continuously, all day, at your current pace, effectively all month.** Keep the weekly meter in view during crunch weeks; otherwise use off-peak, shift volume to the cheapest high-coverage lanes, or Zen overflow.

### Shift-to-off-peak cheat code (DeepSeek only)

DeepSeek peak = 01:00–04:00 and 06:00–10:00 UTC Mon–Fri. For IST that’s ~06:30–09:30 and ~11:30–15:30 local. **Evenings, nights and all weekend are 50% off.** Your logs show a lot of activity in 06:00–10:00 UTC (peak) — shifting those same requests to after ~15:30 IST **roughly doubles** your effective monthly capacity (the measured mix already assumes only a 28% peak share — $0.00190/req → 52,632 req/mo; pure off-peak would bill less still).

### On the premium models (K3.1 Pro, Argon, Step 5, M3.1 Flash)

At your intensity these are **minutes-to-hours-per-5h, tasks-per-week** models (measured-profile capacity):
- **Kimi K3.1 Pro:** **~5 minutes** of max-burst work per 5h window (≈52 requests), ~130/week, **259/month** (heavy: 54 / 134 / 269).
- **Gemini 4 Argon:** **~18 minutes** per 5h (≈192), ~480/week, **961/month** (heavy: 146 / 364 / 728) — 3.7× K3.1 Pro's capacity at AA 50.
- **Step 5:** **~13 minutes** per 5h (≈135), ~339/week, **677/month** (heavy: 118 / 296 / 591).
- **MiniMax M3.1 Flash:** **~1.8 hours** per 5h (≈1,152), ~2,880/week, **5,760/month** (heavy: 995 / 2,488 / 4,975) — the only premium-tier model with real daily capacity.

**Plan to use the $15–$30 rations for 1–4 elevated tasks per week**, not as drivers. This matches the community: users who run K3/GLM everywhere burn 73% of their weekly cap in 24 hours.

---

## 5. What Go Plus and Go Teams actually buy

**Go Plus:** $40/mo. Multipliers vs Go are **2×–8×** depending on the model (not a flat 4×):

| Model | Go | Plus | Multiplier |
|---|---|---|---|
| GLM-5.3 | $15 | $120 | **8×** |
| Kimi K3.1 Pro | $15 | $60 | 4× |
| Kimi K3 | $15 | $60 | 4× |
| Grok 4.7 | $15 | $60 | 4× |
| Qwen3.8 Max | $15 | $60 | 4× |
| Qwen4 Max | $15 | $60 | 4× |
| MiMo-V2.6-Pro | $15 | $60 | 4× |
| **Gemini 4 Argon** | $30 | $120 | **4×** |
| **Hy4 preview** | $30 | $120 | **4×** |
| **MiniMax M3.1 Flash** | $20 | $80 | **4×** |
| GPT 6 / 5.6 Luna | $15 | $60 | 4× |
| Claude Haiku 5.5 | $15 | $60 | 4× |
| Step 5 Preview | $15 | $60 | 4× |
| LongCat / Hy3 / Hy4 (GA) | $60 | $240 | 4× |
| GLM-5.2 / MiniMax M3 / K2.7 / Qwen3.7 | $60 | $180 | 3× |
| **GLM-5.3-Flash** | $60 | $180 | 3× |
| **Qwen3.8 Flash** | $30 | $90 | 3× |
| **DeepSeek V4.1 Flash** | **$100** | **$200** | **2×** |
| **MiMo-V2.6-Flash / Muse Spark** | $60 | $120 | **2×** |
| Free models (DS/GLM free, Beam, LongCat 2.5, Hy4 Flash, Iceman) | Free | Free | — |

**Go Teams — $20/member/mo, 2-member minimum ($40/month):** the second seat covers the next member who joins at no extra charge; after that, mid-period joiners pay $20. Every member gets **their own allowance** (shared across models, normalized per model), every model cap gets **+$5/mo** (DeepSeek $100→$105, K3.1 Pro $15→$20, Argon $30→$35, M3.1 Flash $20→$25), and **Extra Usage is ON by default** (falls back to Zen PAYG balance past limits instead of blocking). Sub-limits everywhere: 5h = 20% of monthly, weekly = 50% — of the one shared allowance, per member (see §0 / [01](./01-go-roster-and-limits.md) §2 for the per-model normalization).

**Long-context price tiers (new findings — same cap, doubled/tripled token prices above the threshold):**

| Model | Tier | Input / Output / Cache-read (/ Cache-write) |
|---|---|---|
| MiniMax M3 | ≤512K → **>512K** | $0.30/$1.20/$0.06 → **$0.60/$2.40/$0.12** |
| Qwen3.7 Plus | ≤256K → **>256K** | $0.40/$1.60/$0.04/$0.50 → **$1.20/$4.80/$0.12/$1.50** |
| Claude Haiku 5.5 | ≤100K → **>100K** | $0.10/$0.50/$0.01/$0.125 → **$0.50/$2.50/$0.05/$0.625** |
| Grok 4.7 | ≤200K → **>200K** | $2/$6/$0.50 → **$4/$12/$1** |
| GPT 6 Luna | ≤272K → **>272K** | $0.10/$0.50/$0.01/$0.125 → **$0.20/$0.75/$0.02/$0.25** |
| GPT 5.6 Luna | ≤272K → **>272K** | $0.20/$1.20/$0.02/$0.25 → **$0.40/$1.80/$0.04/$0.50** |

Also new: **Hy4 (GA) ($60/$240/$65) ≠ Hy4 preview ($30/$120/$35)** — separate SKUs at identical token prices; and **Gemini 4 Argon is 50%-off ($2/$10/$0.10) through Nov 30** (list returns to $4/$20/$0.20).

**So:** Go Plus is **great if you live on GLM-5.3 (+8×) or the $15-tier rations (+4×)** — and it also quadruples Argon's cap to $120, Hy4 preview's to $120 and M3.1 Flash's to $80. It is **poor value if your daily driver is DeepSeek V4.1 Flash, MiMo-V2.6-Flash or Muse Spark (only 2×)**. For a DeepSeek-heavy workflow, **Go + $30 of Zen overflow** gives more total capacity with full flexibility for the same $40. Community verdict on Plus was mixed (“4× price for 3× limits”).

---

## 6. Community burn-rate reality check

- *“Hit 73% weekly limit in 24 hours”* — Kimi K3, r/opencode, Aug 30, 2026. Top reply: *“OC go is worthless for the expensive models, only worth it for MiMo, possibly a bit of deepseek.”*
- *“You only get $15 total per month [K3]; the 5 hr limit is $12 which is actually $3 in Kimi usage.”* — r/opencode, Aug 4, 2026.
- *“I hit the 5 hour usage today — using DS flash for gods sake.”* — r/opencode.
- *“It’s limited usage for Kimi 3, GLM, and Qwen Max, but for the rest… a billion+ tokens.”* — happy light user, r/opencodeCLI.
- Measured light user: 109M tokens ≈ “$19.13” over 3 weeks; *“$10 of quota ≈ 35M GLM-5 tokens or 115M MiniMax M2.7 tokens.”*
- Research on agent cost: **~4.17M tokens / ~$1.86 per SWE-bench task** across models (arXiv 2604.22750); Kimi K3’s max vs low thinking effort raises cost **3.6–6.5×** (arXiv 2608.25399). Reasoning effort is the single biggest cost lever you control.

Sources: [r/opencode](https://www.reddit.com/r/opencode/comments/1w2muhx/), [r/opencodeCLI](https://www.reddit.com/r/opencodeCLI/comments/1vbkpk6/), [Patshead](https://blog.patshead.com/2026/03/opencode-go-coding-plan-from-a-light-users-perspective.html), [arXiv 2604.22750](https://arxiv.org/pdf/2604.22750), [arXiv 2608.25399](https://arxiv.org/html/2608.25399).

---

## 7. Practical limit-management playbook

1. **Watch the console, not the 5h window.** The weekly and monthly meters are the ones that bind: [opencode.ai/auth](https://opencode.ai/auth) → usage. ⚠ The monthly meter currently shows **$60** while the docs list DeepSeek's cap at **$100** (see §0 — hypotheses flagged, not resolved; known meter-accuracy bug **anomalyco/opencode#43032**). Plan against the docs' $100 and keep a 10% margin.
2. **Route by role** (see `03-task-playbook.md`): high-volume routine work on DeepSeek V4.1 Flash / M3.1 Flash / MiMo-V2.6-Flash / the free twins; premium models only for planning, hard debugging, design review, and visual verification.
3. **Lower default reasoning effort for bulk work.** Max effort multiplies cost 3.6–6.5×. Use `max` only for planning/hard tasks; `medium`/`low` for routine edits.
4. **Shift DeepSeek work off-peak** (after ~15:30 IST and weekends) for a free 2×.
5. **Keep free models as your floor.** When premium caps run out, **GLM-5.3-Flash Free (AA 28) and DeepSeek V4.1 Flash Free (AA 33 for the 1017 checkpoint; base checkpoint unmeasured)** — both zero-retention — plus **Beam Free (AA 18)** keep you working. **LongCat 2.5 Free / Hy4 Flash Free** are also listed (LongCat needs Regions=Global). **Flint 40B Free / Iceman Contributor Free / MiMo free train on data** — non-sensitive only.
6. **Use the workhorse value lanes.** DeepSeek V4.1 Flash (52,632 req/mo measured, 17,368 AA pts/$) and MiMo-V2.6-Flash (51,433 / 23,145 pts/$) are the volume lanes; **M3.1 Flash** (5,760 req/mo measured, 8,352 pts/$) is the paid quality lane.
7. **When you need headroom:** options in order of cost — (a) off-peak shift, (b) the free twins (real capability, $0), (c) shift volume to the highest solo-coverage lanes (DeepSeek / MiMo-Flash / M3.1 Flash — one shared allowance, normalized per model, so these consume the least of it per request), (d) add Zen balance overflow (DeepSeek at Zen rates; Argon 50% off through Nov 30), (e) Go Plus (best if you use GLM-5.3 or Argon; worst if you use DeepSeek/MiMo/Muse), (f) frontier models via GitHub Copilot or Zen for the 5% hardest work.
8. **Remember free session-title/small-model calls** also consume tiny amounts on cheap models; nothing to optimize there.

---

**Next:** [05 — Intelligence per Dollar](./05-intelligence-per-dollar.md)
