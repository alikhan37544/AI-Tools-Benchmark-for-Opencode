# 12 — OpenCode Go vs Going Direct: Per-Model Break-Even

> **Snapshot: October 25, 2026; re-based November 17, 2026 (AA v5.0.1 era).** Every number now uses the **measured fleet profile** from provider-side logs (both Go accounts, all machines, **24,160 requests over 30 days**): **3.5k input / 768 output+reasoning / 166k cache read per request**. The old **frozen heavy profile** (7.8k in / 1.1k out / 146k cache) is kept as the secondary, conservative **"heavy mix"** where cross-plan comparisons need it (specialist-plan credit math in [13](./13-best-value-coding-plans.md) is heavy-mix based). Go list prices and direct list prices are compared like-for-like; the only structural difference is Go’s **monthly allowance**.
>
> **The one-sentence answer:** Go’s per-token prices are essentially the **same as going direct** for almost every model. What you are buying with $10 is **one shared allowance with per-model normalization** — each model’s $15–$100 limit is the plan’s coverage **if you use only that model** (a 1.5×–10× **solo-usage** multiplier vs the $10 price), and mixing models draws from the same pool proportionally (the pools are **not** additive). Go wins when your usage concentrates on a **high-multiplier lane**; direct or a specialist subscription wins when you need **one model at low volume**, provider features, or a model Go does not carry.
>
> 🟢 verified from official pricing/docs · 🟡 proxy or partly documented · 🔴 vendor-only.

---

## 1. The core math

For a single model, going direct costs:

```
direct $/month = requests × $/request
```

Go costs **$10/month** and gives you `cap ÷ $/request` requests. So the **single-model break-even** is:

```
break-even requests = $10 ÷ $/request
Go headroom        = cap ÷ $10        (the face-value multiplier)
```

If you would use **more than the break-even** of that one model, Go is cheaper. If you would use less, direct is cheaper. But because Go’s $10 also covers 31 other models (one shared allowance, normalized per model), the real comparison is usually “Go + maybe one specialist plan” vs “several direct accounts.”

**Example — Kimi K3.1 Pro:** $0.05783/request at the measured profile → break-even **173 requests/mo**. Go gives **259** requests for $10 (a $15 allowance, 1.5× face value). Direct at 259 requests costs **$14.98**. Go saves $4.98 — real, but not transformative. If you only use 100 K3.1 Pro requests/month, direct costs **$5.78** and Go is overpaying unless you use the other models.

---

## 2. The per-model table

“Go req/mo” is the calibrated capacity at the **measured fleet profile** (heavy-mix capacity — the conservative secondary — is in [04](./04-limits-and-burn-rate.md)). “Direct $/req” is the direct list price at the same token profile (equal to Go’s list price unless noted). **Bold** = Go’s multiplier is ≥3× (a genuinely good deal). Break-even = $10 ÷ $/req. Rows marked *unmeasured AA* have no v5.0.1 score (capacity math is pure price arithmetic).

