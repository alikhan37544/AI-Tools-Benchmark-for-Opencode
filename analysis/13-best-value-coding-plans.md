# 13 — Best-Value Coding Plans, Ranked for India (Oct 2026)

> **Snapshot: October 25, 2026.** Ranking is on **verified $ per heavy request at the frozen profile** (7.8k input / 1.1k output+reasoning / 146k cache read), then adjusted for **model quality (AA v4.3.2)**, **quota transparency**, **OpenCode compatibility**, **privacy**, and **India availability**.
>
> **Why “heavy request” and not “tokens per dollar”:** every plan advertises a different unit (dollars, credits, requests, “3× usage”). The only unit that survives contact with an agentic coding session is **requests at your real token profile**. A plan that looks cheap per token but caps you at 200 requests/month is not cheap.
>
> 🟢 verified from official docs · 🟡 proxy/relative · 🔴 excluded.

---

## 0. The ranking

| # | Plan | Price | Headline model (AA) | Heavy req/mo | Plan-effective $/req | AA pts / plan $ | India | Verdict |
|---|---|---|---|---|---|---|---|---|
| **1** | **OpenCode Go** | **$10/mo** | **Kimi K3.1 Pro (55.1)** · Argon (53) · M3.1 Flash (43) · DeepSeek (39) | **269** K3.1 Pro · **728** Argon · **4,975** M3.1 Flash · **25,484** DeepSeek | **$0.0372** K3.1 Pro · **$0.0137** Argon · **$0.0020** M3.1 Flash | 1,482 · 3,858 · 21,393 | 🟢 **UPI** | **Best overall. Buy first.** 29 models, one key, free floor, highest quality ceiling. |
| **2** | **StepFun Step Plan Pro** | **$29/mo** (Plus $9.99, Max $99) | Step 5 (44) | **~45,000** (if credit math holds) | **$0.00064** | **68,273** | 🟢 Stripe | **Raw-value outlier.** If the console confirms it, nothing else is close on $/req — but quality is AA 44, not 55, and the math needs a test. |
| **3** | **Z.ai GLM Coding Plan Lite** | **$18/mo** (Pro $80, Max $168) | GLM-5.3 (45) | **1,319** peak · **2,639** off-peak | **$0.0136** peak · **$0.0068** off-peak | 3,297 · 6,597 | 🟢 Card/PayPal | **Best GLM-only value.** 4.7× Go’s GLM-5.3 capacity for 1.8× the price. |
| **4** | **Xiaomi MiMo Token Plan Lite** | **$6/mo** (Standard $16, Pro $50, Max $100) | MiMo-V2.6-Pro (46) · Flash (38) | **1,218** Pro · **3,173** Flash | **$0.0049** Pro · **$0.0019** Flash | 9,338 · 20,095 | 🟢 Overseas email + Waffo | **Cheap MiMo entry.** Wins below ~3k req/mo; Go wins above. No overseas invoice. |
| **5** | **Kimi Code Plus** | **$19/mo** ($15 annual; Pro $39, Max $99) | **K3.1 Pro (55.1)** | **Opaque** — break-even vs Go is **269** K3.1 Pro req/mo | Unknown | Unknown | 🟢/🟡 Card | **The K3.1 Pro subscription.** Official OpenCode guide; could beat Go for K3.1 Pro-heavy users if the quota is real. |
| **6** | **MiniMax M Plan Go** | **$22/mo** (Explore $55, Build $132) | M3.1 Flash (43) | **Opaque** — 1×/3×/7.5×; break-even vs Go is **~10,945** req/mo | Unknown | Unknown | 🟡 Stripe | **Opaque quota, single text model.** Only if you specifically want a MiniMax-native plan. |
| — | **Alibaba Token Plan** | $6–$68 | Qwen3.8 Max/Flash | — | — | — | 🔴 **Blocked** | Singapore-only; India not selectable. Use Qwen via Go/OpenRouter. |
| — | **Meta Muse Code** | $5–$200 | Muse Spark | — | — | — | 🔴 **Blocked** | US-first; no India availability. Muse Spark via Go. |

