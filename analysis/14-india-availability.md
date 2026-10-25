# 14 — India Availability: Every Recommended Plan vs Signup, Phone & Payment

> **Snapshot: October 25, 2026.** Scope: the plans recommended in [12](./12-opencode-vs-direct.md) and [13](./13-best-value-coding-plans.md), plus the direct APIs behind the Go roster.
>
> **Definition used here — "works in India" means all four gates pass:**
> 1. you can create an account with an Indian identity (country/region selectable);
> 2. you can pass phone/identity verification **without a US, Chinese or other foreign number**;
> 3. you can pay with an instrument an Indian resident can actually hold (UPI, Indian card, PayPal, etc.);
> 4. the models are actually served to your account from India (no region lock on inference).
>
> 🟢 verified in official docs · 🟡 likely / partly documented / community-confirmed · 🔴 blocked.
>
> **Why this file exists:** a plan can be the best value in the world and still be unusable from India. Alibaba's Token Plan is Singapore-only and its signup requires the phone country to match the selected region; Meta's Muse Code is US-first. Those two are excluded from the rankings, not because of price but because of access.

---

## 0. Bottom line for an Indian buyer

| Rank | Plan | India verdict | Why |
|---|---|---|---|
| **1** | **OpenCode Go — $10/mo** (Plus $40) | 🟢 **Available, cleanest path** | No phone verification; Stripe checkout with **UPI**, card, Link, Alipay, WeChat Pay; **29 models behind one key**; free zero-retention twins as the floor. |
| **2** | **StepFun Step Plan — $6.99–$99** | 🟢 **Available** | Email signup, Stripe/account balance, no phone gate. The published credit conversion makes it the raw-value outlier — **verify consumption in the console before relying on it**. |
| **3** | **Z.ai GLM Coding Plan — $18/$80/$168** | 🟢 **Available** | Bank card or PayPal, no phone gate, OpenCode officially supported. Best value if you specifically want GLM-5.3. |
| **4** | **Xiaomi MiMo Token Plan — $6–$100** | 🟢 **Available via the overseas path** | Overseas email/Google/Facebook registration; **no Chinese phone needed**; Waffo USD checkout (Apple Pay/Google Pay/card). Roughly list-price parity with Go. |
| **5** | **Kimi Code — $19–$199** | 🟢 / 🟡 **Available** | Global USD plans; official OpenCode guide; card payment is the expected path but not spelled out in the English docs. The only plan that puts **K3.1 Pro** behind a flat subscription — quota is opaque. |
| **6** | **MiniMax M Plan — $22/$55/$132** | 🟡 **Available** | Global USD, Stripe, OpenCode supported. Single text model (M3.1 Flash) and **no absolute quota** — you are buying a relative multiplier. |
| — | **Alibaba Token Plan** | 🔴 **Blocked** | Singapore-only; India is not selectable as country/region; the phone country must match the selected region. Use Qwen through Go or OpenRouter instead. |
| — | **Meta Muse Code** | 🔴 **Blocked** | US-first rollout; no India availability announced as of Oct 2026. Muse Spark is still reachable **through Go**, with the Contributor-training caveat. |

**If you buy exactly one thing: OpenCode Go at $10.** It is the only plan where an Indian resident can pay by UPI, get 29 models, and keep working on free models after the caps. Everything else is a specialist add-on.

---

## 1. The full matrix

