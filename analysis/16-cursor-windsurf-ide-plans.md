# AI Coding IDE/Tool Plans — Research Report (late October 2026)

**Audience:** Solo developer in India, optimizing for *real token value* (not IDE features).
**Date of research:** ~Oct 26, 2026 (prices verified against official pages where reachable).
**Confidence key:** 🟢 high (official page) · 🟡 medium (reputable third-party, may lag) · 🔴 low/unverified.

> **Big 2026 shift you must know:** Cursor was acquired by SpaceX/xAI (~$60B, closing Q3 2026) and is now sold as **"The X Subscription"** (Grok + Cursor + X combined). Windsurf/Codeium was acquired by Cognition and is rebranded as **Devin Desktop**. Amazon Q Developer is being sunset in favor of **Kiro**. Continue.dev was acquired by Cursor. Sourcegraph Cody is enterprise-only. Tabnine discontinued its free/individual tier and is enterprise-only.

---

## 1. Cursor

### 1.1 Current plan structure (post X-Subscription unification)

Cursor now has **two parallel product lines**. New customers start on The X Subscription; legacy subscribers keep their plans.

**The X Subscription (new customers, USD, excludes tax):**

| Plan | Price | Included usage | Third-party models (Claude/GPT/Gemini) |
|---|---|---|---|
| Free | $0 | Limited | Not available |
| Plus | $8/mo ($80/yr) | Base (weekly pool) | Not available |
| Premium | $30/mo ($300/yr) | 4× Plus | API list price, from prepaid credit |
| Super | $100/mo ($1,000/yr) | 15× Plus | API list price, from prepaid credit |
| Ultra | $200/mo ($2,000/yr) | 50× Plus | API list price, from prepaid credit |
| Teams | $30 / $100 / $200 per seat/mo | Matches seat tier | API list price + Cursor Token Rate |
| Enterprise | Custom | Pooled | API list price + Cursor Token Rate |

🟢 Source: cursor.com/docs/models-and-pricing (Oct 2026).

**Legacy Cursor plans (still available to existing subscribers, USD):**

| Plan | Price | Comparable X plan |
|---|---|---|
| Hobby | Free | Free |
| Start (India only) | ₹649/mo, tax-inclusive | Plus |
| Pro | $20/mo | Premium |
| Pro+ | $60/mo | Super |
| Ultra | $200/mo | Ultra |
| Teams Standard | $40/user/mo | Teams Premium seat |
| Teams Premium | $120/user/mo | Teams Super seat |

🟢 Source: cursor.com/help/account-and-billing/pricing.

### 1.2 Model access & mechanics
- **Cursor models (included in pool):** Grok 4.7, 4.6, 4.5, Composer 2.5. Grok 4.7/4.6/4.5 at $2/$6 per 1M (input/output); Composer 2.5 at $0.5/$2.5 per 1M. Fast mode = 2× pricing. Long context (>256k) = 2×.
- **Third-party models (Premium+ only, billed at API list price from prepaid credit):** Claude 4.6/4.7/5/5.5 Opus & Sonnet, Claude Haiku 5.5, GPT-5/5.4/5.5/5.6 series, Gemini 3.x/4.x, GLM, Kimi K3, Muse Spark, etc. 🟢
- **Plus plan is locked down:** fixed medium effort, Fast off, 256k context, Grok+Composer only. **No Auto, no Cloud Agents, no Automations, no Bugbot, no Origin, no third-party models, no BYOK.** 🟢
- **Premium+ adds:** Cloud Agents, Automations, Origin code hosting, Bugbot, third-party models, Grok Bot.
- **Auto mode** (Cost/Balance/Intelligence) routes among Cursor + third-party models; on Teams/Enterprise, Balance/Intelligence routes bill at the routed model's list price + $0.25/M Cursor Token Rate. Individual plans have Cost mode only. 🟢
- **Weekly pool** (not monthly) — refreshes weekly so one heavy day doesn't eat the month. 🟢
- **Cursor Token Rate:** $0.25/M tokens on top of model pricing for eligible third-party requests on Teams/Enterprise (input+output+cached). Excluded for small/cheap models (Haiku 5.5, Flash variants, GPT-5 mini/nano/luna, etc.). 🟢