| Model | Go $/req | Go cap | Go req/mo (measured) | Direct $/req | Break-even vs $10 | Go multiplier | Best direct / subscription alternative | India | Verdict |
|---|---|---|---|---|---|---|---|---|---|
| **Kimi K3.1 Pro** | $0.05783 | $15 | **259** | ~$0.05783 🟡 | 173 | 1.5× | **Kimi Code Plus $19** (includes K3.1 Pro, official OpenCode guide; quota opaque) | 🟢 | Go is the cheapest *verified* K3.1 Pro route; Kimi Plus may beat it at high volume |
| Kimi K3 | $0.08674 | $15 | 173 | ~$0.08674 🟡 | 115 | 1.5× | Kimi Code Plus/Pro | 🟢 | Go wins past 115; Kimi Code for K3-heavy |
| **Gemini 4 Argon** | $0.03123 | $30 | **961** | $0.03123 (50% off thru Nov 30) | 320 | **3.0×** | Gemini API direct (India listed); $4/$20 after Nov 30 | 🟢 | Best hard-task capacity on Go (AA 50 = the Go ceiling); direct is the fallback if you need no cap |
| **Step 5 Preview** | $0.02215 | $15 | **677** | $0.02215 | 451 | 1.5× | **StepFun Step Plan Pro $29** (~45k heavy req/mo *if* credit math holds) | 🟢 | Go is safe; StepFun is the value outlier to verify |
| **GLM-5.3** | $0.05140 | $15 | **292** | $0.05140 | 195 | 1.5× | **Z.ai Lite $18** (~1,319 heavy req/mo peak, 2,639 off-peak) | 🟢 | **Z.ai wins for GLM-only** — ~4.7× Go's heavy-mix capacity (279) for 1.8× price |
| Qwen3.8 Max | $0.06556 | $15 | 229 | ~$0.06556 | 153 | 1.5× | Alibaba direct is **blocked in India**; OpenRouter | 🟢 (Go) | Go is the practical India route |
| Qwen4 Max | $0.03049 | $15 | 492 | ~$0.03049 | 328 | 1.5× | Alibaba direct blocked in India; OpenRouter | 🟢 (Go) | AA 43 (v5.0.1) at a $15 ration; Go is the India route |
| Grok 4.7 | $0.09455 | $15 | 159 | $0.09455 | 106 | 1.5× | xAI direct (global, card) | 🟢 | Go wins past 106; direct for higher volume or provider features |
| **DeepSeek V4.1 Flash** | $0.00190 | $100 | **52,632** | $0.00190 (off-peak base + measured 28% peak blend) | 5,263 | **10.0×** | DeepSeek direct (card; same prices) | 🟢 | **Go is the best DeepSeek deal on the planet** |
| MiMo-V2.6-Pro | $0.00278 | $15 | 5,391 | ~$0.00278 | 3,594 | 1.5× | Xiaomi Token Plan Lite $6 (~1,218 heavy req/mo) | 🟢 (overseas path) | Go wins above ~1.2k req/mo; Xiaomi Lite below |
| **MiMo-V2.6-Flash** | $0.00117 | $60 | **51,433** | ~$0.00117 | 8,572 | **6.0×** | Xiaomi Token Plan Lite $6 (~3,173 heavy req/mo) | 🟢 | Go wins above ~3.2k req/mo; Xiaomi Lite below |
| **MiniMax M3.1 Flash** | $0.00347 | $20 | **5,760** | $0.00347 | 2,880 | **2.0×** | MiniMax M Plan Go $22 (opaque quota) | 🟡 | Go is the transparent value; MiniMax plan only if it gives >2× capacity |
| **GLM-5.3-Flash** | $0.00588 | $60 | **10,196** | $0.00588 | 1,699 | **6.0×** | Z.ai Lite (GLM-5.3-Flash ~3,994 peak / 7,988 off-peak, heavy mix) | 🟢 | Go wins at high volume; Z.ai for GLM-only |
| Claude Haiku 5.5 (>100K) | $0.01508 | $15 | 995 | ~$0.01508 | 663 | 1.5× | Anthropic direct | 🟢 | Go for convenience; direct for rate limits/features |
| Claude Haiku 5.5 (≤100K) | $0.00302 | $15 | 4,973 | ~$0.00302 | 3,315 | 1.5× | Anthropic direct | 🟢 | The subagent-context option — but the measured mix (170k prompt) always bills >100K |
| GPT 6 Luna | $0.00302 | $15 | 4,973 | ~$0.00302 | 3,315 | 1.5× | OpenAI direct | 🟢 | Go, unless your contract bans OpenAI (then moot) |
| GPT 5.6 Luna | $0.00619 | $15 | 2,425 | ~$0.00619 | 1,616 | 1.5× | OpenAI direct | 🟢 | Go for convenience |
| **Qwen3.8 Flash** | $0.00454 | $30 | 6,611 | ~$0.00454 | 2,204 | **3.0×** | Alibaba direct blocked; OpenRouter | 🟢 (Go) | Go is the India route |
| **Hy4 (GA)** | $0.01179 | $60 | **5,088** | ~$0.01179 | 848 | **6.0×** | Tencent direct | 🟡 | Go is the practical route; AA 35 on v5.0.1 |
| **Hy4 preview** (separate SKU) | $0.01179 | $30 | **2,544** | ~$0.01179 | 848 | **3.0×** | Tencent direct | 🟡 | Same price as GA but half the cap; unmeasured on AA |
| **Hy3** *(unmeasured AA)* | $0.00674 | $60 | 8,900 | ~$0.00674 | 1,484 | **6.0×** | Tencent direct (China-centric) | 🟡 | Go is the practical route |
| **LongCat-2.0** *(unmeasured AA)* | $0.00296 | $60 | 20,266 | ~$0.00296 | 3,378 | **6.0×** | Meituan direct (China-centric) | 🟡 | Go is the practical route |
| **MiniMax M3** | $0.01192 | $60 | 5,032 | ~$0.01192 | 839 | **6.0×** | MiniMax direct | 🟢 | Go; but M3.1 Flash is better value (M3 prices double >512K) |
| Kimi K2.7 Code *(unmeasured AA)* | $0.03791 | $60 | 1,583 | ~$0.03791 | 264 | **6.0×** | Kimi direct | 🟢 | Go; legacy model |
| DeepSeek V4 Pro (legacy) | $0.00747 (off-peak; peak = 2×) | $15 | 2,009 | ~$0.00747 | 1,339 | 1.5× | DeepSeek direct | 🟢 | Legacy; V4.1 Flash dominates it on value |
| **Muse Spark Contributor** | $0.00083 | $60 | **72,007** | $0.00083 (Contributor) / ~$0.0363 (Standard, heavy mix) | 12,001 | **6.0×** | Meta Standard (no training) at ~28× the Contributor price (per heavy request) | 🔴 (Muse Code) | Go is the only practical route; **trains on data** |

