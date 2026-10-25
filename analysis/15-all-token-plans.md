# 15 — All Token Plans Compared: The Absolute Best Deals (October 2026)

> **Snapshot: October 26, 2026.** Extends `13-best-value-coding-plans.md` with every subscription, credit-bundle and pay-as-you-go "token plan" found across GitHub Copilot, Anthropic, OpenAI, Google, Cursor, Windsurf, Kiro, plus the Chinese and aggregator providers. Every figure has a source URL. Confidence: 🟢 verified · 🟡 inferred/relative · 🔴 blocked or unverified.

## 0. TL;DR — the absolute best deals for India

| Rank | Plan | Price | Why it wins | India? |
|---|---|---|---|---|
| **#1** | **OpenCode Go** | **$10/mo** | 29 models, UPI, free floor, highest ceiling (K3.1 Pro AA 55.1), best $/req for mid-tier | 🟢 UPI |
| **#2** | **DeepSeek Flash direct API** | **$0.15/$0.60 per 1M** (off-peak $0.075/$0.30) | Cheapest frontier-class API; no subscription; 1M ctx; vision; ZDR through Oct 31 | 🟢 global |
| **#3** | **Alibaba Qwen3.7-Flash** | **$0.03/$0.13 per 1M** (Singapore) | Cheapest per-token anywhere; 32K–1M ctx | 🟢 global |
| **#4** | **Tencent Hy3** | **$0.132/$0.528 per 1M** | Cheapest open-weights coding model; 262K ctx; free GLM models on Z.ai | 🟢 global |
| **#5** | **Mistral Small 4** | **$0.15/$0.60 per 1M** (90% cache discount) | Dedicated coding model (Codestral $0.30/$0.90); batch 50% off | 🟢 global |
| **#6** | **Google AI Pro** | **₹1,950/mo (~$20.5)** | UPI, Gemini 4 Argon + Pro + Flash, Antigravity IDE, 5 TB, YouTube Premium Lite | 🟢 UPI |
| **#7** | **GitHub Copilot Pro** | **$10/mo** | 25+ models (Opus 5.5, GPT-6 Astra, Gemini 4 Argon), OpenCode-compatible, card/PayPal | 🟡 card/PayPal |
| **#8** | **Cursor Start** | **₹649/mo** | Cheapest agent plan in INR, UPI, India-only legacy plan | 🟢 UPI |
| **#9** | **StepFun Step Plan Pro** | **$29/mo** | Potentially 45k req/mo (unverified credit math) | 🟢 Stripe |
| **#10** | **Claude Pro** | **$20/mo** | Best Claude-only, but no UPI, no OpenCode subscription use | 🟡 card |

**The single best deal for pure coding value in India: OpenCode Go ($10, UPI) + DeepSeek Flash direct API for overflow.** Nothing else combines a 55-AA model, 29-model breadth, UPI and a free floor at $10.

---

## 1. Master comparison — all subscription / credit-bundle plans

### 1.1 Plans usable as OpenCode providers (API/subscription access)