| Plan / price | Signup from India | Phone / identity | Payment | Models & access | Verdict |
|---|---|---|---|---|---|
| **OpenCode Go** $10/mo · **Plus** $40/mo | 🟢 Email/GitHub; no country gate documented | 🟢 **None** | 🟢 **Card, Link, Alipay, UPI, WeChat Pay** (Stripe); top-ups add **4.6% + $0.31** | 🟢 29 Go models + Zen + free models. **DeepSeek needs Regions = Global**; Muse needs “Allow paid endpoints that train on request data”; Beam regional exclusions **do not include India** | **#1 — buy this first** |
| **Z.ai GLM Coding Plan** Lite $18 · Pro $80 · Max $168 (annual −30%) | 🟢 Email; global | 🟢 None documented | 🟢 **Bank card / PayPal** ([usage policy](https://docs.z.ai/devpack/usage-policy)); UPI not documented | 🟢 GLM-5.3, GLM-5.3-Flash; OpenCode listed as supported; off-peak 50% (peak Mon–Fri 14:00–18:00 SGT) | **#3 — best GLM-only value** |
| **StepFun Step Plan** Mini $6.99 · Plus $9.99 · Pro $29 · Max $99 | 🟢 Email; global platform | 🟢 None documented | 🟢 **Stripe or account balance** | 🟢 Step 5 / Step 3.7 Flash / Step 3.5 Flash; OpenCode-compatible; monthly credits | **#2 — value wildcard; verify credits** |
| **Xiaomi MiMo Token Plan** Lite $6 · Standard $16 · Pro $50 · Max $100 (annual −12%) | 🟢 **Overseas email, Google or Facebook**; no Chinese phone | 🟢 Email is the security identifier; overseas real-name not required | 🟢 **Waffo USD checkout** — Apple Pay, Google Pay, credit/debit cards ([FAQ](https://mimo.mi.com/docs/en-US/quick-start/faq/payment)) | 🟢 MiMo-V2.6 Pro/Flash; OpenCode supported; overseas **Base URL + key are separate** from China | **#4 — cheap MiMo entry; no invoice overseas** |
| **Kimi Code** Plus $19 ($15 annual) · Pro $39 ($31) · Max $99 ($79) · Ultra $199 ($159) | 🟢 Kimi account (email / phone) | 🟡 Indian +91 should work; not explicitly listed | 🟡 Card expected; English docs do not spell out methods | 🟢 K3.1 Pro, K3, K3-256K, K2.8 Preview, K2.7 Code; **official OpenCode guide**; shared quota across tools | **#5 — the K3.1 Pro subscription** |
| **MiniMax M Plan** Go $22 · Explore $55 (3×) · Build $132 (7.5×) | 🟢 Email; global USD | 🟢 None documented | 🟡 **Stripe** (card); UPI not documented | 🟢 M3.1 Flash text only; OpenCode supported; **no absolute quota published** | **#6 — opaque quota** |
| **Alibaba Token Plan** Lite $6 · Essential $10 · Standard $18 · Pro $68 | 🔴 **India not selectable**; Singapore region only | 🔴 Phone country must match the selected region | 🔴 Would need a foreign payment/identity path | 🔴 Qwen models are reachable through **Go** and OpenRouter | **Blocked — do not build on it** |
| **Meta Muse Code** Everyday $5 · High $15 · Power $50 · Maximum $200 | 🔴 **US-first**; no India availability | 🔴 US billing/identity path | 🔴 US payment path | 🔴 Muse Spark is on Go (Contributor SKU) | **Blocked — use Go for Muse** |

### Direct APIs (for completeness)

| Provider / API | India access | Payment | Notes |
|---|---|---|---|
| **DeepSeek API** | 🟢 Global | Card top-up | On Go you must set **Regions = Global** (default allowed regions are Europe & United States). ZDR on Go valid **through Oct 31, 2026**. |
| **xAI API (Grok)** | 🟢 Global endpoint | Card | US regional endpoint costs +10%; global endpoint is the default. |
| **Google Gemini API** | 🟢 **India is on Google’s available-regions list** | Card | Argon is 50% off through Nov 30, 2026, then list price. |
| **Anthropic API** | 🟢 India supported | Card | 30-day retention standard. |
| **OpenAI API** | 🟢 India supported | Card | Your CV client contract bans OpenAI models for that project — access is not the issue, the contract is. |
| **Kimi API** | 🟢 Global | Card 🟡 | Direct API pricing table is JS-rendered; use Go/Kimi Code as the practical route. |
| **Z.ai API** | 🟢 Global | Card / PayPal | Same models as the Coding Plan, pay-as-you-go. |
| **MiniMax API** | 🟢 Global | Card / Stripe | M3.1 Flash list price matches Go. |
| **StepFun API** | 🟢 Global | Stripe / balance | Step 5 list price matches Go. |

---

## 2. The three gates, explained (and why Alibaba/Meta fail)

### Gate 1 — Country/region at signup

Most AI plans let you pick India and proceed. Two do not:

- **Alibaba Cloud Model Studio Token Plan (Personal Edition)** is documented as **Singapore region only** ([overview](https://www.alibabacloud.com/help/en/model-studio/token-plan-personal-overview), updated Oct 21, 2026). Alibaba’s international signup requires the **phone country to match the selected country/region**, and India is not a selectable region for this plan. Community reports of Indian users being unable to complete registration line up with the documented rule. **Do not use a foreign number or a mismatched region** — that risks account closure and refund loss.
- **Meta Muse Code** is US-first. The product page and subscription docs describe regional availability but publish **no India timeline**; third-party coverage through Oct 2026 still lists India as unavailable. Muse Spark is available through OpenCode Go, so you are not locked out of the model — only out of Meta’s own subscription.

### Gate 2 — Phone verification

- **OpenCode Go:** no phone step. Email/GitHub login and Stripe checkout.
- **Z.ai:** email account; no phone gate documented for the Coding Plan.
- **StepFun:** email account on the global platform; no phone gate documented.
- **Xiaomi:** overseas users register with **email, Google or Facebook** — the docs explicitly separate “Mainland Chinese users” (mobile number) from “Overseas users” (email). **A Chinese phone is not required.** This corrects a common assumption.
- **Kimi:** Kimi accounts accept international numbers; Indian +91 is the expected path. 🟡 because Kimi does not publish a country list for Code.
- **MiniMax:** email; no phone gate documented.

### Gate 3 — Payment

| Instrument | Where it works | Notes |
|---|---|---|
| **UPI** | **OpenCode Go/Plus** 🟢 | The single strongest India-specific advantage in this whole comparison. |
| **Indian credit/debit card** | All available plans | Visa/Mastercard are the safe choice; RuPay international acceptance varies. Expect 3-D Secure OTP. |
| **PayPal** | Z.ai 🟢; others 🟡 | Useful fallback when a card’s recurring mandate is declined. |
| **Waffo (USD)** | Xiaomi 🟢 | Apple Pay, Google Pay, credit/debit cards. |
| **Stripe** | OpenCode, StepFun, MiniMax 🟢/🟡 | OpenCode explicitly supports UPI through Stripe; the others document card/Stripe only. |
| **Alipay / WeChat Pay** | OpenCode 🟢 | Listed, but require a Chinese wallet — not a practical India path. Use UPI/card. |

**Practical India caveats (🟡 general, not vendor-specific):**
- Some Indian issuers decline **recurring international USD mandates** even when the first charge succeeds. Keep a second card or use one-time credit top-ups.
- Your card issuer adds an **FX markup** (typically ~2–3.5%); the USD prices here are before that.
- Use your **real Indian billing address**; mismatches are a common cause of gateway declines.
- Prices are list USD, before card FX and any tax the seller adds at checkout.

### Gate 4 — Model access from India

- **OpenCode** serves all Go models through its own gateway (US-hosted). Two models need a setting changed:
  - **DeepSeek V4.1 Flash / V4 Pro:** set **Regions = Global** in the Go model settings. The default allowed regions are **Europe & United States**, so DeepSeek can appear “blocked” until you change it.
  - **Muse Spark 1.3/1.2 Contributor:** enable **“Allow paid endpoints that train on request data.”** Only do this on non-client, non-sensitive work.
  - **Beam Free:** the regional exclusion list (Angola, Belarus, Cambodia, China/HK/Macau, Cuba, DRC, Equatorial Guinea, Iran, Iraq, Laos, Libya, Nigeria, North Korea, Russia, Syria, Turkmenistan, Uzbekistan, Venezuela, Crimea/Donetsk/Luhansk) **does not include India**.
- **Gemini API:** India is explicitly listed in Google’s available regions (updated Oct 22, 2026).
- **xAI:** the global endpoint (`https://api.x.ai`) is the default; no India restriction documented.
- **Alibaba/Qwen:** the models are reachable through Go/OpenRouter even though the Token Plan is not sold to India.

---

## 3. India-first stack (concrete)

### If you want one subscription
**OpenCode Go — $10/mo.** Pay by UPI. Set DeepSeek to Regions=Global. Use:
- `deepseek-v4.1-flash` as the daily driver (25.5k req/mo at your profile),
- `minimax-m3.1-flash` as the cheap quality step-up (4,975 req/mo, AA 43),
- `kimi-k3.1-pro` for the hard 5% (269 req/mo, AA 55.1),
- `gemini-4-argon` for planning on non-client work (728 req/mo, AA 53, now **ZDR/not trained**),
- the free twins `deepseek-v4.1-flash-free` / `glm-5.3-flash-free` when a cap binds.

### If you are GLM-first
**Z.ai GLM Coding Plan Lite — $18/mo.** At the frozen profile that is ~1,319 GLM-5.3 requests/mo at peak (2,639 off-peak) vs Go’s 279 — roughly **4.7× the capacity** for 1.8× the price. Card/PayPal. Keep Go for the non-GLM models.

### If you are MiMo-first and low-volume
**Xiaomi Token Plan Lite — $6/mo.** ~3,173 MiMo-Flash requests/mo or ~1,218 MiMo-Pro requests/mo at the frozen profile. Overseas email + Waffo checkout. At <3k req/mo this is cheaper than Go; above that, Go’s much larger allowance wins. No overseas invoice.

### If you are K3.1 Pro-first
**Kimi Code Plus — $19/mo.** The only flat plan that includes K3.1 Pro, and it officially supports OpenCode. Go’s K3.1 Pro silo is only ~269 heavy requests/mo; Kimi’s quota is opaque but a Plus plan is likely to beat that for K3.1 Pro-heavy work. Keep Go for everything else.

### If you want the raw-value experiment
**StepFun Step Plan Pro — $29/mo.** The published conversion ($1 ≈ 7M credits) implies ~45,000 Step 5 requests/mo at your profile — an order of magnitude beyond anything else. **Verify actual credit consumption in the console on the smallest plan first.** If it holds, it is the best $/heavy-request in this repo; if it does not, it is a footnote.

### Do not buy
- **Alibaba Token Plan** — India is not a supported region; the workaround (foreign number/region mismatch) violates the signup rule.
- **Meta Muse Code** — not available in India; use Muse Spark through Go if you need it.
- **MiniMax M Plan as your only plan** — single text model, opaque quota; fine as a $22 experiment, not as a foundation.

---

## 4. Pre-payment checklist (2 minutes)

1. **Country:** can you select India at signup? If no, stop.
2. **Phone:** is it optional, or does it accept +91? If it must match a foreign region, stop.
3. **Payment:** does checkout show UPI, card or PayPal? Take a screenshot of the final USD amount before confirming.
4. **OpenCode support:** is there an official provider/tool guide (OpenCode, Claude Code, OpenAI-compatible endpoint)? If it is “OpenAI-compatible” only, expect config work.
5. **Quota:** is it an absolute number (requests, credits, dollars) or a relative multiplier (“3×”)? Relative quotas cannot be compared without a test.
6. **Model list:** does the plan include the model you actually want, at the context/effort level you need? (Example: MiniMax M Plan’s Go tier is M3.1 Flash text only.)
7. **Refunds:** Xiaomi Token Plan packages are **non-refundable** once paid; OpenCode credits and subscriptions have their own terms. Read before paying annually.
8. **Data policy:** does the plan train on your data? Contributor SKUs (Muse Spark, and previously Argon) trade data rights for price. Argon on Go is now documented **not used / 0 days** — but re-verify before client/PHI work.
9. **Tax/FX:** add your card’s FX markup and any GST/OIDAR the seller charges before comparing to the USD headline.

---

## 5. What changed vs the Oct 16 advice

| Claim | Oct 16 | Oct 25 (corrected) |
|---|---|---|
| Alibaba Token Plan in India | “Cheap Qwen option” | **Blocked** — Singapore-only, country/phone must match, India not selectable |
| Meta Muse Code in India | “Watch it” | **Blocked** — US-first, no India availability |
| Xiaomi signup | “Needs a Chinese phone” (assumption) | **Wrong** — overseas email/Google/Facebook; Waffo USD checkout |
| Xiaomi vs Go value | “Go is 5–6× better” | **Roughly list-price parity**; Go wins only at high volume because of its $60 allowance for $10 |
| OpenCode payment | “Card” | **UPI explicitly supported** — the decisive India advantage |
| Gemini 4 Argon privacy | “Trains on your data” | **Withdrawn** — Go documents **Not used / 0 days** |
| Kimi Code | “Global USD” | **Confirmed**: Plus $19/$15 annual, Pro $39/$31, Max $99/$79, Ultra $199/$159; official OpenCode guide |

---

## Sources

- OpenCode billing & payment methods: https://opencode.ai/v2/docs/console/billing (Card, Link, Alipay, UPI, WeChat Pay; 4.6% + $0.31 top-up fee)
- OpenCode Go plans, caps, privacy, restricted-model settings: https://opencode.ai/docs/go/
- Z.ai Coding Plan overview & usage policy: https://docs.z.ai/devpack/overview · https://docs.z.ai/devpack/usage-policy
- Z.ai subscription terms: https://docs.z.ai/legal-agreement/subscription-terms
- StepFun Step Plan overview & credit conversion: https://platform.stepfun.ai/docs/en/step-plan/overview
- StepFun pricing (Step 5): https://platform.stepfun.ai/docs/en/guides/pricing/details
- Xiaomi Token Plan: https://mimo.mi.com/docs/en-US/price/token-plan (updated Oct 21, 2026)
- Xiaomi account FAQ (overseas email/Google/Facebook): https://mimo.mi.com/docs/en-US/quick-start/faq/account
- Xiaomi payment FAQ (Waffo USD; Apple/Google Pay; cards): https://mimo.mi.com/docs/en-US/quick-start/faq/payment
- Kimi membership pricing: https://www.kimi.ai/membership/pricing
- Kimi Code models & OpenCode guide: https://www.kimi.com/code/docs/en/kimi-code/models.html
- MiniMax M Plan: https://www.minimax.io/m-plan · https://platform.minimax.io/docs/m-plan/intro
- Alibaba Token Plan (Singapore-only): https://www.alibabacloud.com/help/en/model-studio/token-plan-personal-overview (updated Oct 21, 2026)
- Meta Muse Code: https://dev.meta.ai/products/muse-code · https://dev.meta.ai/docs/muse-code/subscriptions
- Gemini API available regions (India listed): https://ai.google.dev/gemini-api/docs/available-regions
- DeepSeek pricing & peak/off-peak: https://api-docs.deepseek.com/quick_start/pricing
- xAI regional endpoints: https://docs.x.ai/docs/advanced-api-usage/regions

**Confidence:** OpenCode, Z.ai, StepFun, Xiaomi, Alibaba and Meta rows are 🟢/🔴 from official docs. Kimi payment methods and MiniMax payment methods are 🟡 (global USD plans confirmed; card is the expected instrument, not explicitly listed). Indian-issuer recurring-mandate behaviour and FX markup are general market behaviour, not vendor-documented.

---

**Next:** [12 — Go vs Direct](./12-opencode-vs-direct.md) · [13 — Best-Value Coding Plans](./13-best-value-coding-plans.md) · [README](../README.md)
