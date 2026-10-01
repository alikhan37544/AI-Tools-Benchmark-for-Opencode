# 04 — Limits, Requests & Realistic Continuous Programming

> **Snapshot: October 1, 2026.** This file is calibrated to **your actual OpenCode history** (last 16 days of DeepSeek V4.1 Flash usage, 12,973 requests), not to generic estimates. No session content or client data is used — only aggregate token counts.

---

## 1. Your real usage profile (Sep 15 – Oct 1, 2026)

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

### Your peak intensity (measured, not estimated)

| Window | Max observed | Cap on DS V4.1 Flash | Headroom used |
|---|---|---|---|
| Requests per hour | **630** | — | — |
| Requests per 5h | **1,953** | ~3,823 ($12) | **51%** |
| Requests per 24h | **3,146** | — | — |
| Requests per 7d | **7,036** | ~9,558 ($30) | **74%** |
| 16-day spend | **$39.05** | $60/month | **65%** |
| Max rolling 5h spend | **$5.99** | $12 | **50%** |
| Max rolling 7d spend | **$24.77** | $30 | **83%** ⚠️ |
| Max rolling 24h spend | **$8.97** | — | — |

**The key insight:** you're right that you barely dent the **5-hour** window (peak 50%). But your **weekly** peak hit **83%** of the cap, and at your current pace (~$5–8/day recently) you project to **$45–73/month — i.e. you are on track to touch or exceed the $60 monthly cap for DeepSeek V4.1 Flash near month-end**. It doesn't feel close because the 5h window never walls you; the monthly cap is the one to watch.

---

## 2. Why the docs' "estimated requests" look so much higher than your reality

OpenCode's estimates assume a light request: ~410 input, ~71k cached, ~310 output tokens. You run **7.8k input, 146k cached, 1.1k output+reasoning** — roughly **5–7× heavier per request**. The multiplier:

| Model | Docs est. req/month | **Your calibrated req/month** | Ratio |
|---|---|---|---|
| DeepSeek V4.1 Flash | 130,000 | **19,100** | 6.8× |
| GLM-5.3-Flash | 31,580 | **9,800** | 3.2× |
| MiMo-V2.6-Flash | 150,400 | **33,200** | 4.5× |
| MiMo-V2.6-Pro | 16,300 | **3,100** | 5.3× |
| Muse Spark 1.3 | 226,600 | **46,400** | 4.9× |
| GPT 6 Luna | 21,130 | **5,400** | 3.9× |
| Kimi K3 | 490 | **179** | 2.7× |
| Grok 4.6/4.7 | 845 | **158** | 5.4× |

So yes — for heavy agentic users, take the docs' request counts and divide by **3–7×**.

---

## 3. The definitive capacity table (calibrated to your token profile)

Cost per request uses your averages (7.8k in / 1.1k out+reasoning / 146k cache read) and Go prices (DeepSeek blended at your observed ~40% peak share). "Sessions" assumes 50 requests per typical session. **Bold** = can sustain your current pace.