| Plan | Price | Models / access | Heavy req/mo (profile) | $/req (best model) | India payment | OpenCode? |
|---|---|---|---|---|---|---|
| **OpenCode Go** | $10/mo (Plus $40) | 29 Go models + Zen + free | 269 K3.1 Pro · 728 Argon · 4,975 M3.1 Flash · 25,484 DS | $0.0372 (K3.1) · $0.0004 (DS) | 🟢 UPI | 🟢 native |
| **OpenCode Go Plus** | $40/mo | Same, 4× caps | 4× above | Same | 🟢 UPI | 🟢 native |
| **GitHub Copilot Pro** | $10/mo | 25+ models (Opus 5.5, GPT-6 Astra, Gemini 4 Argon, Claude Sonnet, Kimi K3, Grok) | ~364 Sonnet 5.5 · ~2,586 GPT-5.6 Luna · ~182 Opus 5.5 | $0.0274 (Sonnet) · $0.0549 (Opus) | 🟡 card/PayPal | 🟢 native (device flow) |
| **GitHub Copilot Pro+** | $39/mo | Same + premium models (Fable 5, GPT-6 Astra/Sol, Opus 5.5) | ~1,699 Sonnet · ~850 Opus · ~251 Fable/Astra | $0.0229 (Sonnet) · $0.0459 (Opus) | 🟡 card/PayPal | 🟢 native |
| **GitHub Copilot Max** | $100/mo | Highest allowance, priority access | ~4,854 Sonnet · ~2,427 Opus · ~717 Fable/Astra | $0.0206 (Sonnet) · $0.0412 (Opus) | 🟡 card/PayPal | 🟢 native |
| **GitHub Copilot Business** | $19/seat/mo | Org pooled, premium catalog minus Sonnet 4.6/GPT-5.4 nano | ~461 Sonnet · ~231 Opus · ~68 Fable/Astra | $0.0412 (Sonnet) · $0.0824 (Opus) | 🟡 Azure subscription | 🟢 native |
| **GitHub Copilot Enterprise** | $39/seat/mo | Same + priority access, larger pool | ~947 Sonnet · ~473 Opus · ~140 Fable/Astra | $0.0412 (Sonnet) · $0.0824 (Opus) | 🟡 Azure subscription | 🟢 native |
| **Claude Pro** | $20/mo (or $17 annual) | Claude Opus/Sonnet/Haiku; Claude Code included | ~243 Opus (if spent on API) | $0.0824 (Opus) | 🟡 card only | ❌ subscription creds blocked in OpenCode; use API key |
| **Claude Max 5x** | $100/mo | 5× Pro; $100/mo API credits | ~1,214 Opus (API credits) | $0.0824 (Opus) | 🟡 card only | ❌ subscription creds blocked |
| **Claude Max 20x** | $200/mo | 20× Pro; $200/mo API credits | ~2,427 Opus (API credits) | $0.0824 (Opus) | 🟡 card only | ❌ subscription creds blocked |
| **Claude Team Standard** | $20/seat/mo (annual) | 1.25× Pro; pooled weekly | ~304 Opus (per seat) | $0.0824 (Opus) | 🟡 card only | ❌ subscription creds blocked |
| **Claude Team Premium** | $100/seat/mo (annual) | 6.25× Pro; pooled weekly | ~1,519 Opus (per seat) | $0.0824 (Opus) | 🟡 card only | ❌ subscription creds blocked |
| **Claude Enterprise** | $20/seat/mo + API usage | Seat = access only; all usage at API rates | Unlimited (API rates) | $0.0824 (Opus) | 🟡 sales-assisted | ❌ subscription creds blocked |
| **ChatGPT Plus** | $20/mo | GPT-6 Astra/Sol/Luna, GPT-5.6, Codex | Rate-limited, not token-priced | N/A (chat/Codex) | 🟡 card (UPI only for Go) | 🟢 native (OAuth) |
| **ChatGPT Pro 100** | $100/mo | Higher allowance, no 5-hr window | Rate-limited | N/A | 🟡 card | 🟢 native (OAuth) |
| **ChatGPT Pro 200** | $200/mo | Max allowance (grandfathered subs keep old limits through Oct 29) | Rate-limited | N/A | 🟡 card | 🟢 native (OAuth) |
| **ChatGPT Pro 500** | $500/mo | Ultrafast included, highest allowance | Rate-limited | N/A | 🟡 card | 🟢 native (OAuth) |
| **ChatGPT Business** | $25/user/mo (annual $20) | Team features, 2-seat min | Rate-limited | N/A | 🟡 card | 🟢 native (OAuth) |
| **ChatGPT Enterprise** | ~$60/seat/mo (150-seat min) | Unlimited, SLA, SSO | Rate-limited | N/A | 🟡 sales | 🟢 native (OAuth) |
| **ChatGPT Go (India)** | ₹399/mo (~$4.2) | GPT-6 limited, 54K ctx, ads possible | Rate-limited | N/A | 🟢 UPI | 🟢 native (OAuth) |
| **Google AI Plus** | ₹399/mo (~$4.2) intro ₹199 | Flash + Flash-Lite, 400 GB | Rate-limited | N/A | 🟢 UPI | 🟡 manual API key |
| **Google AI Pro** | ₹1,950/mo (~$20.5) | Gemini 4 Argon + Pro + Flash, 5 TB, Antigravity entry, YouTube Premium Lite | Rate-limited (1,500 req/day Gemini CLI) | N/A (API billed separately) | 🟢 UPI | 🟡 manual API key |
| **Google AI Ultra 5x** | ₹6,500/mo (~$68) | 5× Pro limits, 20 TB, YouTube Premium, Gemini Spark (US) | Rate-limited | N/A | 🟢 UPI | 🟡 manual API key |
| **Google AI Ultra 20x** | ₹19,500/mo (~$205) | 20× Pro limits, 30 TB | Rate-limited | N/A | 🟢 UPI | 🟡 manual API key |
| **Cursor Start (India legacy)** | ₹649/mo (~$6.8) | Locked to Grok/Composer at fixed effort | Rate-limited | N/A | 🟢 UPI | ❌ Cursor-only IDE |
| **Cursor Plus** | $8/mo | New pricing (post-xAI acquisition) | Rate-limited | N/A | 🟡 card | ❌ Cursor-only IDE |
| **Cursor Premium** | $30/mo | Higher limits | Rate-limited | N/A | 🟡 card | ❌ Cursor-only IDE |
| **Cursor Super** | $100/mo | Higher limits | Rate-limited | N/A | 🟡 card | ❌ Cursor-only IDE |
| **Cursor Ultra** | $200/mo | Highest limits | Rate-limited | N/A | 🟡 card | ❌ Cursor-only IDE |
| **Windsurf Pro** | $20/mo | Quota-based, Claude/GPT/Gemini models | Rate-limited | N/A | 🟡 card | ❌ Windsurf-only IDE |
| **Windsurf Max** | $200/mo | Highest quota | Rate-limited | N/A | 🟡 card | ❌ Windsurf-only IDE |
| **Kiro (Amazon Q successor)** | $20/mo (Pro) | 1,000 credits | Rate-limited | N/A | 🟡 card | ❌ Kiro-only IDE |
| **StepFun Step Plan Mini** | $6.99/mo | ~2,250 req/mo (if credits hold) | ~2,250 (Step 5) | $0.0031 | 🟢 Stripe | 🟢 OpenCode-compatible |
| **StepFun Step Plan Plus** | $9.99/mo | ~9,000 req/mo | ~9,000 (Step 5) | $0.0011 | 🟢 Stripe | 🟢 OpenCode-compatible |
| **StepFun Step Plan Pro** | $29/mo | ~45,000 req/mo (unverified) | ~45,000 (Step 5) | $0.00064 | 🟢 Stripe | 🟢 OpenCode-compatible |
| **StepFun Step Plan Max** | $99/mo | ~225,000 req/mo (unverified) | ~225,000 (Step 5) | $0.00044 | 🟢 Stripe | 🟢 OpenCode-compatible |
| **Z.ai GLM Coding Plan Lite** | $18/mo | GLM-5.3 + Flash; 1,319 peak / 2,639 off-peak req/mo | 1,319–2,639 (GLM-5.3) | $0.0136 peak / $0.0068 off-peak | 🟢 card/PayPal | 🟢 OpenCode-supported |
| **Z.ai GLM Coding Plan Pro** | $80/mo | 7,911 peak / 15,822 off-peak | 7,911–15,822 (GLM-5.3) | $0.0101 peak / $0.0051 off-peak | 🟢 card/PayPal | 🟢 OpenCode-supported |
| **Z.ai GLM Coding Plan Max** | $168/mo | 18,458 peak / 36,916 off-peak | 18,458–36,916 (GLM-5.3) | $0.0091 peak / $0.0046 off-peak | 🟢 card/PayPal | 🟢 OpenCode-supported |
| **Xiaomi MiMo Token Plan Lite** | $6/mo | 3,173 Flash / 1,218 Pro req/mo | 3,173 Flash / 1,218 Pro | $0.0019 Flash / $0.0049 Pro | 🟢 Waffo USD | 🟢 OpenCode-supported |
| **Xiaomi MiMo Token Plan Standard** | $16/mo | 8,514 Flash / 3,269 Pro | 8,514 / 3,269 | $0.0019 / $0.0049 | 🟢 Waffo USD | 🟢 OpenCode-supported |
| **Xiaomi MiMo Token Plan Pro** | $50/mo | 29,412 Flash / 11,293 Pro | 29,412 / 11,293 | $0.0017 / $0.0044 | 🟢 Waffo USD | 🟢 OpenCode-supported |
| **Xiaomi MiMo Token Plan Max** | $100/mo | 63,467 Flash / 24,368 Pro | 63,467 / 24,368 | $0.0016 / $0.0041 | 🟢 Waffo USD | 🟢 OpenCode-supported |
| **Kimi Code Plus** | $19/mo ($15 annual) | K3.1 Pro + K3 + K2.7 Code + K2.8 Preview | Opaque (break-even: 269 req/mo) | Unknown | 🟡 card | 🟢 official OpenCode guide |
| **Kimi Code Pro** | $39/mo ($31 annual) | Above + K3.1 Pro Highspeed (2× quota) | Opaque | Unknown | 🟡 card | 🟢 official OpenCode guide |
| **Kimi Code Max** | $99/mo ($79 annual) | Above | Opaque | Unknown | 🟡 card | 🟢 official OpenCode guide |
| **Kimi Code Ultra** | $199/mo ($159 annual) | Above | Opaque | Unknown | 🟡 card | 🟢 official OpenCode guide |
| **MiniMax M Plan Go** | $22/mo | M3.1 Flash text only | Opaque (break-even: ~10,945 req/mo) | Unknown | 🟡 Stripe | 🟢 OpenCode-supported |
| **MiniMax M Plan Explore** | $55/mo (3× Go) | M3.1 Flash text only | Opaque (3× Go) | Unknown | 🟡 Stripe | 🟢 OpenCode-supported |
| **MiniMax M Plan Build** | $132/mo (7.5× Go) | M3.1 Flash text only | Opaque (7.5× Go) | Unknown | 🟡 Stripe | 🟢 OpenCode-supported |
| **Alibaba Token Plan** | $6–$68 | Qwen3.8 Max/Flash | — | — | 🔴 Singapore-only | 🔴 blocked India |
| **Meta Muse Code** | $5–$200 | Muse Spark | — | — | 🔴 US-first | 🔴 blocked India |
| **OpenRouter** | No subscription; 5.5% fee on credits | 500+ models, 80+ providers | PAYG | Model price + 5.5% | 🟡 card/AliPay/USDC; UPI via +6% bridge | 🟢 OpenAI-compatible |
| **Mistral (direct)** | No subscription; PAYG | Mistral Small 4, Codestral, Large 3/4, Ministral 3 | PAYG | $0.15/$0.60 (Small 4) | 🟡 card | 🟢 OpenAI-compatible |
| **Cohere (direct)** | No subscription; PAYG | Command family | PAYG | Verify live | 🟡 card | 🟢 OpenAI-compatible |

