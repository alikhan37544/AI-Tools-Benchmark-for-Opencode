# 12 — OpenCode Go vs Going Direct: Per-Model Break-Even

> **Snapshot: October 25, 2026.** Every number uses the **frozen heavy-user profile** from [04](./04-limits-and-burn-rate.md): **7.8k input / 1.1k output+reasoning / 146k cache read per request**. Go list prices and direct list prices are compared like-for-like; the only structural difference is Go’s **monthly allowance**.
>
> **The one-sentence answer:** Go’s per-token prices are essentially the **same as going direct** for almost every model. What you are buying with $10 is a **bundle of prepaid allowances worth $15–$80 per model** — a 1.5×–8× face-value multiplier — siloed per model. Go wins when you use **several models** or a **high-multiplier model**; direct or a specialist subscription wins when you need **one model at low volume**, provider features, or a model Go does not carry.
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

If you would use **more than the break-even** of that one model, Go is cheaper. If you would use less, direct is cheaper. But because Go’s $10 also covers 28 other models, the real comparison is usually “Go + maybe one specialist plan” vs “several direct accounts.”

**Example — Kimi K3.1 Pro:** $0.0558/request at your profile → break-even **179 requests/mo**. Go gives **269** requests for $10 (a $15 allowance, 1.5× face value). Direct at 269 requests costs **$15.01**. Go saves $5.01 — real, but not transformative. If you only use 100 K3.1 Pro requests/month, direct costs **$5.58** and Go is overpaying unless you use the other models.

---

## 2. The per-model table

“Go req/mo” is the calibrated capacity from [04](./04-limits-and-burn-rate.md). “Direct $/req” is the direct list price at the same token profile (equal to Go’s list price unless noted). **Bold** = Go’s multiplier is ≥3× (a genuinely good deal).