*Off-table (unmeasured AA, same math): Qwen3.7 Plus $0.01176/req → 5,103 req/mo (break-even 850) · GLM-5.2 $0.05140 → 1,167/mo (195) · Muse Spark 1.2 Contributor = Muse 1.3 prices.*

### Reading the multiplier

- **1.5×** (most $15-cap models) — Go is a **modest 50% discount**. Fine for convenience, but not a reason to consolidate everything.
- **2×–3×** (M3.1 Flash 2×; Argon, Qwen3.8 Flash, Hy4 preview 3×) — a real discount; worth using Go even if you mostly want that model.
- **6×–10×** (DeepSeek **10×** at $100/$10; MiMo-Flash / GLM-Flash / Hy4 GA / Hy3 / LongCat / M3 / K2.7 / Muse 6×) — **Go is the deal**. These are the models that make the $10 plan feel absurdly cheap.
- **The multiplier is a solo-usage ratio, not a stack of pools.** The paid models **share one allowance** with per-model normalization: a $15 K3.1 Pro limit and a $100 DeepSeek limit each show what the plan covers **at that model alone**, and usage on either draws from the same pool in proportion to that model's limit. So the capacity figures below are **solo-usage coverage** (the docs-endorsed reading) — don't add the per-model pools together. **Go Teams ($20/member/mo, 2-member minimum — $40/mo) adds +$5 to every model cap** (DeepSeek $100 → $105, $15 rations → $20), a small uniform bump to every multiplier.

---

## 3. When direct (or a specialist plan) wins

| Situation | Better choice | Why |
|---|---|---|
| You use **one model, below its break-even** | Direct API | You pay only for what you use; Go’s $10 is a floor. |
| You want **GLM-5.3 only** | **Z.ai Lite $18** | ~1,319 heavy req/mo peak (2,639 off-peak) vs Go’s 292 measured (279 heavy) — ~4.7× capacity for 1.8× price. |
| You want **Step 5 only** | **StepFun Step Plan Pro $29** (after verifying credits) | Published conversion implies ~45k heavy req/mo; Go gives 677 measured (591 heavy). |
| You want **K3.1 Pro only** | **Kimi Code Plus $19** | Flat plan includes K3.1 Pro; Go's solo-usage coverage is only 259 measured req/mo (269 heavy). Quota opaque. |
| You want **MiMo only, low volume** | **Xiaomi Token Plan Lite $6** | ~3,173 Flash / ~1,218 Pro heavy req/mo; cheaper than Go at <3k req/mo. |
| You want **MiniMax only** | MiniMax M Plan Go $22 | Only if it gives >2× Go’s M3.1 Flash capacity (5,760 measured; opaque — test). |
| You need **provider features** | Direct | Batch API, fine-tuning, prompt-caching controls, dedicated rate limits, data residency, ZDR contracts, invoices, custom base URLs. |
| You need a **model Go doesn’t carry** | Direct / Copilot / Zen | Claude Opus 5.5, GPT-6 Astra, Fable 5.1, Muse Wonder. |
| You need **compliance isolation** | Direct | A direct contract with the provider may be easier to audit than a gateway’s sub-processor chain. |
| You are **India-only and want UPI** | **Go** | No direct provider in this list documents UPI. |

---

## 4. When Go wins

1. **Your usage lands on models above their break-even** — the $10 is one shared allowance (normalized per model limit; per-model figures are solo-usage coverage), so what matters is how much of your usage sits on lanes where the multiplier beats direct; even 1.5× models add up.
2. **You use a 6×–10× model** — DeepSeek V4.1 Flash (**10×**), MiMo-Flash / GLM-Flash / Hy4 GA / Hy3 / LongCat / M3 / K2.7 / Muse (6×). This is where Go is genuinely unbeatable.
3. **You want one key, one bill, one payment method.** UPI is the India-specific killer feature.
4. **You want a free floor.** The Zen free twins (`deepseek-v4.1-flash-free`, `glm-5.3-flash-free`) keep working after caps; direct APIs do not have an equivalent.
5. **You do not want to manage 8 provider accounts, API keys and billing relationships.**
6. **You value the privacy table.** Go documents retention/training per model in one place; direct providers each have their own policy page and change them independently.

---

## 5. Privacy & features: Go gateway vs direct