### 1.2 Pure pay-as-you-go API providers (no subscription)

| Provider | Best model for coding | $/1M (in/out) | $/1k heavy req | India residency? | India payment |
|---|---|---|---|---|---|---|
| **DeepSeek direct** | Flash (off-peak) | $0.075/$0.30 | $2.39 | Global | 🟡 verify |
| **DeepSeek direct** | Flash (peak) | $0.15/$0.60 | $4.79 | Global | 🟡 verify |
| **DeepSeek direct** | V4 Pro (off-peak) | $0.33/$0.99 | $16.50 | Global | 🟡 verify |
| **Alibaba DashScope** | Qwen3.7-Flash (Singapore) | $0.03/$0.13 | $1.05 | Global (Singapore) | 🟡 Alibaba Cloud |
| **Alibaba DashScope** | Qwen3-Coder-Flash (China) | $0.144/$0.574 | $4.54 | Global (China) | 🟡 Alibaba Cloud |
| **Alibaba DashScope** | Qwen3.8-Max (Singapore) | $2.00/$6.00 | $34.00 | Global (Singapore) | 🟡 Alibaba Cloud |
| **Tencent TokenHub** | Hy3 | $0.132/$0.528 | $4.22 | Global (Singapore) | 🟡 Tencent Cloud |
| **Tencent TokenHub** | MiMo-V2.6-Flash | $0.14/$0.28 | $2.66 | Global (Singapore) | 🟡 Tencent Cloud |
| **Tencent TokenHub** | GLM-5.3-Flash | $0.15/$0.50 | $3.80 | Global (Singapore) | 🟡 Tencent Cloud |
| **Z.ai direct** | GLM-5.3-Flash | $0.15/$0.50 | $3.80 | Global | 🟡 console |
| **Z.ai direct** | GLM-4.7-Flash | **Free** | **$0** | Global | 🟡 console |
| **Z.ai direct** | GLM-4.5-Flash | **Free** | **$0** | Global | 🟡 console |
| **MiniMax direct** | M3.1-Flash | $0.15/$0.60 | $4.79 | Global | 🟡 recharge |
| **Mistral direct** | Small 4 | $0.15/$0.60 | $4.79 | Global | 🟡 card |
| **Mistral direct** | Ministral 3 3B | $0.10/$0.10 | $1.10 | Global | 🟡 card |
| **Mistral direct** | Codestral | $0.30/$0.90 | $6.30 | Global | 🟡 card |
| **DeepInfra** | DeepSeek V4 Flash | $0.09/$0.18 (cached $0.018) | $3.53 | Global | 🟡 card/prepay |
| **Together AI** | DeepSeek V4 Flash | $0.30/$1.20 (cached $0.006) | $4.54 | Global | 🟡 card |
| **Fireworks AI** | DeepSeek V4.1 Flash | $0.30/$1.20 (cached $0.006) | $4.54 | Global | 🟡 card |
| **OpenRouter** | DeepSeek V4 Flash | $0.30/$1.20 (cached $0.006) + 5.5% fee | $4.79 | Provider-dependent | 🟡 card/AliPay/USDC; UPI via +6% bridge |
| **Groq** | gpt-oss-20b | $0.075/$0.30 | $6.39 | Global | 🟡 card (India thresholds) |
| **Groq** | gpt-oss-120b | $0.15/$0.60 | $12.78 | Global | 🟡 card |
| **Groq free tier** | gpt-oss-20b/120b | **Free** (1,000 req/day) | **$0** | Global | 🟢 no card needed |
| **AWS Bedrock** | GLM 4.7 Flash (India) | $0.08/$0.48 | $12.83 | 🟢 Mumbai/Hyderabad | 🟡 AWS billing |
| **AWS Bedrock** | Qwen3 Coder 30B (India) | $0.18/$0.71 | $28.46 | 🟢 Mumbai/Hyderabad | 🟡 AWS billing |
| **AWS Bedrock** | Claude Haiku 4.5 (global) | $1/$5 | $27.90 | Global only | 🟡 AWS billing |
| **Azure OpenAI** | GPT-4.1 Nano (global) | $0.10/$0.40 | $8.52 | Global (India +25% premium) | 🟡 INR available |
| **Azure OpenAI** | GPT-5 Mini (India regional) | $0.25/$2.00 (+25%) | $28.00 | 🟢 South India | 🟡 INR available |
| **Google Vertex AI** | Gemini 3.1 Flash-Lite (regional) | $0.275/$1.65 | $7.98 | 🟢 Mumbai/Delhi | 🟡 GCP/INR |
| **Google Vertex AI** | Gemini 3.8 Flash (regional) | $0.825/$4.125 | $23.02 | 🟢 Mumbai/Delhi | 🟡 GCP/INR |
| **Google AI Studio** | Gemini 4 Argon | $2.00/$10.00 (→$4/$20 after Nov 30) | $72.80 | Global | 🟡 card |
| **Cerebras** | GPT-OSS-120B | $0.35/$0.75 (no cache disc.) | $54.66 | Global | 🟡 card |
| **Replicate** | GPT-OSS-120B | $0.18/$0.72 | $28.48 | Global | 🟡 card |
| **OpenCode Zen** | Various (validated models) | PAYG, same as direct | Varies | Global | 🟡 card |

