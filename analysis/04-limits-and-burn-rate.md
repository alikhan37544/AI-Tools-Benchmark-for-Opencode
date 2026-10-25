# 04 — Limits, Requests & Realistic Continuous Programming

> **Snapshot: October 1, 2026; refreshed October 13, 16 and 25, 2026.** Usage history remains **Sep 15–Oct 1** (from the primary machine’s v1 DB). Caps and prices re-verified live **Oct 25**: **Kimi K3.1 Pro added ($15 cap)**, **MiniMax M3.1 Flash added ($20 cap)**, **Step 5 Preview back to $15** (4× promo ended), **Gemini 4 Argon renamed/50%-off at $30** (not a Contributor SKU; ZDR), **Space Bunny and LongCat 2.5 Preview Free removed**. No session content or client data is used — only aggregate token counts.
>
> 🆕 **Oct 25 — the new stuff:** **K3.1 Pro gives ~269 heavy requests/month** (5h: 54, week: 134) — the smallest premium ration on Go, but at AA 55.1. **M3.1 Flash gives ~4,975/month** (5h: 995, week: 2,488) at AA 43 — the new value workhorse. **Argon gives ~728/month** at the 50%-off $30 cap. **Step 5 is back to ~591/month** at $15. The fresh v2 DB (Oct 25) confirms the frozen profile within ~5%.

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

**The key insight:** you barely dent the **5-hour** window (peak 37% of the $16 cap) and the weekly peak sits at **62%** of the $40 cap. At your current pace (~$5–8/day recently) you project to **$45–73/month — under the $80 cap in normal months, binding only in crunch months**.

---

## 2. Why the docs’ “estimated requests” look so much higher than your reality

OpenCode’s estimates assume a light request: ~410 input, ~71k cached, ~310 output tokens. You run **7.8k input, 146k cached, 1.1k output+reasoning** — roughly **5–7× heavier per request**. The multiplier:

### The pricing table multiplier update (Oct 25)

| Model | Docs est. req/month | **Your calibrated req/month** | Ratio |
|---|---|---|---|
| DeepSeek V4.1 Flash | 173,330 | **25,484** | 6.8× |
| GLM-5.3-Flash | 31,580 | **9,836** | 3.2× |
| MiMo-V2.6-Flash | 150,400 | **33,171** | 4.5× |
| MiMo-V2.6-Pro | 16,300 | **3,074** | 5.3× |
| Muse Spark 1.3 | 226,600 | **46,440** | 4.9× |
| GPT 6 Luna | 21,130 | **5,376** | 3.9× |
| Claude Haiku 5.5 | 19,230 | **5,375** | 3.6× |
| **Gemini 4 Argon** | 2,120 | **728** | 2.9× |
| **Kimi K3.1 Pro** | 735 | **269** | 2.7× |
| **MiniMax M3.1 Flash** | 19,380 | **4,975** | 3.9× |
| **Step 5 Preview** | 2,130 | **591** | 3.6× |
| Kimi K3 | 490 | **179** | 2.7× |
| Grok 4.7 | 845 | **158** | 5.3× |
| MiniMax M3 | 16,000 | **4,831** | 3.3× |
| LongCat-2.0 | 57,200 | **13,228** | 4.3× |

So yes — for heavy agentic users, take the docs’ request counts and divide by **3–7×**.

---

## 3. The definitive capacity table (calibrated to your token profile)

Cost per request uses your averages (7.8k in / 1.1k out+reasoning / 146k cache read) and Go prices (DeepSeek blended at your observed ~40% peak share). “Sessions” assumes 50 requests per typical session. **Bold** = can sustain your current pace.