### 1.3 "Unlimited" caveats & overage
- Auto mode on **legacy** paid plans is "unlimited" but only when you let Cursor pick (Cursor models). Manually selecting premium models burns the credit pool. 🟡
- On X Subscription, Plus has a **fixed weekly pool**; overage requires prepaid credit top-ups or plan upgrade. No quality downgrade — requests just pause or you pay. 🟢
- **Monthly additional usage limit** caps overage spend regardless of credit balance. 🟢
- Legacy plans: two monthly pools (Cursor Models + Other Models) + on-demand usage billed in arrears. 🟢

### 1.4 India availability (Cursor)
- **Cursor Start (legacy, India-only):** ₹649/mo, tax-inclusive, UPI or Indian card (3DS required). Verifies Indian phone number. Models: Grok 4.7/4.6/4.5 + Composer 2.5 only (fixed medium effort, non-fast). Includes Cloud Agents, Agent/Plan/Ask modes, plugins, MCP, hooks, skills. **No** Bugbot, SDK, Automations, third-party models, on-demand spend. Pool is monthly; Grok 4.5 consumes ~3× faster than Composer 2.5. 🟢 Source: cursor.com/help/account-and-billing/cursor-start.
- **Cursor Start is now "legacy"** — new customers in India choose The X Subscription (Plus/Premium/…). Can only be purchased while account is on free plan; once you switch to any paid plan you can't go back to Start. 🟢
- **X Subscription in India:** priced in USD ($8/$30/$100/$200). Payment via cards, Apple Pay, Google Pay, Link (per docs.x.ai/x-subscription/payment-methods). **No UPI** for X Subscription. Indian cards work but may face 3DS/bank declines. GST (18%) applies on top (prices exclude tax). 🟡 (payment methods from official docs; UPI absence inferred).
- **India is Cursor's 3rd-largest market** (>3M users, tripled in a year). 🟡 Source: Times of India.
- **Student deal** (1 year free Pro for .edu) **closed to new signups June 25, 2026.** 🟡

### 1.5 OpenCode compatibility
- Cursor is a VS Code fork; OpenCode is a terminal TUI agent. They are **complementary** — run OpenCode in Cursor's integrated terminal. OpenCode can also use Cursor? No — OpenCode does not consume Cursor subscription; it uses BYOK or OpenCode Go/Zen. 🟢
- Cursor's BYOK provider list does **not** include Ollama/LM Studio local models; OpenCode does. 🟢

---

## 2. Windsurf (Codeium → now Devin Desktop, by Cognition)

### 2.1 Plan structure (Oct 2026)
Pricing now lives at devin.ai/pricing. Windsurf is rebranded "Devin Desktop."

| Plan | Price | Quota | Best for |
|---|---|---|---|
| Free | $0 | Light daily+weekly quota | Trying out |
| Pro | $20/mo | Standard daily+weekly | Solo devs |
| Max | $200/mo | Significantly higher | Power users |
| Teams | $80/mo team fee + $40/mo per full dev seat | Per-user | Teams (≤200 users) |
| Enterprise | Custom | Custom | Large orgs |

- Annual billing: ~17% savings (Pro ~$16.6/mo). 🟡
- Tab autocomplete + inline edits = **unlimited on all plans** (including Free). 🟢
- Student discount: 50%+ off Pro with .edu email (~$7-8/mo). 🟡 (terms not specifying exact %).

🟢 Source: devin.ai/pricing, nocode.mba (Oct 2 2026).