| Dimension | OpenCode Go | Direct |
|---|---|---|
| **Data policy** | One table per model. Most: **0-day retention, not trained**. Grok/GPT/Haiku/Beam: **30-day, not trained**. Muse Spark 1.3/1.2 Contributor: **trained**. DeepSeek ZDR valid **through Nov 30, 2026** (renewed monthly — re-verify). Argon: **0-day / not trained** (corrected Oct 25). | Provider-specific. Google Argon **Standard** does not train; **Contributor** does. Meta Standard does not train; Contributor does. Z.ai/DeepSeek/MiniMax/Kimi each have their own terms. Anthropic/OpenAI standard 30-day. |
| **Hosting** | OpenCode hosts in the **US**. | Provider regions; some offer EU/US/Asia endpoints (xAI US endpoint +10%). |
| **Rate limits** | Per-model monthly dollar caps; 5h/weekly/monthly sub-limits. | Provider RPM/TPM; usually much higher for paid tiers. |
| **Features** | Chat/completions through OpenCode; vision where the model supports it; tools; no batch/fine-tune. | Batch, fine-tuning, prompt caching controls, structured output, dedicated capacity, SDKs. |
| **Billing** | $10/$40 flat + optional Zen overflow; UPI/card/PayPal? (card, Link, Alipay, UPI, WeChat Pay). | Per-token, card; some accept PayPal. |
| **Failure mode** | Cap binds → switch model or Extra Usage. | Bill grows; rate limit → retry/upgrade tier. |
| **Model churn** | Roster changes weekly; a model can disappear. | Provider deprecations, usually with notice. |

**Do not assume Go’s privacy terms carry over to direct** (or vice versa). If you switch a PHI-adjacent workflow from `opencode-go/gemini-4-argon` to the Gemini API, you are now under Google’s Standard terms, not OpenCode’s table. Re-verify.

---

## 6. The decision in one page

```
Do you use more than one model, or any 6×–10× model?
 ├─ Yes → OpenCode Go $10. Add a specialist plan only if one model dominates.
 └─ No  → Which single model?
      ├─ GLM-5.3        → Z.ai Lite $18 (peak) / off-peak if you can shift
      ├─ Step 5         → StepFun Step Plan Pro $29 (verify credits first)
      ├─ K3.1 Pro       → Kimi Code Plus $19 (or Go if you also want 31 others)
      ├─ MiMo (low vol) → Xiaomi Lite $6
      ├─ MiniMax        → Go $10 (transparent) or M Plan $22 (opaque)
      ├─ DeepSeek       → Go $10 (10× — direct cannot compete)
      └─ Argon/Grok/GPT → Go $10 (Argon 3×; Grok/GPT 1.5×)
```

**The India overlay:** Go is the only option with **UPI**. Everything else needs an Indian card, PayPal or Waffo. If payment friction is the deciding factor, Go wins before the math starts.

---

## Sources

- Go roster, prices, caps, privacy: https://opencode.ai/docs/go/ · *(pricing/estimate tables moved to Console: console/go#pricing, console/go#limits — docs defer to Console as of Nov 17; values unchanged)*
- Go billing/payment methods: https://opencode.ai/v2/docs/console/billing
- Z.ai Coding Plan: https://docs.z.ai/devpack/overview · https://docs.z.ai/devpack/usage-policy
- StepFun Step Plan: https://platform.stepfun.ai/docs/en/step-plan/overview · pricing https://platform.stepfun.ai/docs/en/guides/pricing/details
- Xiaomi Token Plan: https://mimo.mi.com/docs/en-US/price/token-plan
- Kimi Code: https://www.kimi.com/code/docs/en/kimi-code/models.html · https://www.kimi.ai/membership/pricing
- MiniMax M Plan: https://www.minimax.io/m-plan
- DeepSeek pricing: https://api-docs.deepseek.com/quick_start/pricing
- Gemini API regions: https://ai.google.dev/gemini-api/docs/available-regions
- xAI regions: https://docs.x.ai/docs/advanced-api-usage/regions

**Confidence:** caps and list prices are 🟢 from the live docs (Nov 17 re-verify; per-token prices unchanged). Capacity/break-even figures are 🟢 arithmetic at the measured fleet profile (provider-side logs) with the heavy mix as the conservative secondary. Direct prices for Kimi K3.1 Pro/K3 are 🟡 (JS-rendered table; Go list used as proxy). MiniMax M Plan quotas are 🟡 (relative only). StepFun credit conversion is 🟢 documented but the implied capacity is **unverified in the console**.

---

**Next:** [13 — Best-Value Coding Plans](./13-best-value-coding-plans.md) · [14 — India Availability](./14-india-availability.md) · [README](../README.md)