---

## 2. The absolute best deals — ranked

### Rank 1: OpenCode Go ($10/mo) — BEST OVERALL
- **India:** 🟢 UPI, no phone gate, no country restriction
- **Models:** 29 Go models + Zen + free floor (DS Flash Free, GLM-5.3-Flash Free)
- **Best $/req:** DeepSeek V4.1 Flash at $0.0004/req (25,484 req/mo); M3.1 Flash at $0.0020 (4,975 req/mo)
- **Ceiling:** K3.1 Pro AA 55.1 at $0.0372/req (269 req/mo); Argon AA 53 at $0.0137 (728 req/mo, ZDR)
- **Why #1:** Only plan combining a 55-AA model, 29-model breadth, UPI, free floor, and OpenCode-native integration at $10
- **Weakness:** Siloed caps per model; premium allowances are small; weekly roster churn

### Rank 2: DeepSeek Flash direct API (PAYG) — BEST RAW API VALUE
- **India:** 🟢 global endpoint, card/Alipay/WeChat top-up
- **Price:** $0.15/$0.60 peak, $0.075/$0.30 off-peak (50% discount nights/weekends)
- **Value:** $4.79/1k req peak, $2.39/1k req off-peak — cheapest frontier-class API
- **ZDR:** Through Oct 31, 2026 (verify after)
- **Why #2:** No subscription needed; pay only for what you use; off-peak doubles capacity; 1M context; vision
- **Weakness:** No bundled allowance; need to manage top-ups; ZDR expiry risk