| Model | $/req | Req/5h | Req/week | Req/month | Sessions/mo | Continuous hours¹ | Sustains your pace? |
|---|---|---|---|---|---|---|---|
| **GLM-5.3-Flash Free** | $0 | ∞ | ∞ | **∞** | ∞ | ∞ | ✅ (zero-retention) |
| **DeepSeek V4.1 Flash Free** | $0 | ∞ | ∞ | **∞** | ∞ | ∞ | ✅ (zero-retention) |
| Beam Free | $0 | ∞ | ∞ | **∞** | ∞ | ∞ | ✅ (no training, 30-day) |
| **Muse Spark 1.3 Contrib** | $0.0013 | 9,288 | 23,220 | **46,440** | 929 | ∞ (>24h) | ✅ (trains on data) |
| MiMo-V2.6-Flash | $0.0018 | 6,634 | 16,586 | **33,171** | 663 | ∞ (>24h) | ✅ |
| **DeepSeek V4.1 Flash** | $0.0031 | 5,097 | 12,742 | **25,484** | 510 | ~8.1h | ✅ ($80 cap) |
| LongCat-2.0 | $0.0045 | 2,646 | 6,614 | 13,228 | 265 | ~4.2h | ❌ |
| GLM-5.3-Flash | $0.0061 | 1,967 | 4,918 | 9,836 | 197 | ~3.1h | ❌ (weekly in ~5 heavy days) |
| Hy3 | $0.0068 | 1,754 | 4,386 | 8,772 | 175 | ~2.8h | ❌ |
| Qwen3.8 Flash | $0.0040 | 1,491 | 3,729 | 7,457 | 149 | ~2.4h | ❌ |
| **MiniMax M3.1 Flash** | **$0.0040** | **995** | **2,488** | **4,975** | **99.5** | **~1.6h** | ❌ (best paid value) |
| MiniMax M3 | $0.0124 | 966 | 2,415 | 4,831 | 97 | ~1.5h | ❌ |
| Claude Haiku 5.5² | $0.0028 | 1,075 | 2,688 | 5,375 | 108 | ~1.7h | ❌ (subagent use is fine) |
| GPT 6 Luna | $0.0028 | 1,075 | 2,688 | 5,376 | 108 | ~1.7h | ❌ |
| **MiMo-V2.6-Pro** | $0.0049 | 615 | 1,537 | **3,074** | 61 | ~1.0h | ❌ (escalation model) |
| GPT 5.6 Luna | $0.0058 | 517 | 1,293 | 2,586 | 52 | ~0.8h | ❌ |
| Hy4 preview | $0.0154 | 390 | 975 | 1,950 | 39 | ~0.6h | ❌ |
| Kimi K2.7 Code | $0.0395 | 303 | 759 | 1,517 | 30 | ~0.5h | ❌ |
| **Gemini 4 Argon** | **$0.0412** | **146** | **364** | **728** | **14.6** | **~14 min** | ❌ (best hard-task capacity) |
| **Step 5 Preview** | **$0.0254** | **118** | **296** | **591** | **11.8** | **~11 min** | ❌ (AA 44 capacity) |
| GLM-5.3 | $0.0537 | 56 | 140 | **279** | 5.6 | ~5.3 min | ❌ (ration) |
| **Kimi K3.1 Pro** | **$0.0558** | **54** | **134** | **269** | **5.4** | **~5.1 min** | ❌ (AA 55.1 ration) |
| Qwen3.8 Max | $0.0587 | 51 | 128 | **256** | 5.1 | ~4.9 min | ❌ (ration) |
| Kimi K3 | $0.0837 | 36 | 90 | **179** | 3.6 | ~3.4 min | ❌ (ration) |
| Grok 4.7 | $0.0952 | 32 | 79 | **158** | 3.2 | ~3.0 min | ❌ (ration) |

¹ *Continuous hours at your maximum observed burst rate (630 req/h) before the 5h rolling cap bites. “∞” means even at max burst you can’t fill the 5h cap.*

² **Haiku 100K-tier footnote:** the 5,375 req/mo figure assumes a prompt of **≤100K tokens**. The frozen profile (7.8k input + 146k cache read) is above that boundary, so Haiku is billed at the **>100K tier** — $0.50 input / $2.50 output / $0.05 cache read per 1M. The same heavy request then costs **~$0.014** and the $15 cap buys **~1,075 req/mo** (5h ~215, week ~538). Keep Haiku on explore/subagent contexts under 100K; above that, DeepSeek V4.1 Flash or MiMo-V2.6-Flash is cheaper and stronger.

**Read it like this:** at your observed intensity, one heavy agent task ≈ 50–150 requests. So:
- **Kimi K3.1 Pro** gives you **~2–5 substantial tasks/month** (269 req/mo) — the smallest premium ration, but the highest AA on Go.
- **Argon** gives **~5–15 heavy tasks/month** (728).
- **Step 5** gives **~4–12 tasks/month** (591).
- **M3.1 Flash** gives **~33–100 tasks/month** (4,975) — the best paid value.
- **GLM-5.3** gives **~2–6 tasks/month** (279).
- **DeepSeek V4.1 Flash** gives **~170–510 tasks/month** (25,484).
- The **free twins are effectively unlimited** (AA 42/39, zero-retention).

---

## 4. “How long can I keep programming continuously?”

### On DeepSeek V4.1 Flash (your current model, max effort)

- **5-hour window:** your peak 5h used 1,953 requests ≈ $5.99 = **37% of the $16 cap**. You could roughly **triple** your highest observed intensity before throttling. At your max burst rate (630 req/h) you’d need **~8 hours** of unbroken maximum-intensity agent work to fill a 5h window — and because it’s a rolling window, normal work never gets walled.
- **Daily:** you peaked at 3,146 requests/24h ($8.97). Typical heavy day is 2,500–3,000.
- **Weekly:** your heaviest 7 days cost **$24.77 of $40 (62%)**. A crunch week can still throttle by the weekend, but normal weeks clear it.
- **Monthly:** 16 days cost $39.05 (49% of $80). At the recent ~$5–8/day pace you land at **$45–73/month — under the cap in normal months, binding only in crunch months**.
- **Verdict:** you can program **continuously, all day, at your current pace, effectively all month.** Keep the weekly meter in view during crunch weeks; otherwise use off-peak, a second model’s allowance, or Zen overflow.

### Shift-to-off-peak cheat code (DeepSeek only)