| Model | Go $/req | Go cap | Go req/mo | Direct $/req | Break-even vs $10 | Go multiplier | Best direct / subscription alternative | India | Verdict |
|---|---|---|---|---|---|---|---|---|---|
| **Kimi K3.1 Pro** | $0.0558 | $15 | **269** | ~$0.0558 🟡 | 179 | 1.5× | **Kimi Code Plus $19** (includes K3.1 Pro, official OpenCode guide; quota opaque) | 🟢 | Go is the cheapest *verified* K3.1 Pro route; Kimi Plus may beat it at high volume |
| Kimi K3 | $0.0837 | $15 | 179 | ~$0.0837 🟡 | 119 | 1.5× | Kimi Code Plus/Pro | 🟢 | Go wins up to 179; Kimi Code for K3-heavy |
| **Gemini 4 Argon** | $0.0412 | $30 | **728** | $0.0412 (50% off thru Nov 30) | 243 | **3.0×** | Gemini API direct (India listed); $4/$20 after Nov 30 | 🟢 | Best hard-task capacity on Go; direct is the fallback if you need no cap |
| **Step 5 Preview** | $0.0254 | $15 | **591** | $0.0254 | 394 | 1.5× | **StepFun Step Plan Pro $29** (~45k req/mo *if* credit math holds) | 🟢 | Go is safe; StepFun is the value outlier to verify |
| **GLM-5.3** | $0.0537 | $15 | **279** | $0.0537 | 186 | 1.5× | **Z.ai Lite $18** (~1,319 req/mo peak, 2,639 off-peak) | 🟢 | **Z.ai wins for GLM-only** — 4.7× Go’s capacity for 1.8× price |
| Qwen3.8 Max | $0.0587 | $15 | 256 | ~$0.0587 | 170 | 1.5× | Alibaba direct is **blocked in India**; OpenRouter | 🟢 (Go) | Go is the practical India route |
| Grok 4.7 | $0.0952 | $15 | 158 | $0.0952 | 105 | 1.5× | xAI direct (global, card) | 🟢 | Go wins up to 158; direct for >158 or provider features |
| **DeepSeek V4.1 Flash** | $0.0031 | $80 | **25,484** | $0.0031 (off-peak) | 3,226 | **8.0×** | DeepSeek direct (card; same off-peak price) | 🟢 | **Go is the best DeepSeek deal on the planet** |
| MiMo-V2.6-Pro | $0.0049 | $15 | 3,074 | ~$0.0049 | 2,041 | 1.5× | Xiaomi Token Plan Lite $6 (~1,218 req/mo) | 🟢 (overseas path) | Go wins above ~1.2k req/mo; Xiaomi Lite below |
| **MiMo-V2.6-Flash** | $0.0018 | $60 | **33,171** | ~$0.0018 | 5,556 | **6.0×** | Xiaomi Token Plan Lite $6 (~3,173 req/mo) | 🟢 | Go wins above ~3.2k req/mo; Xiaomi Lite below |
| **MiniMax M3.1 Flash** | $0.0040 | $20 | **4,975** | $0.0040 | 2,500 | **2.0×** | MiniMax M Plan Go $22 (opaque quota) | 🟡 | Go is the transparent value; MiniMax plan only if it gives >2× capacity |
| **GLM-5.3-Flash** | $0.0061 | $60 | **9,836** | $0.0061 | 1,639 | **6.0×** | Z.ai Lite (GLM-5.3-Flash ~3,994 peak / 7,988 off-peak) | 🟢 | Go wins at high volume; Z.ai for GLM-only |
| Claude Haiku 5.5 | $0.0028 | $15 | 5,375 | ~$0.0028 | 3,571 | 1.5× | Anthropic direct | 🟢 | Go for convenience; direct for rate limits/features |
| GPT 6 Luna | $0.0028 | $15 | 5,376 | ~$0.0028 | 3,571 | 1.5× | OpenAI direct | 🟢 | Go, unless your contract bans OpenAI (then moot) |
| GPT 5.6 Luna | $0.0058 | $15 | 2,586 | ~$0.0058 | 1,724 | 1.5× | OpenAI direct | 🟢 | Go for convenience |
| **Qwen3.8 Flash** | $0.0040 | $30 | 7,457 | ~$0.0040 | 2,500 | **3.0×** | Alibaba direct blocked; OpenRouter | 🟢 (Go) | Go is the India route |
| **Hy3** | $0.0068 | $60 | 8,772 | ~$0.0068 | 1,471 | **6.0×** | Tencent direct (China-centric) | 🟡 | Go is the practical route |
| **LongCat-2.0** | $0.0045 | $60 | 13,228 | ~$0.0045 | 2,222 | **6.0×** | Meituan direct (China-centric) | 🟡 | Go is the practical route |
| **Hy4 preview** | $0.0154 | $30 | 1,950 | ~$0.0154 | 649 | **3.0×** | Tencent direct | 🟡 | Go; unmeasured quality |
| **MiniMax M3** | $0.0124 | $60 | 4,831 | ~$0.0124 | 806 | **6.0×** | MiniMax direct | 🟢 | Go; but M3.1 Flash is better value |
| Kimi K2.7 Code | $0.0395 | $60 | 1,517 | ~$0.0395 | 253 | **6.0×** | Kimi direct | 🟢 | Go; legacy model |
| **Muse Spark Contributor** | $0.0013 | $60 | **46,440** | $0.0013 (Contributor) / $0.0125 (Standard) | 7,692 | **6.0×** | Meta Standard (no training) at ~10× the price | 🔴 (Muse Code) | Go is the only practical route; **trains on data** |

### Reading the multiplier

- **1.5×** (most $15-cap models) — Go is a **modest 50% discount**. Fine for convenience, but not a reason to consolidate everything.
- **2×–3×** (M3.1 Flash, Argon, Qwen Flash, Hy4) — a real discount; worth using Go even if you mostly want that model.
- **6×–8×** (DeepSeek, MiMo-Flash, GLM-Flash, Hy3, LongCat, M3, K2.7, Muse) — **Go is the deal**. These are the models that make the $10 plan feel absurdly cheap.
- **The multiplier is not transferable.** A $15 K3.1 Pro allowance cannot be spent on DeepSeek. This is why “29 models” matters: you are buying 29 separate small allowances, not one $300 pot.

---

## 3. When direct (or a specialist plan) wins

| Situation | Better choice | Why |
|---|---|---|
| You use **one model, below its break-even** | Direct API | You pay only for what you use; Go’s $10 is a floor. |
| You want **GLM-5.3 only** | **Z.ai Lite $18** | ~1,319 req/mo peak (2,639 off-peak) vs Go’s 279 — 4.7× capacity for 1.8× price. |
| You want **Step 5 only** | **StepFun Step Plan Pro $29** (after verifying credits) | Published conversion implies ~45k req/mo; Go gives 591. |
| You want **K3.1 Pro only** | **Kimi Code Plus $19** | Flat plan includes K3.1 Pro; Go’s silo is only 269 heavy req/mo. Quota opaque. |
| You want **MiMo only, low volume** | **Xiaomi Token Plan Lite $6** | ~3,173 Flash / ~1,218 Pro req/mo; cheaper than Go at <3k req/mo. |
| You want **MiniMax only** | MiniMax M Plan Go $22 | Only if it gives >2× Go’s M3.1 Flash capacity (opaque — test). |
| You need **provider features** | Direct | Batch API, fine-tuning, prompt-caching controls, dedicated rate limits, data residency, ZDR contracts, invoices, custom base URLs. |
| You need a **model Go doesn’t carry** | Direct / Copilot / Zen | Claude Opus 5.5, GPT-6 Astra, Fable 5.1, Muse Wonder. |
| You need **compliance isolation** | Direct | A direct contract with the provider may be easier to audit than a gateway’s sub-processor chain. |
| You are **India-only and want UPI** | **Go** | No direct provider in this list documents UPI. |