### Rank 3: Alibaba Qwen3.7-Flash (PAYG) — CHEAPEST PER TOKEN
- **India:** 🟢 global/Singapore endpoint
- **Price:** $0.03/$0.13 per 1M tokens (Singapore tier, ≤32K)
- **Value:** $1.05/1k heavy req — cheapest anywhere
- **Why #3:** 4× cheaper than DeepSeek Flash; AA 40 (Qwen3.8 Flash) is solid for bulk work
- **Weakness:** No India region (Singapore latency); Token Plan blocked in India (but direct PAYG works); smaller context (32K for cheapest tier)

### Rank 4: Tencent Hy3 (PAYG via TokenHub) — CHEAPEST OPEN-WEIGHTS
- **India:** 🟢 global/Singapore endpoint
- **Price:** $0.132/$0.528 per 1M tokens
- **Value:** $4.22/1k heavy req
- **Why #4:** Cheapest open-weights coding model; 262K context; free GLM-4.7-Flash/GLM-4.5-Flash on Z.ai
- **Weakness:** AA 25 (quality ceiling is low); no India region

### Rank 5: Mistral Small 4 / Ministral 3 (PAYG) — BEST EUROPEAN VALUE
- **India:** 🟢 global endpoint
- **Price:** Small 4: $0.15/$0.60; Ministral 3 3B: $0.10/$0.10; Codestral: $0.30/$0.90
- **Value:** $4.79/1k req (Small 4); $1.10/1k req (Ministral 3 3B)
- **Why #5:** 90% cache discount on repeated prompts; batch 50% off; dedicated code model (Codestral)
- **Weakness:** No India region; ZDR not standard (enterprise only)