**The one-line answer:** **Go is #1 because it is the only plan that combines a 55.1-AA model, 29-model breadth, UPI, and a free floor at $10.** StepFun is the math anomaly; Z.ai is the GLM specialist; Xiaomi is the cheap MiMo entry; Kimi is the K3.1 Pro subscription; MiniMax is the opaque one.

---

## 1. How the math works

For each plan:

```
monthly capacity = plan allowance ÷ heavy-request cost
plan $/req      = plan price ÷ monthly capacity
AA pts / plan $ = AA ÷ plan $/req
```

The **heavy-request cost** comes from the model’s list price at your token profile ([04](./04-limits-and-burn-rate.md)). The **plan allowance** is the published cap (Go), credit balance (Z.ai/Xiaomi/StepFun), or relative multiplier (MiniMax).

This is deliberately harsh: it assumes every request is a heavy agentic one. Light users will get several× more requests per plan, but the **ranking between plans** is stable because the same profile is applied to all of them.

---

## 2. Plan-by-plan

### #1 — OpenCode Go, $10/mo

**Why it wins:** it is not one plan, it is **29 independent allowances**. At your profile:

| Model | AA | Cap | Req/mo | Plan $/req | What it’s for |
|---|---|---|---|---|---|
| Kimi K3.1 Pro | **55.1** | $15 | **269** | $0.0372 | Hardest 5%: architecture, marathon debugging, long-context |
| Gemini 4 Argon | **53** | $30 (50% off) | **728** | $0.0137 | Planning/general intelligence — now **ZDR/not trained** |
| MiniMax M3.1 Flash | 43 | $20 | **4,975** | $0.0020 | Cheap quality workhorse; the new value anchor |
| DeepSeek V4.1 Flash | 39 | $80 | **25,484** | $0.0004 | Daily driver at volume; 8× face value |
| GLM-5.3-Flash | 42 | $60 | **9,836** | $0.0010 | Bulk edits/frontend; 6× |
| MiMo-V2.6-Pro | 46 | $15 | 3,074 | $0.0033 | Privacy-safe reasoning |
| Step 5 | 44 | $15 | 591 | $0.0169 | Paid AA 44 capacity |
| GLM-5.3 | 45 | $15 | 279 | $0.0358 | Standardized terminal/security |
| Qwen3.8 Max | 45 | $15 | 256 | $0.0391 | Visual QA / OSWorld #1 |
| Grok 4.7 | 46 | $15 | 158 | $0.0633 | Deep reasoning, edge cases |

**Strengths:** highest quality ceiling (55.1), unmatched breadth, UPI, free zero-retention twins, Zen overflow, one bill.
**Weaknesses:** allowances are siloed (a $15 K3.1 Pro cap is not transferable); premium caps are small; roster churns weekly; US-hosted gateway.
**Best for:** almost everyone in India who wants one subscription. **Start here.**

### #2 — StepFun Step Plan Pro, $29/mo

**The published math:** StepFun says **$1 ≈ 7M credits** and Step 5 costs **$1.00 / $2.70 / $0.10** per 1M (input / output / cache hit). At your profile that is **$0.02537 per request ≈ 177.8k credits**. Then:

| Tier | Price | Credits | Req/mo | $/req |
|---|---|---|---|---|
| Mini | $6.99 | 400M | ~2,250 | $0.00311 |
| Plus | $9.99 | 1.6B | ~9,000 | $0.00111 |
| **Pro** | **$29** | **8B** | **~45,000** | **$0.00064** |
| Max | $99 | 40B | ~225,000 | $0.00044 |

**Why it is not #1 despite the math:** (a) Step 5 is **AA 44**, a tier below K3.1 Pro/Argon; (b) the credit conversion is documented but **the implied 45k requests/month is 76× Go’s Step 5 allowance** — too good to trust without a console test; (c) it is a single-vendor plan with less model breadth; (d) the plan is new and the credit meter has not been independently audited.
**Best for:** anyone willing to spend $6.99 on the Mini tier to measure actual credit burn before committing to Pro. If the math holds, it is the best raw $/req in this repo.

### #3 — Z.ai GLM Coding Plan Lite, $18/mo