| Model | $/req | Req/5h | Req/week | Req/month | Sessions/mo | Continuous hours¹ | Sustains your pace? |
|---|---|---|---|---|---|---|---|
| **Space Bunny Free** | $0 | ∞ | ∞ | **∞** | ∞ | ∞ | ✅ (until it ends) |
| **LongCat 2.5 Free** | $0 | ∞ | ∞ | **∞** | ∞ | ∞ | ✅ (until it ends) |
| **Muse Spark 1.3 Contrib** | $0.0013 | 9,288 | 23,220 | **46,440** | 929 | ∞ (>24h) | ✅ (privacy caveat) |
| MiMo-V2.6-Flash | $0.0018 | 6,634 | 16,586 | **33,171** | 663 | ∞ (>24h) | ✅ |
| MiMo-V2.5 (weak) | $0.0018 | 6,634 | 16,586 | 33,171 | 663 | ∞ | ✅ but AA 25 |
| **DeepSeek V4.1 Flash** | $0.0031 | 3,823 | 9,558 | **19,117** | 382 | ~6.1h | ⚠️ monthly cap near day 24 |
| LongCat-2.0 | $0.0045 | 2,646 | 6,614 | 13,228 | 265 | ~4.2h | ❌ |
| GLM-5.3-Flash | $0.0061 | 1,967 | 4,918 | 9,836 | 197 | ~3.1h | ❌ (weekly in ~5 heavy days) |
| DeepSeek V4 Flash | $0.0032 | 1,890 | 4,724 | 9,448 | 189 | ~3.0h | ❌ |
| Hy3 | $0.0068 | 1,754 | 4,386 | 8,772 | 175 | ~2.8h | ❌ |
| Qwen3.8 Flash | $0.0040 | 1,491 | 3,729 | 7,457 | 149 | ~2.4h | ❌ |
| Qwen3.7 Plus (weak) | $0.0107 | 1,119 | 2,799 | 5,597 | 112 | ~1.8h | ❌ |
| GPT 6 Luna | $0.0028 | 1,075 | 2,688 | 5,376 | 108 | ~1.7h | ❌ |
| MiniMax M3 / M2.7 | $0.0124 | 966 | 2,415 | 4,831 | 97 | ~1.5h | ❌ |
| DS V4 Flash Vision | $0.0032 | 945 | 2,362 | 4,724 | 94 | ~1.5h | ❌ (fine for vision-only use) |
| MiMo-V2.6-Pro | $0.0049 | 615 | 1,537 | **3,074** | 61 | ~1.0h | ❌ (escalation model) |
| MiMo-V2.5-Pro | $0.0049 | 615 | 1,537 | 3,074 | 61 | ~1.0h | ❌ |
| GPT 5.6 Luna | $0.0058 | 517 | 1,293 | 2,586 | 52 | ~0.8h | ❌ |
| Hy4 preview | $0.0154 | 390 | 975 | 1,950 | 39 | ~0.6h | ❌ |
| Kimi K2.6 | $0.0352 | 341 | 853 | 1,706 | 34 | ~0.5h | ❌ |
| Kimi K2.7 Code | $0.0395 | 303 | 759 | 1,517 | 30 | ~0.5h | ❌ |
| GLM-5.2 | $0.0537 | 223 | 558 | 1,117 | 22 | ~0.35h | ❌ |
| DeepSeek V4 Pro | $0.0148 | 203 | 508 | 1,017 | 20 | ~0.3h | ❌ |
| GLM-5.3 | $0.0537 | 56 | 140 | **279** | 5.6 | ~5.3 min | ❌ (ration) |
| Qwen3.8 Max | $0.0587 | 51 | 128 | **256** | 5.1 | ~4.9 min | ❌ (ration) |
| **Kimi K3** | $0.0837 | 36 | 90 | **179** | 3.6 | ~3.4 min | ❌ (ration) |
| Grok 4.7 | $0.0952 | 32 | 79 | **158** | 3.2 | ~3.0 min | ❌ (ration) |
| Grok 4.6 | $0.0952 | 32 | 79 | **158** | 3.2 | ~3.0 min | ❌ (ration) |

¹ *Continuous hours at your maximum observed burst rate (630 req/h) before the 5h rolling cap bites. "∞" means even at max burst you can't fill the 5h cap.*

**Read it like this:** at your observed intensity, one heavy agent task ≈ 50–150 requests. So Kimi K3 gives you **1–3 substantial tasks per week** (179 req/month), Grok 4.6 gives **~1–3/week**, Qwen3.8 Max **~2–5/week**, MiMo-V2.6-Pro **~20–60 tasks/month**, GLM-5.3-Flash **~65–190 tasks/month**, and DeepSeek V4.1 Flash **~127–380 tasks/month**.

---

## 4. "How long can I keep programming continuously?"

### On DeepSeek V4.1 Flash (your current model, max effort)

- **5-hour window:** your peak 5h used 1,953 requests ≈ $5.99 = **50% of the $12 cap**. You could roughly **double** your highest observed intensity before throttling. At your max burst rate (630 req/h) you'd need **~6.1 hours** of unbroken maximum-intensity agent work to fill a 5h window — and because it's a rolling window, normal work never gets walled.
- **Daily:** you peaked at 3,146 requests/24h ($8.97). Typical heavy day is 2,500–3,000.
- **Weekly:** the real constraint. Your heaviest 7 days cost **$24.77 of $30 (83%)**. A slightly heavier week will start throttling on Fridays/Saturdays.
- **Monthly:** 16 days cost $39.05 (65% of $60). At the recent ~$5–8/day pace, **the $60 cap lands around day 22–26**.
- **Verdict:** you can program **continuously, all day, at your current pace, for ~3 weeks a month.** Then either slow down, switch models, use off-peak, or add Go Plus / Zen overflow.

### Shift-to-off-peak cheat code (DeepSeek only)

DeepSeek peak = 01:00–04:00 and 06:00–10:00 UTC Mon–Fri. For IST that's ~06:30–09:30 and ~11:30–15:30 local. **Evenings, nights and all weekend are 50% off.** Your logs show a lot of activity in 06:00–10:00 UTC (peak) — shifting those same requests to after ~15:30 IST **roughly doubles** your effective monthly capacity (19.1k → ~30k+ requests).

### On the premium models (Grok 4.6/4.7, Kimi K3, GLM-5.3, Qwen3.8 Max)

At your intensity these are **minutes-per-5h, tasks-per-week** models. Kimi K3: ~3.4 minutes of max-burst work per 5h window (36 requests), ~90 requests/week, ~179/month. **Plan to use them for 1–4 elevated tasks per week**, not as drivers. This matches the community: users who run K3/GLM everywhere burn 73% of their weekly cap in 24 hours.

---