DeepSeek peak = 01:00–04:00 and 06:00–10:00 UTC Mon–Fri. For IST that’s ~06:30–09:30 and ~11:30–15:30 local. **Evenings, nights and all weekend are 50% off.** Your logs show a lot of activity in 06:00–10:00 UTC (peak) — shifting those same requests to after ~15:30 IST **roughly doubles** your effective monthly capacity (25.5k → ~40k+ requests).

### On the premium models (K3.1 Pro, Argon, Step 5, M3.1 Flash)

At your intensity these are **minutes-to-hours-per-5h, tasks-per-week** models:
- **Kimi K3.1 Pro:** **~5.1 minutes** of max-burst work per 5h window (54 requests), 134/week, **269/month**.
- **Gemini 4 Argon:** **~14 minutes** per 5h (146), 364/week, **728/month** — 2.7× K3.1 Pro’s capacity at AA 53.
- **Step 5:** **~11 minutes** per 5h (118), 296/week, **591/month**.
- **MiniMax M3.1 Flash:** **~1.6 hours** per 5h (995), 2,488/week, **4,975/month** — the only premium-tier model with real daily capacity.

**Plan to use the $15–$30 rations for 1–4 elevated tasks per week**, not as drivers. This matches the community: users who run K3/GLM everywhere burn 73% of their weekly cap in 24 hours.

---

## 5. What Go Plus actually buys

$40/mo. Multipliers vs Go are **2×–8×** depending on the model (not a flat 4×):

| Model | Go | Plus | Multiplier |
|---|---|---|---|
| GLM-5.3 | $15 | $120 | **8×** |
| Kimi K3.1 Pro | $15 | $60 | 4× |
| Kimi K3 | $15 | $60 | 4× |
| Grok 4.7 | $15 | $60 | 4× |
| Qwen3.8 Max | $15 | $60 | 4× |
| MiMo-V2.6-Pro | $15 | $60 | 4× |
| **Gemini 4 Argon** | $30 | $120 | **4×** |
| **MiniMax M3.1 Flash** | $20 | $80 | **4×** |
| GPT 6 / 5.6 Luna | $15 | $60 | 4× |
| Claude Haiku 5.5 | $15 | $60 | 4× |
| Step 5 Preview | $15 | $60 | 4× |
| LongCat / Hy3 | $60 | $240 | 4× |
| GLM-5.2 / MiniMax M3 / K2.7 / Qwen3.7 | $60 | $180 | 3× |
| **GLM-5.3-Flash** | $60 | $180 | 3× |
| **Qwen3.8 Flash** | $30 | $90 | 3× |
| **DeepSeek V4.1 Flash** | $80 | $160 | **2×** |
| **MiMo-V2.6-Flash / Muse Spark** | $60 | $120 | **2×** |
| Free models (DS/GLM free, Beam) | Free | Free | — |

**So:** Go Plus is **great if you live on GLM-5.3 (+8×) or the $15-tier rations (+4×)** — and it also quadruples Argon’s cap to $120 and M3.1 Flash to $80. It is **poor value if your daily driver is DeepSeek V4.1 Flash, MiMo-V2.6-Flash or Muse Spark (only 2×)**. For a DeepSeek-heavy workflow, **Go + $30 of Zen overflow** gives more total capacity with full flexibility for the same $40. Community verdict on Plus was mixed (“4× price for 3× limits”).

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

1. **Watch the console, not the 5h window.** The weekly and monthly meters are the ones that bind: [opencode.ai/auth](https://opencode.ai/auth) → usage. There are open bugs about monthly meter accuracy — keep a 10% margin.
2. **Route by role** (see `03-task-playbook.md`): high-volume routine work on DeepSeek V4.1 Flash / M3.1 Flash / MiMo-V2.6-Flash / the free twins; premium models only for planning, hard debugging, design review, and visual verification.
3. **Lower default reasoning effort for bulk work.** Max effort multiplies cost 3.6–6.5×. Use `max` only for planning/hard tasks; `medium`/`low` for routine edits.
4. **Shift DeepSeek work off-peak** (after ~15:30 IST and weekends) for a free 2×.
5. **Keep free models as your floor.** When premium caps run out, **GLM-5.3-Flash Free (AA 42) and DeepSeek V4.1 Flash Free (AA 39)** — both zero-retention — plus Beam Free keep you working. **Flint 40B Free may train** — non-sensitive only.
6. **Use M3.1 Flash as the paid value lane.** At 4,975 req/mo and $0.0020/req plan-effective, it is the cheapest way to get AA 43 on Go.
7. **When you need headroom:** options in order of cost — (a) off-peak shift, (b) the free twins (real capability, $0), (c) use a second model’s independent allowance (e.g. M3.1 Flash or GLM-5.3-Flash when DS is dry), (d) add Zen balance overflow (DeepSeek at Zen rates; Argon 50% off through Nov 30), (e) Go Plus (best if you use GLM-5.3 or Argon; worst if you use DeepSeek/MiMo/Muse), (f) frontier models via GitHub Copilot or Zen for the 5% hardest work.
8. **Remember free session-title/small-model calls** also consume tiny amounts on cheap models; nothing to optimize there.

---

**Next:** [05 — Intelligence per Dollar](./05-intelligence-per-dollar.md)