**The math:** Lite gives **2,000 credits/5h + 10,000/week**. GLM-5.3 consumes **32.842 credits per heavy request** (6.9 input / 1.7 cached / 24 output per 10k tokens). Weekly credits × 4.33 = 43,333/month → **1,319 requests/month at peak**; **2,639 off-peak** (50% discount). GLM-5.3-Flash consumes **10.85 credits/req** → **3,994 peak / 7,988 off-peak**.

| Plan | Price | GLM-5.3 peak | GLM-5.3 off-peak | $/req peak | $/req off-peak |
|---|---|---|---|---|---|
| Lite | $18 | 1,319 | 2,639 | $0.0136 | $0.0068 |
| Pro | $80 | 7,911 | 15,822 | $0.0101 | $0.0051 |
| Max | $168 | 18,458 | 36,916 | $0.0091 | $0.0046 |

**Strengths:** 4.7× Go’s GLM-5.3 capacity at Lite; off-peak doubles it; OpenCode supported; card/PayPal.
**Weaknesses:** GLM-only; peak is Mon–Fri 14:00–18:00 SGT (11:30–15:30 IST — exactly the Indian afternoon); credit multipliers are model-specific and can change.
**Best for:** GLM-first users. Keep Go for everything else.

### #4 — Xiaomi MiMo Token Plan Lite, $6/mo

**The math:** Lite = **4.1B credits**. MiMo-V2.6-Flash consumes **1.292M credits per heavy request** → **3,173 req/mo**; MiMo-V2.6-Pro consumes **3.365M** → **1,218 req/mo**. Night (00:00–08:00 Beijing) is **0.8×**.

| Tier | Price | Flash req/mo | Pro req/mo | $/req Flash | $/req Pro |
|---|---|---|---|---|---|
| Lite | $6 | 3,173 | 1,218 | $0.00189 | $0.00493 |
| Standard | $16 | 8,514 | 3,269 | $0.00188 | $0.00489 |
| Pro | $50 | 29,412 | 11,293 | $0.00170 | $0.00443 |
| Max | $100 | 63,467 | 24,368 | $0.00158 | $0.00410 |

**The honest comparison:** Xiaomi’s list prices are essentially at parity with Go’s (Flash ~$0.0018–0.0019/req; Pro ~$0.0049/req). Go’s advantage is the **allowance multiplier** ($60 of Flash for $10, $15 of Pro for $10). So:
- **Below ~3k Flash req/mo:** Xiaomi Lite ($6) is cheaper than Go ($10).
- **Above ~3k Flash req/mo:** Go’s $60 allowance wins.
- **Pro:** Go wins above ~1.2k req/mo.
**Strengths:** cheapest entry ($6), overseas email/Google/Facebook, Waffo USD checkout (Apple/Google Pay/card), OpenCode supported, annual −12%.
**Weaknesses:** MiMo-only; overseas base URL/keys are separate from China; **no overseas invoice**; Token Plan packages are **non-refundable**; no balance/bonus deduction.
**Best for:** low-volume MiMo users and anyone who wants a $6 experiment.

### #5 — Kimi Code Plus, $19/mo

**The math:** Kimi does not publish an absolute request quota. New members lost the weekly quota; a **rolling 5h** and a **monthly total** remain, shared across tools. What is confirmed:
- **Plus $19/mo ($15 annual)** includes **K3.1 Pro** and **K3** (1M context for Pro and above).
- **Pro $39 ($31)** adds **K3.1 Pro Highspeed** (same capability, 2–3× speed, **2× quota usage**).
- **Max $99 ($79)** and **Ultra $199 ($159)** scale further.
- **OpenCode is officially supported** (Kimi Code docs have an OpenCode guide), and you use model IDs like `k3.1-pro`.
- China pricing is separate (¥49/99/199/699/1399).