## 5. What Go Plus actually buys

$40/mo. Multipliers vs Go are **2×–8×** depending on the model (not a flat 4×):

| Model | Go | Plus | Multiplier |
|---|---|---|---|
| GLM-5.3 | $15 | $120 | **8×** |
| Kimi K3 | $15 | $60 | 4× |
| Grok 4.6/4.7 | $15 | $60 | 4× |
| Qwen3.8 Max | $15 | $60 | 4× |
| MiMo-V2.6-Pro | $15 | $60 | 4× |
| DeepSeek V4 Pro | $15 | $60 | 4× |
| GPT 6 / 5.6 Luna | $15 | $60 | 4× |
| Kimi K2.6 / LongCat / Hy3 / M2.7 | $60 | $240 | 4× |
| GLM-5.2 / MiniMax M3 / K2.7 / Qwen3.7 | $60 | $180 | 3× |
| **GLM-5.3-Flash** | $60 | $180 | 3× |
| **Qwen3.8 Flash** | $30 | $90 | 3× |
| **DeepSeek V4.1 Flash** | $60 | $120 | **2×** |
| **MiMo-V2.6-Flash / Muse Spark** | $60 | $120 | **2×** |
| Hy4 / DS V4 Flash | $30 | $120 | 4× |

**So:** Go Plus is **great if you live on GLM-5.3 (+8×) or the $15-tier rations (+4×)**, and **poor value if your daily driver is DeepSeek V4.1 Flash, MiMo-V2.6-Flash or Muse Spark (only 2×)**. For a DeepSeek-heavy workflow, **Go + $30 of Zen overflow** gives more total capacity with full flexibility for the same $40. Community verdict on Plus was mixed ("4× price for 3× limits").

---

## 6. Community burn-rate reality check

- *"Hit 73% weekly limit in 24 hours"* — Kimi K3, r/opencode, Aug 30, 2026. Top reply: *"OC go is worthless for the expensive models, only worth it for MiMo, possibly a bit of deepseek."*
- *"You only get $15 total per month [K3]; the 5 hr limit is $12 which is actually $3 in Kimi usage."* — r/opencode, Aug 4, 2026.
- *"I hit the 5 hour usage today — using DS flash for gods sake."* — r/opencode.
- *"It's limited usage for Kimi 3, GLM, and Qwen Max, but for the rest… a billion+ tokens."* — happy light user, r/opencodeCLI.
- Measured light user: 109M tokens ≈ "$19.13" over 3 weeks; *"$10 of quota ≈ 35M GLM-5 tokens or 115M MiniMax M2.7 tokens."*
- Research on agent cost: **~4.17M tokens / ~$1.86 per SWE-bench task** across models (arXiv 2604.22750); Kimi K3's max vs low thinking effort raises cost **3.6–6.5×** (arXiv 2608.25399). Reasoning effort is the single biggest cost lever you control.

Sources: [r/opencode](https://www.reddit.com/r/opencode/comments/1w2muhx/), [r/opencodeCLI](https://www.reddit.com/r/opencodeCLI/comments/1vbkpk6/), [Patshead](https://blog.patshead.com/2026/03/opencode-go-coding-plan-from-a-light-users-perspective.html), [arXiv 2604.22750](https://arxiv.org/pdf/2604.22750), [arXiv 2608.25399](https://arxiv.org/html/2608.25399).

---

## 7. Practical limit-management playbook

1. **Watch the console, not the 5h window.** The weekly and monthly meters are the ones that bind: [opencode.ai/auth](https://opencode.ai/auth) → usage. There are open bugs about monthly meter accuracy — keep a 10% margin.
2. **Route by role** (see `03-task-playbook.md`): high-volume routine work on DeepSeek V4.1 Flash / MiMo-V2.6-Flash; premium models only for planning, hard debugging, design review, and visual verification.
3. **Lower default reasoning effort for bulk work.** Max effort multiplies cost 3.6–6.5×. Use `max` only for planning/hard tasks; `medium`/`low` for routine edits.
4. **Shift DeepSeek work off-peak** (after ~15:30 IST and weekends) for a free 2×.
5. **Keep free models as your floor.** When premium caps run out, Space Bunny / LongCat 2.5 / Zen free models keep you working. Verify their data policies first.
6. **When you need headroom:** options in order of cost — (a) off-peak shift, (b) use a second model's independent allowance (e.g. GLM-5.3-Flash when DS is dry), (c) add Zen balance overflow (~$0.30/$1.20 for V4.1 Flash at Zen rates), (d) Go Plus (best if you use GLM-5.3; worst if you use DeepSeek/MiMo/Muse), (e) frontier models via GitHub Copilot or Zen for the 5% hardest work.
7. **Remember free session-title/small-model calls** also consume tiny amounts on cheap models; nothing to optimize there.

---

**Next:** [05 — Intelligence per Dollar](./05-intelligence-per-dollar.md)