---

## 4. When Go wins

1. **You use two or more models.** The $10 is amortized across independent allowances; even 1.5× models add up.
2. **You use a 6×–8× model** — DeepSeek V4.1 Flash (8×), MiMo-Flash / GLM-Flash / Hy3 / LongCat / M3 / K2.7 / Muse (6×). This is where Go is genuinely unbeatable.
3. **You want one key, one bill, one payment method.** UPI is the India-specific killer feature.
4. **You want a free floor.** The Zen free twins (`deepseek-v4.1-flash-free`, `glm-5.3-flash-free`) keep working after caps; direct APIs do not have an equivalent.
5. **You do not want to manage 8 provider accounts, API keys and billing relationships.**
6. **You value the privacy table.** Go documents retention/training per model in one place; direct providers each have their own policy page and change them independently.

---

## 5. Privacy & features: Go gateway vs direct

| Dimension | OpenCode Go | Direct |
|---|---|---|
| **Data policy** | One table per model. Most: **0-day retention, not trained**. Grok/GPT/Haiku/Beam: **30-day, not trained**. Muse Spark 1.3/1.2 Contributor: **trained**. DeepSeek ZDR valid **through Oct 31, 2026**. Argon: **0-day / not trained** (corrected Oct 25). | Provider-specific. Google Argon **Standard** does not train; **Contributor** does. Meta Standard does not train; Contributor does. Z.ai/DeepSeek/MiniMax/Kimi each have their own terms. Anthropic/OpenAI standard 30-day. |
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
Do you use more than one model, or any 6×–8× model?
 ├─ Yes → OpenCode Go $10. Add a specialist plan only if one model dominates.
 └─ No  → Which single model?
      ├─ GLM-5.3        → Z.ai Lite $18 (peak) / off-peak if you can shift
      ├─ Step 5         → StepFun Step Plan Pro $29 (verify credits first)
      ├─ K3.1 Pro       → Kimi Code Plus $19 (or Go if you also want 28 others)
      ├─ MiMo (low vol) → Xiaomi Lite $6
      ├─ MiniMax        → Go $10 (transparent) or M Plan $22 (opaque)
      ├─ DeepSeek       → Go $10 (8× — direct cannot compete)
      └─ Argon/Grok/GPT → Go $10 (Argon 3×; Grok/GPT 1.5×)
```

**The India overlay:** Go is the only option with **UPI**. Everything else needs an Indian card, PayPal or Waffo. If payment friction is the deciding factor, Go wins before the math starts.

---

## Sources

- Go roster, prices, caps, privacy: https://opencode.ai/docs/go/
- Go billing/payment methods: https://opencode.ai/v2/docs/console/billing
- Z.ai Coding Plan: https://docs.z.ai/devpack/overview · https://docs.z.ai/devpack/usage-policy
- StepFun Step Plan: https://platform.stepfun.ai/docs/en/step-plan/overview · pricing https://platform.stepfun.ai/docs/en/guides/pricing/details
- Xiaomi Token Plan: https://mimo.mi.com/docs/en-US/price/token-plan
- Kimi Code: https://www.kimi.com/code/docs/en/kimi-code/models.html · https://www.kimi.ai/membership/pricing
- MiniMax M Plan: https://www.minimax.io/m-plan
- DeepSeek pricing: https://api-docs.deepseek.com/quick_start/pricing
- Gemini API regions: https://ai.google.dev/gemini-api/docs/available-regions
- xAI regions: https://docs.x.ai/docs/advanced-api-usage/regions

**Confidence:** caps and list prices are 🟢 from the live docs (Oct 25). Direct prices for Kimi K3.1 Pro/K3 are 🟡 (JS-rendered table; Go list used as proxy). MiniMax M Plan quotas are 🟡 (relative only). StepFun credit conversion is 🟢 documented but the implied capacity is **unverified in the console**.

---

**Next:** [13 — Best-Value Coding Plans](./13-best-value-coding-plans.md) · [14 — India Availability](./14-india-availability.md) · [README](../README.md)