**The break-even:** Go gives **269** K3.1 Pro heavy requests for $10. Kimi Plus at $19 must give **more than 269** to beat Go on K3.1 Pro $/req; Pro at $39 must give **more than 1,049** to match Go’s $0.0372/req. Those are plausible but **unverified**.
**Strengths:** the only flat plan with K3.1 Pro; official OpenCode support; good for K3.1 Pro-heavy work.
**Weaknesses:** opaque quota; card payment not explicitly documented; no 29-model breadth; shared quota across tools means other Kimi usage eats your coding budget.
**Best for:** K3.1 Pro-first users who will actually use >269 heavy requests/mo.

### #6 — MiniMax M Plan Go, $22/mo

**The math:** Go = **1×**, Explore = **3×**, Build = **7.5×** usage. The only text model is **M3.1 Flash**. No absolute quota is published. Go’s M3.1 Flash allowance is **4,975 req/mo for $10**; MiniMax Go at $22 needs **>10,945 req/mo** to match Go’s $/req. Unknown.
**Strengths:** global USD, Stripe, OpenCode supported; if you also want MiniMax video/image, the plan bundles them.
**Weaknesses:** single text model; opaque quota; no clear advantage over Go for coding.
**Best for:** MiniMax-native users who want video/image too. Not a coding-value pick.

### Excluded — Alibaba Token Plan and Meta Muse Code

- **Alibaba Token Plan:** Lite $6/11,500 credits, Essential $10/25,500, Standard $18/45,000, Pro $68/180,000; night 60%/50% discounts; **Singapore region only**, India not selectable, phone country must match. Credit-per-request is not published. **Cannot rank for India.**
- **Meta Muse Code:** Everyday $5, High $15, Power $50, Maximum $200; Contributor mode default; **US-first, no India availability**. Muse Spark is reachable through Go (Contributor SKU, trains on data). **Cannot rank for India.**

---

## 3. Quality-adjusted view (AA × monthly capacity)

“AA points per plan dollar” rewards cheap low-AA models; “AA × req/mo” rewards volume. Neither is the whole truth, so here is the combined view for the plans with verified math:

| Plan | AA | Req/mo | AA × req/mo | AA pts / plan $ |
|---|---|---|---|---|
| **StepFun Pro $29** | 44 | ~45,000 | **1,980,000** | **68,273** |
| Xiaomi Max $100 (Flash) | 38 | 63,467 | 2,411,746 | 24,113 |
| OpenCode Go — DeepSeek | 39 | 25,484 | 993,876 | 99,490* |
| OpenCode Go — MiMo-Flash | 38 | 33,171 | 1,260,498 | 126,000* |
| OpenCode Go — M3.1 Flash | 43 | 4,975 | 213,925 | 21,393 |
| Xiaomi Lite $6 (Flash) | 38 | 3,173 | 120,574 | 20,095 |
| Z.ai Lite $18 (GLM-5.3 off-peak) | 45 | 2,639 | 118,755 | 6,597 |
| OpenCode Go — Argon | 53 | 728 | 38,584 | 3,858 |
| OpenCode Go — K3.1 Pro | 55.1 | 269 | 14,822 | 1,482 |

\* The “AA pts / plan $” for individual Go models assumes the whole $10 is spent on that model — true only if you use nothing else. It illustrates the multiplier, not a realistic single-model purchase.

**Interpretation:** StepFun Pro is the only plan that combines **high volume and AA 44+** at a price that beats everything on throughput. Go wins on **ceiling** (55.1) and **breadth**, not on raw throughput per dollar. Xiaomi Max is a volume play at AA 38. Z.ai is the quality-per-dollar GLM play.

---

## 4. “Which plan should I buy?” — decision table

| If your month looks like… | Buy | Why |
|---|---|---|
| Mixed coding: DeepSeek daily, some K3.1 Pro/Argon, free bulk | **Go $10** | 29 allowances + UPI + free floor. |
| GLM-5.3 is 70%+ of your work | **Z.ai Lite $18** (+ Go if you need other models) | 4.7× Go’s GLM capacity; off-peak doubles it. |
| You want to test the cheapest possible agentic volume | **StepFun Mini $6.99**, then Pro if credits hold | Measure actual credit burn on Mini first. |
| MiMo only, <3k req/mo | **Xiaomi Lite $6** | Cheaper than Go at low volume. |
| K3.1 Pro only, >269 heavy req/mo | **Kimi Code Plus $19** | Flat plan includes K3.1 Pro; official OpenCode guide. |
| You need video/image too | **MiniMax M Plan** | Bundles other modalities; coding value is opaque. |
| You are in India and want UPI | **Go $10** | The only documented UPI path. |
| You need Opus 5.5/GPT-6 Astra | **Copilot or Zen** | Not on any of these plans. |