### 2.2 Model access & credits
- **All premium models** on Pro+: OpenAI, Claude, Gemini, xAI, plus leading open-source. 🟢
- **SWE-2** (Windsurf's proprietary model) free use on paid plans. SWE-1.7 (earlier) was the free model; now SWE-2. 🟡
- **Cascade** agent + **Fast Context** (deep codebase understanding). Cloud sessions for background dev on paid plans. 🟢
- Quota measured in "units"; 1 unit per Cascade prompt (regardless of internal steps). Premium models may cost 2×+. ~50-70 prompts/day on Pro. 🟡
- **Extra usage:** paid plans can purchase at API pricing; free users wait for reset. Auto-refill available with budget cap. 🟢
- No fixed monthly prompt-credit count; daily+weekly refresh. 🟢

### 2.3 India availability (Windsurf/Devin)
- No India-specific plan or UPI mentioned. Standard USD pricing via Stripe (likely). 🟡 (inferred from absence of India page; confidence medium).
- Student discount requires .edu email — Indian university emails (.ac.in) may not qualify for the .edu-based program. 🔴 (unverified).
- Devin Desktop available on macOS/Windows/Linux. 🟢

---

## 3. Other notable tools

### 3.1 Cline (open source, VS Code/JetBrains/Cursor/Windsurf extension + CLI + desktop)
- **Price:** Free (Apache 2.0). You pay model API costs directly (BYOK). 🟢
- **Model access:** Every major provider — Claude, GPT, Gemini, OpenRouter (200+ models), AWS Bedrock, Azure, GCP Vertex, Ollama/LM Studio local. No markup. 🟢
- **India:** No subscription; works wherever VS Code/JetBrains does. Pay API providers directly. Local models (Ollama) = $0. 🟢
- **OpenCode compatibility:** Cline runs inside VS Code/Cursor/Windsurf as extension; OpenCode is terminal. Fully complementary. Cline also supports MCP. 🟢

### 3.2 Continue (acquired by Cursor)
- **Status:** Continue was acquired by Cursor (2026). Open-source codebase remains available. 🟢 Source: continue.dev.
- **Price:** Was free + BYOK / configurable. Post-acquisition, the company/product direction is now Cursor's. 🟡
- **India:** N/A (no standalone paid plan anymore). 🟡

### 3.3 Aider (open source terminal pair programmer)
- **Price:** Free (open source). Pay model API costs only. 🟢
- **Model access:** Any provider via API (OpenAI, Anthropic, Gemini, DeepSeek, Groq, Ollama, OpenRouter, GitHub Copilot). 🟢
- **India:** Works globally; local models = $0. 🟢
- **OpenCode compatibility:** Both terminal tools; can run side-by-side (different sessions). 🟢

### 3.4 Amazon Q Developer → Kiro (AWS)
- **Status:** New Q Developer signups blocked May 15, 2026; full EOL April 30, 2027. Replacement is **Kiro**. 🟢
- **Q Developer (legacy):** Free tier 50 agentic requests/mo; Pro $19/user/mo (1,000 agentic requests, 4,000 LOC Java transform, IP indemnity). 🟢
- **Kiro pricing:** Free $0 (50 credits + Claude Sonnet 4.5 + open-weight models); Pro $20 (1,000 credits); Pro+ $40 (2,000); Pro Max $100 (5,000); Power $200 (10,000). Add-on credits $0.04/credit. 🟢
- **Model access:** Auto, Claude Sonnet 5/Opus 5 (paid), open-weight (Qwen, DeepSeek, MiniMax). "Not all premium models available in all countries/regions." 🟢
- **India:** Kiro is AWS-built; AWS has India regions. Sign-up via AWS Builder ID or social login. Payment via AWS billing (credit card). Free tier available globally. Premium model availability in India is not explicitly confirmed — verify at signup. 🟡
- **License note:** Kiro CLI uses AWS IP License (not Apache 2.0 like Q CLI) — compliance flag for enterprise. 🟢
- **OpenCode compatibility:** Kiro is an IDE/CLI; OpenCode is terminal. Complementary, but both are agent tools — pick one per workflow. 🟡

### 3.5 Tabnine
- **Status:** Free/individual tier **discontinued** (April 2025). Now enterprise-focused. 🟢
- **Pricing:** Dev plan ~$9-12/mo (individual, basic completions); Enterprise $39/user/mo (Code Assistant) or $59/user/mo (Agentic Platform), annual only. 🟡 (conflicting sources: $9/mo vs $12/mo vs $39/mo — official page now shows $39/$59 enterprise; individual Dev plan availability uncertain).
- **Model access:** Self-hosted/air-gapped option; IP indemnity. 🟢
- **India:** Enterprise sales required; no India-specific plan. 🟡
- **OpenCode compatibility:** Tabnine is an IDE plugin (autocomplete); complementary to OpenCode. 🟢

### 3.6 Sourcegraph Cody
- **Status:** Free & Pro **discontinued July 23, 2025**. Enterprise-only now. 🟢
- **Pricing:** ~$59/user/mo (annual contract); bundled Sourcegraph packages from ~$16,000/yr. 🟡
- **India:** Enterprise procurement via sales; no self-serve. 🟡
- **OpenCode compatibility:** N/A (enterprise, not individual). 🟢

### 3.7 Replit
- **Pricing:** Starter (Free); Core $20/mo ($18 annual); Pro $100/mo ($90 annual); Enterprise custom. 🟢 Source: replit.com/pricing (Oct 2026).
- **Model access:** Replit Agent (powered by LLMs), 50+ languages, autonomous build+deploy+host. 🟢
- **India:** Replit is global; accepts cards. No India-specific pricing. Taxes apply by location. 🟡
- **OpenCode compatibility:** Replit is a browser IDE; OpenCode is local terminal — different workflows, but can use Replit for hosting/deploy. 🟡

### 3.8 Bolt (StackBlitz)
- **Pricing:** Free $0 (1M tokens/mo, 300K/day); Pro $18/mo annual ($216/yr, 10M tokens/mo, rollover); Teams $27/mo per member; Enterprise custom. 🟢 Source: bolt.new/pricing.
- **Model access:** Token-based; access to newest AI models on Pro. 🟢
- **India:** Global; card payments. No UPI. 🟡
- **OpenCode compatibility:** Bolt is a browser builder; complementary. 🟡

### 3.9 Lovable
- **Pricing:** Free ($0, 5 daily credits up to 30/mo); Pro $25/mo ($250/yr ≈ $21/mo, 100 base monthly credits + 5 daily); Business $50/mo; Enterprise custom. 🟡 (from earlier search; pricing page is JS-rendered).
- **Model access:** Message-based credits; full-stack web apps. 🟢
- **India:** Global; card payments. No UPI mentioned. 🟡
- **OpenCode compatibility:** Complementary (browser builder vs terminal agent). 🟡

### 3.10 v0 (Vercel)
- **Pricing:** Free $0 ($5 credits, 7 msg/day); Plus $30/user/mo ($30 included monthly credits + $2 daily); Business $100/user/mo; Enterprise custom. 🟢 Source: v0.dev/pricing.
- **Model access:** v0 Mini/Pro/Max/Max Fast (token-priced). Frontend/React/Next.js focused. 🟢
- **India:** Global; prices in USD, exclude GST. Vercel accepts cards. "Do you offer purchasing power parity (PPP)?" is in FAQ (implies no PPP). 🟡
- **OpenCode compatibility:** Complementary. 🟡

### 3.11 Bonus: Google Antigravity (not asked but relevant)
- **Pricing:** Individual Free $0; Google AI Pro ~₹1,950/mo in India (includes Antigravity expanded rate limits + Gemini 4 Argon); Google AI Ultra (higher, ~$250/mo globally); Business via Google Cloud from $30/seat. 🟢 Source: one.google.com (India page).
- **India:** Yes — Google AI plans are available in India (Pro ₹1,950/mo). Antigravity is a Google product with India support. 🟢
- **OpenCode compatibility:** Antigravity is an IDE; OpenCode complementary. 🟡

### 3.12 Bonus: OpenCode itself
- **Price:** Free (MIT, open source). Optional: OpenCode Go $10/mo (29 curated models, generous limits) or Go Plus $40/mo (higher limits). Zen = pay-as-you-go at API rates. Enterprise = custom (SSO, internal gateway). 🟢 Source: opencode.ai/go.
- **Model access (Go):** Kimi K3.1 Pro, MiniMax M3/M3.1 Flash, GPT 6/5.6 Luna, Claude Haiku 5.5, Gemini 4 Argon, GLM-5.3, DeepSeek V4.1 Flash/Pro, Qwen 3.8, Grok 4.7, Muse Spark, and more. No Claude Sonnet/Opus or GPT-5.5 in Go (use Zen/BYOK for those). 🟢
- **India:** OpenCode is a CLI tool, works globally. Payment for Go via card (Stripe). No UPI mentioned but card works. 🟡
- **Compatibility:** OpenCode runs in terminal alongside any IDE (Cursor, Windsurf, VS Code). It cannot consume Cursor/Windsurf subscriptions — BYOK or Go/Zen only. Anthropic blocked Claude subscription credentials for third-party tools (Jan 2026), so Claude Pro/Max cannot be used with OpenCode; use API keys. 🟢

---

## 4. India availability matrix

| Tool | India signup | Payment | India-specific plan | Confidence |
|---|---|---|---|---|
| Cursor | Yes | UPI (Start only, legacy); cards/Google Pay/Apple Pay/Link (X Sub) | Yes — Start ₹649/mo (legacy, India-only) | 🟢 |
| Windsurf/Devin | Yes (global) | Cards (Stripe, inferred) | No | 🟡 |
| Cline | Yes (global) | N/A (free + BYOK) | No | 🟢 |
| Continue | N/A (acquired by Cursor) | — | — | 🟢 |
| Aider | Yes (global) | N/A (free + BYOK) | No | 🟢 |
| Amazon Q/Kiro | Yes (AWS India) | AWS billing (card) | No (but AWS India region) | 🟡 |
| Tabnine | Enterprise sales only | Enterprise contract | No | 🟡 |
| Sourcegraph Cody | Enterprise sales only | Enterprise contract | No | 🟡 |
| Replit | Yes (global) | Cards | No | 🟡 |
| Bolt | Yes (global) | Cards | No | 🟡 |
| Lovable | Yes (global) | Cards | No | 🟡 |
| v0 | Yes (global) | Cards | No (no PPP) | 🟡 |
| Google Antigravity | Yes | Google One (UPI via Google Pay? cards) | Yes — Pro ₹1,950/mo | 🟢 |
| OpenCode | Yes (global CLI) | Cards (Stripe) | No | 🟡 |
| GitHub Copilot | Yes (global) | Cards/GitHub billing | No (but prices in USD) | 🟡 |

**Key India insight:** Only **Cursor Start (₹649)** and **Google AI Pro (₹1,950)** offer INR pricing with local payment. Everyone else bills in USD. Indian credit/debit cards generally work but may face 3DS/bank declines; UPI is the most reliable recurring payment in India, and only Cursor Start supports it directly.

---

## 5. OpenCode compatibility summary

| Tool | Can use alongside OpenCode? | Notes |
|---|---|---|
| Cursor | ✅ Yes | Complementary: IDE (Cursor) + terminal agent (OpenCode). OpenCode runs in Cursor's terminal. Cursor subscription is independent of OpenCode. |
| Windsurf | ✅ Yes | Same as above. |
| Cline | ✅ Yes | Cline is an IDE extension; OpenCode is terminal. Both can be active. Cline also has its own CLI. |
| Aider | ✅ Yes | Both terminal; run in separate sessions. |
| GitHub Copilot | ✅ Yes | Copilot is IDE extension; OpenCode is terminal. |
| Kiro | ⚠️ Partial | Both are agents; redundant. Pick one. Kiro CLI replaces Q CLI. |
| Tabnine | ✅ Yes | Tabnine = autocomplete plugin; OpenCode = agent. Complementary. |
| Replit/Bolt/Lovable/v0 | ✅ Yes | Browser builders; OpenCode is local. Different workflows. |
| Google Antigravity | ✅ Yes | Antigravity is an IDE; OpenCode complementary. |

**Important OpenCode caveat (Jan 2026):** Anthropic blocked third-party tools from using Claude Pro/Max subscription credentials. OpenCode cannot use a Claude subscription — use API keys (Zen/BYOK) or OpenCode Go ($10/mo) for Claude Haiku 5.5 only. For Sonnet/Opus via OpenCode, use Zen pay-as-you-go or BYOK with your own Anthropic API key. 🟢

---

## 6. Value math — best value picks for India (Oct 2026)

### Tier 1: Cheapest real token value
1. **OpenCode Go — $10/mo (~₹835 + GST ≈ ₹985)** 🟢
   - 29 models including DeepSeek V4.1 Flash (~34,670 req/5h), MiMo-V2.6-Flash (~30,100 req/5h), GLM-5.3-Flash (~6,320 req/5h), GPT 6 Luna, Claude Haiku 5.5, Gemini 4 Argon, Grok 4.7.
   - **Best $/token ratio** of any subscription. Works with any agent. Zero data retention on most models.
   - Caveat: No Claude Sonnet/Opus or GPT-5.5; use Zen/BYOK for those.

2. **Cursor Start — ₹649/mo (legacy, India-only)** 🟢
   - Only INR-priced agent plan with UPI. Grok 4.7/4.6/4.5 + Composer 2.5. ~3× cheaper than Pro in INR terms.
   - Caveat: Fixed medium effort, Fast off, no third-party models, no on-demand spend, monthly (not weekly) pool. Once you upgrade away, you can't return.

3. **GitHub Copilot Pro — $10/mo (~₹835 + GST)** 🟢
   - Unlimited inline suggestions, agent mode, cloud agent, CLI. $15/mo AI credits + $5 flex. Cheapest "polished IDE assistant."
   - Caveat: Premium models cost credits; less agentic power than Cursor/Cline.

### Tier 2: Best mid-range ($20-30/mo)
4. **Cursor Premium (X Sub) — $30/mo** or **legacy Pro — $20/mo** 🟢
   - Premium: 4× Plus weekly pool + Cloud Agents + third-party models at API price. Legacy Pro: $20 credit pool + unlimited tab + on-demand.
   - For India: legacy Pro ≈ ₹1,670 + 18% GST ≈ ₹1,970/mo; Premium ≈ ₹2,505 + GST ≈ ₹2,956/mo.
   - Best if you want Claude/GPT/Gemini inside the IDE with predictable-ish billing.

5. **Windsurf Pro — $20/mo** 🟢
   - Same price as Cursor Pro but quota-based (50-70 prompts/day). Student discount 50%+ if .edu qualifies. Strong value with SWE-2 + Cascade.

6. **Google AI Pro — ₹1,950/mo** 🟢
   - INR pricing, includes Antigravity (agent IDE) with expanded Gemini 4 Argon rate limits + Gemini in Workspace + 5TB storage + YouTube Premium Lite. Excellent bundle value if you use Google ecosystem.

7. **Kiro Pro — $20/mo** 🟢
   - 1,000 credits + full model roster (Claude Sonnet/Opus 5). Spec-driven development. Good if you want structured agent workflows.

### Tier 3: Heavy users ($100-200/mo)
8. **Cursor Ultra / Super — $100-200/mo** or **Windsurf Max — $200/mo** or **Copilot Max — $100/mo** 🟢
   - Only if you hit limits on mid-tier. Most devs don't need this.

### Tier 4: Free / near-free
9. **Cline + Aider (free) + Ollama local models** = $0 (model cost only). Best for privacy and budget. 🟢
10. **Gemini CLI free tier** (1,000 req/day) + **OpenCode free** + local models. 🟡

### Recommended stack for an India dev (best value)
- **Minimum viable:** OpenCode (free) + OpenCode Go ($10/mo) + Ollama (free local) = ~₹985/mo. Covers 90% of coding needs with 29 models.
- **IDE-centric:** Cursor Start (₹649, if eligible and staying on free plan) OR Cursor Premium ($30) + OpenCode Go ($10) = ~₹3,800/mo with Claude/GPT/Gemini access.
- **Google ecosystem:** Google AI Pro (₹1,950) + OpenCode Go ($10) = ~₹2,800/mo. Gives Antigravity + Gemini 4 Argon + Workspace AI.
- **Avoid:** Tabnine (enterprise-only, expensive), Sourcegraph Cody (enterprise-only), v0/Bolt/Lovable (app builders, not IDEs — different use case, token-opaque pricing).

---

## 7. Sources

- Cursor pricing/docs: cursor.com/help/account-and-billing/pricing, cursor.com/help/account-and-billing/cursor-start, cursor.com/docs/models-and-pricing, cursor.com/start, cursor.com/blog/cursor-start-india, docs.x.ai/x-subscription/*
- Windsurf/Devin: devin.ai/pricing, nocode.mba/articles/windsurf-pricing, cloudzero.com/blog/windsurf-pricing, usagepricing.com/blueprint/codeium
- GitHub Copilot: github.com/features/copilot/plans
- Kiro: kiro.dev/pricing, kiro.dev/faq, digitalapplied.com (Q→Kiro migration)
- OpenCode: opencode.ai/go, aiidelist.com/ide/opencode, morphllm.com comparisons
- Replit: replit.com/pricing
- Bolt: bolt.new/pricing
- v0: v0.dev/pricing
- Lovable: lovable.dev/pricing (JS-rendered; prices from earlier comparison articles)
- Google AI: one.google.com (India)
- Tabnine: tabnine.com/pricing, krater.ai, layer3labs.io
- Sourcegraph Cody: sourcegraph.com/docs/cody, aicentralresources.com
- Cline: github.com/cline/cline
- Aider: aider.chat
- Continue: continue.dev (acquired by Cursor)
- Google Antigravity: antigravity.google/pricing

**Confidence notes:** Prices for Lovable, Windsurf India availability, Tabnine individual Dev plan, and v0 India PPP were not directly verifiable from official pages (JS-rendered or no region page). Marked 🟡/🔴 accordingly. All USD prices exclude tax; India GST (18%) typically applies. Exchange rate assumed ~₹83.5/USD for INR conversions (illustrative).