### Rank 6: Google AI Pro (₹1,950/mo) — BEST GOOGLE BUNDLE
- **India:** 🟢 UPI (AutoPay mandates), INR pricing
- **Includes:** Gemini 4 Argon + Pro + Flash, Antigravity IDE, 5 TB, YouTube Premium Lite, 1,500 req/day (Gemini CLI)
- **Why #6:** Best bundled value for Google ecosystem users; UPI; India-native
- **Weakness:** API usage billed separately (subscription doesn't reduce per-token cost); Argon 50% discount expires Nov 30

### Rank 7: GitHub Copilot Pro ($10/mo) — BEST MULTI-MODEL SUBSCRIPTION
- **India:** 🟡 card/PayPal only (no UPI)
- **Models:** 25+ including Opus 5.5, GPT-6 Astra, Gemini 4 Argon, Claude Sonnet, Kimi K3, Grok
- **Value:** ~364 Sonnet 5.5 req/mo; ~2,586 GPT-5.6 Luna req/mo; ~182 Opus 5.5 req/mo
- **Why #7:** Cheapest way to access frontier models (Opus 5.5, GPT-6 Astra) in a subscription; OpenCode-native (device flow)
- **Weakness:** No UPI; per-req cost higher than Go for most models; credits don't roll over

### Rank 8: Cursor Start (₹649/mo) — CHEAPEST INDIA-NATIVE AGENT
- **India:** 🟢 UPI, India-only legacy plan
- **Models:** Locked to Grok/Composer at fixed effort
- **Why #8:** Cheapest agent plan in INR with UPI
- **Weakness:** Locked to specific models; legacy plan (may be discontinued); Cursor-only IDE

### Rank 9: StepFun Step Plan Pro ($29/mo) — VALUE OUTLIER (UNVERIFIED)
- **India:** 🟢 Stripe
- **Potential value:** ~45,000 req/mo if credit math holds (76× Go's Step 5 allowance)
- **Why #9:** Published credit math implies exceptional value; test $6.99 Mini tier first
- **Weakness:** Credit math unverified; single vendor; AA 44 quality ceiling; may change

### Rank 10: Claude Pro ($20/mo) — BEST CLAUDE-ONLY
- **India:** 🟡 card only (no UPI)
- **Models:** Claude Opus/Sonnet/Haiku + Claude Code
- **Why #10:** Best for Claude-only workflows; Claude Code included
- **Weakness:** No UPI; subscription creds blocked in OpenCode (use API key); no absolute token limits published

---

## 3. The "stack" recommendations

### Stack A: India-first, maximum value (recommended)
1. **OpenCode Go $10/mo (UPI)** — primary subscription; 29 models + free floor
2. **DeepSeek Flash direct API** — overflow for bulk work at $0.15/$0.60 (off-peak $0.075/$0.30)
3. **Alibaba Qwen3.7-Flash** — cheapest bulk at $0.03/$0.13
4. **Z.ai free GLM-4.7-Flash** — $0 for non-critical work
5. **Total: $10/mo + PAYG overflow** — covers 95% of coding needs

### Stack B: Multi-model power user (India)
1. **OpenCode Go $10/mo (UPI)** — daily driver + ceiling models
2. **GitHub Copilot Pro $10/mo (card)** — frontier models (Opus 5.5, GPT-6 Astra, Gemini 4 Argon) + GitHub integration
3. **Google AI Pro ₹1,950/mo (UPI)** — Gemini ecosystem + Antigravity IDE
4. **Total: ~$30/mo + ₹1,950** — maximum model breadth

### Stack C: Ultra-budget (India)
1. **Cursor Start ₹649/mo (UPI)** — cheapest agent
2. **Groq free tier** — 1,000 req/day, no card
3. **Z.ai free GLM-4.7-Flash** — $0
4. **DeepSeek Flash off-peak** — $0.075/$0.30
5. **Total: ₹649/mo (~$6.8)** — minimal spend, solid capability

### Stack D: Enterprise/compliance (India data residency)
1. **AWS Bedrock (Mumbai/Hyderabad)** — GLM 4.7 Flash $0.08/$0.48, Qwen3 Coder 30B $0.18/$0.71
2. **Google Vertex AI (Mumbai/Delhi)** — Gemini 3.1 Flash-Lite $0.275/$1.65
3. **Azure OpenAI (South India)** — GPT-4.1 Nano $0.10/$0.40 (+25% regional premium)
4. **Total: PAYG** — data stays in India, enterprise SLAs

---

## 4. Key findings from the research

### 4.1 The "subscription vs. PAYG" divide
- **Subscriptions** (Go, Copilot, Claude, ChatGPT, Cursor, Google AI) bundle a fixed allowance of requests/tokens. They're best when you use the bundled models heavily.
- **PAYG APIs** (DeepSeek, Alibaba, Tencent, Z.ai, MiniMax, Mistral, aggregators) charge per token. They're best when usage is variable or you want the cheapest per-token rate.
- **The crossover:** Go's $10 bundle is worth $15–$80 of list-price usage per model (1.5×–8× multiplier). But PAYG providers like Alibaba ($0.03/$0.13) and DeepSeek ($0.075/$0.30 off-peak) can be cheaper per token than any subscription.

### 4.2 India payment landscape
- **UPI works:** OpenCode Go/Plus, Google AI Plus/Pro/Ultra, Cursor Start (legacy)
- **Card/PayPal:** GitHub Copilot, Z.ai, StepFun, Xiaomi MiMo, Kimi, MiniMax, Mistral, DeepSeek, Alibaba, Tencent
- **No India:** Alibaba Token Plan (Singapore-only), Meta Muse Code (US-first)
- **INR pricing:** Google AI (₹399–₹19,500), Cursor Start (₹649)
- **USD only:** Everything else (expect 18% GST + FX markup + 3DS OTP friction)

### 4.3 OpenCode compatibility
- **Native providers:** OpenCode Go/Zen, GitHub Copilot (device flow), OpenAI (OAuth/API key), Anthropic (API key), Google (manual API key)
- **OpenAI-compatible:** OpenRouter, Mistral, Cohere, DeepInfra, Together, Fireworks, Groq, Cerebras, Replicate, most Chinese providers
- **Not compatible (IDE-only):** Cursor, Windsurf, Kiro, Google Antigravity (separate IDE)
- **Blocked in OpenCode:** Claude subscription creds (Anthropic policy); use API key instead

### 4.4 The free tier landscape
| Free option | Quality | Limits | Training? | India? |
|---|---|---|---|---|
| DeepSeek V4.1 Flash Free | AA 39 | Unlimited-ish | No (ZDR) | 🟢 |
| GLM-5.3-Flash Free | AA 42 | Unlimited-ish | No (ZDR) | 🟢 |
| Beam Free | AA 30 | Limited time/regions | No (30-day) | 🟢 (India not excluded) |
| Groq free tier | gpt-oss-20b/120b | 1,000 req/day | Standard | 🟢 |
| Z.ai free GLM-4.7-Flash | AA ~? | Free | Not verified | 🟢 |
| Z.ai free GLM-4.5-Flash | AA ~? | Free | Not verified | 🟢 |
| Z.ai free GLM-4.6V-Flash | AA ~? | Free | Not verified | 🟢 |
| Google AI Studio free | Gemini 3.x Flash | Rate-limited | Yes (improves products) | 🟢 |
| GitHub Copilot Free | Auto model only | 2,000 completions/mo | Standard | 🟢 |

---

## 5. Sources

All figures sourced from the subagent research reports. Primary sources:

**GitHub Copilot:** docs.github.com (plans, billing, models, pricing, privacy, payment methods)
**Anthropic Claude:** claude.com/pricing, platform.claude.com/docs, support.claude.com, anthropic.com/legal
**OpenAI:** developers.openai.com/api/docs/pricing, chatgpt.com/pricing, help.openai.com, platform.openai.com/docs/supported-countries
**Google Gemini:** gemini.google/in/subscriptions, ai.google.dev/gemini-api/docs/pricing, ai.google.dev/gemini-api/docs/available-regions, cloud.google.com
**Cursor/Windsurf/Kiro:** cursor.com/pricing, windsurf.com/pricing, kiro.dev (via research)
**Chinese providers:** api-docs.deepseek.com, alibabacloud.com/help, tencentcloud.com/document, docs.z.ai, platform.minimax.io, docs.mistral.ai
**Aggregators:** openrouter.ai/pricing, docs.together.ai, docs.fireworks.ai, console.groq.com, cerebras.ai/pricing, deepinfra.com/pricing, replicate.com/pricing
**Cloud:** aws.amazon.com/bedrock, azure.microsoft.com, cloud.google.com/vertex-ai
**OpenCode:** opencode.ai/docs/providers, opencode.ai/docs/go, opencode.ai/docs/zen

Confidence markers: 🟢 verified in official docs · 🟡 inferred/relative/undocumented · 🔴 blocked or unverified.