---

## 5. Risks and fine print

1. **StepFun’s credit math is the biggest open question.** The $1 ≈ 7M credits conversion is official, but the implied 45k Step 5 requests/month is 76× Go’s allowance. **Test on Mini ($6.99) before paying for Pro.** If the console shows a different credit-per-request rate, the ranking changes.
2. **Opaque quotas cannot be ranked.** Kimi and MiniMax publish relative or rolling limits, not absolute requests. Their positions (#5/#6) reflect **transparency risk**, not necessarily worse value.
3. **Annual prepay amplifies risk.** Z.ai annual is −30%, Xiaomi −12%, Kimi annual saves ~20%. Only prepay annually after a monthly test.
4. **FX and tax.** All prices are USD; Indian cards add ~2–3.5% FX. Some sellers add tax at checkout. OpenCode top-ups add **4.6% + $0.31**.
5. **Roster churn.** Go changed composition twice in October. A plan that is #1 today can lose a model tomorrow; the free floor and multi-model breadth are the hedge.
6. **Privacy is part of value.** Muse Spark Contributor (Go) trains on data; Argon on Go is now **ZDR/not trained**; DeepSeek ZDR expires **Oct 31, 2026**. A cheap plan you cannot use for client work is not cheap.
7. **Do not use foreign-number/region workarounds** for Alibaba or Meta. The account risk outweighs the savings.

---

## 6. India payment summary

| Plan | UPI | Card | PayPal | Wallet | Verdict |
|---|---|---|---|---|---|
| OpenCode Go | ✅ | ✅ | — | Alipay/WeChat (not practical) | **Best India path** |
| StepFun | — | ✅ (Stripe) | — | Balance | Works |
| Z.ai | — | ✅ | ✅ | — | Works |
| Xiaomi | — | ✅ | — | Waffo (Apple/Google Pay) | Works via overseas path |
| Kimi Code | — | 🟡 | — | — | Likely works |
| MiniMax | — | 🟡 (Stripe) | — | — | Likely works |
| Alibaba | — | — | — | — | **Blocked** |
| Meta Muse Code | — | — | — | — | **Blocked** |

---

## Sources

- OpenCode Go: https://opencode.ai/docs/go/ · billing https://opencode.ai/v2/docs/console/billing
- StepFun Step Plan: https://platform.stepfun.ai/docs/en/step-plan/overview · pricing https://platform.stepfun.ai/docs/en/guides/pricing/details
- Z.ai Coding Plan: https://docs.z.ai/devpack/overview · usage policy https://docs.z.ai/devpack/usage-policy
- Xiaomi Token Plan: https://mimo.mi.com/docs/en-US/price/token-plan · payment FAQ https://mimo.mi.com/docs/en-US/quick-start/faq/payment
- Kimi Code: https://www.kimi.com/code/docs/en/kimi-code/models.html · pricing https://www.kimi.ai/membership/pricing
- MiniMax M Plan: https://www.minimax.io/m-plan · https://platform.minimax.io/docs/m-plan/intro
- Alibaba Token Plan: https://www.alibabacloud.com/help/en/model-studio/token-plan-personal-overview
- Meta Muse Code: https://dev.meta.ai/products/muse-code
- AA Intelligence Index v4.3.2: https://artificialanalysis.ai/leaderboards/models

**Confidence:** Go, Z.ai, Xiaomi, StepFun prices/caps are 🟢 from official docs. Kimi/MiniMax quotas are 🟡 (relative/opaque). StepFun’s implied capacity is 🟢 documented conversion × 🟡 unverified consumption. All India verdicts are in [14](./14-india-availability.md).

---

**Next:** [14 — India Availability](./14-india-availability.md) · [12 — Go vs Direct](./12-opencode-vs-direct.md) · [README](../README.md)
