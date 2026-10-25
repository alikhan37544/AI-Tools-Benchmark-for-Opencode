# AI Tools Benchmark for OpenCode — Go Plan Deep Dive

> **Full refresh: October 1, 2026 · roster refreshes: October 13, 16 and 25, 2026.** 29 Go models · 18 task categories · every major benchmark source · **calibrated to this machine's real OpenCode usage history**.
> 🌐 **Live site (GitHub Pages): https://alikhan37544.github.io/AI-Tools-Benchmark-for-Opencode/**
> Interactive report: **[opencode-go-analysis.html](./opencode-go-analysis.html)** — searchable, sortable, with charts.
>
> **🆕 Oct 25 (latest):** +**Kimi K3.1 Pro** (AA 55.1 — the highest intelligence ever on Go) · +**MiniMax M3.1 Flash** (AA 43 at $0.22/AA task — the new paid value anchor) · **Gemini 4 Argon is now ZDR/not trained** (the old Contributor warning is withdrawn) · **Step 5 back to a $15 cap** (4× promo ended) · **Space Bunny / LongCat 2.5 Preview Free removed** · **this machine runs OpenCode v2.1.4** (v1 = 1.19.4; OmO 5.1.48). **New analyses: [India availability](./analysis/14-india-availability.md) · [Go vs direct](./analysis/12-opencode-vs-direct.md) · [best-value plans](./analysis/13-best-value-coding-plans.md).**
> **Oct 16:** +Gemini 4 Argon (AA 53) · Step 5 free→paid · +Beam Free · Zen free twins (DeepSeek/GLM) · Grok 4.6 / Kimi K2.6 / MiniMax M2.7 removed · v2.0.31 migration.
> **Oct 13:** +Claude Haiku 5.5 · +Step 5 Preview Free · DeepSeek cap $60→$80 · Space Bunny free→paid.

This repo answers eight questions with evidence, not vibes:

1. Which models are on OpenCode Go?
2. How good is each one — across benchmarks, independent labs, HuggingFace, and real user feedback?
3. Which model is best for each specific task (backend, frontend, DB, integrations, agentic deploy, git, visual QA, image analysis, planning, hardware/ROM/general intelligence)?
4. How long can you program continuously before limits bite?
5. What is the best intelligence-per-dollar overall and per task?
6. What are the "pay a little more → huge intelligence jump" tiers?
7. **Is Go worth it versus paying each provider directly?**
8. **Which plans actually work from India — signup, phone, payment and model access?**

---

## TL;DR — the answers

### 1. The roster (29 models, Oct 25, 2026)
**Kimi K3.1 Pro (NEW)** · Gemini 4 Argon · Grok 4.7 · GLM-5.3/5.3-Flash/5.2 · GPT 6 Luna, GPT 5.6 Luna · Claude Haiku 5.5 · Kimi K3/K2.7 Code · DeepSeek V4.1 Flash/V4 Pro · MiMo-V2.6-Pro/Flash, MiMo-V2.5/Pro · **MiniMax M3.1 Flash (NEW)**, MiniMax M3 · Qwen3.8 Max/Flash, Qwen3.7 Plus · LongCat-2.0 · Hy4 preview, Hy3 · Muse Spark 1.3/1.2 Contributor · Step 5 (paid) · **free:** Beam Free. **Removed:** Space Bunny, LongCat 2.5 Preview Free, Grok 4.6, Kimi K2.6, MiniMax M2.7, DS V4 Flash.
Plans: **Go $10/mo**, **Go Plus $40/mo**. Per-model dollar caps; 5h = 20% of monthly, weekly = 50%, monthly = 100%. → [Full details](./analysis/01-go-roster-and-limits.md)

### 2. Best models overall
| | Winner | Why |
|---|---|---|
| **Highest intelligence on Go** | **Kimi K3.1 Pro** (AA 55.1) | New AA ceiling; 1M ctx, vision, 269 heavy req/mo — but a ration, not a driver |
| **Best independent agentic coder** | **Gemini 4 Argon** (AA 53) | Vals v2.2 **69.24% (#3 overall, #1 Go)**, 728 req/mo, and **now ZDR/not trained** |
| **Best privacy-safe intelligence** | **Gemini 4 Argon** / **MiMo-V2.6-Pro** (AA 46) / **Grok 4.7** (AA 46) | Argon is the highest-AA ZDR model on Go; MiMo-Pro is the cheapest AA 46 |
| **Best marathon / 1M-context** | **Kimi K3.1 Pro** | K3 lineage: SWE-Marathon 42.0, FrontierSWE 81.2, OSWorld 84.8; 3.1 adds 1M ctx + vision |
| **Best visual/OS agent** | **Qwen3.8 Max** (AA 45) | **#1 model in the world on OSWorld 86.1**; LMArena Vision **#9** (corrected Oct 25) |
| **Best daily driver at volume** | **DeepSeek V4.1 Flash** (AA 39) | 209–232 tok/s, native vision, 25.5k req/mo ($80 cap), **1017 checkpoint scores AA 45** — free twin on Zen |
| **Best paid value workhorse** | **MiniMax M3.1 Flash** (AA 43) | 4,975 req/mo at $0.0020/req plan-effective; 112.8 tok/s, 1.35s TTFT, **10,697 pts/$** |
| **Best free coder** | **GLM-5.3-Flash Free** (AA 42, zero-retention) | AA 42 at $0/req; DeepSeek V4.1 Flash Free (AA 39) is the high-capacity runner-up |
| **Best free agentic bulk** | **Beam Free** (AA 30) | Reflection AI 501B/23B MoE, Apache-2.0 weights; 30-day retention, no training |
| **Best subagent / quick-task** | **Claude Haiku 5.5** | Fastest Claude, TB4.0 39.2% max, 1M ctx |

→ [Full benchmark dossier](./analysis/02-benchmarks.md)

### 3. Best model per task (Go roster)
| Task | Best on Go | Value pick |
|---|---|---|
| Backend / API / refactors | **Kimi K3.1 Pro** (hard/marathon) / DeepSeek V4.1 Flash (daily) | MiniMax M3.1 Flash |
| Frontend / UI | Muse Spark 1.3 | GLM-5.3-Flash |
| Database / SQL | GLM-5.3 (GLM-5.2 lineage won Spider 2.0-Lite) | MiniMax M3.1 Flash |
| Integrations / auth / webhooks | Kimi K3.1 Pro / Hy4 preview (Toolathlon 74.1) | DeepSeek V4.1 Flash |
| Agentic terminal / DevOps / git / deploy | **Gemini 4 Argon** (Vals #1 Go) / Kimi K3.1 Pro | DeepSeek V4.1 Flash |
| Long-horizon autonomy | Kimi K3.1 Pro | Step 5 / DeepSeek V4.1 Flash |
| Visual QA / Playwright | **Qwen3.8 Max (OSWorld #1 worldwide)** | Qwen3.8 Flash |
| Image / OCR / Arabic docs | Qwen3.8 Max | Qwen3.8 Flash / DeepSeek V4.1 Flash |
| Planning / architecture | **Kimi K3.1 Pro (55.1)** / Gemini 4 Argon (53, ZDR) | MiniMax M3.1 Flash |
| Debugging / RCA | Kimi K3.1 Pro / Grok 4.7 (edge cases) | GLM-5.3-Flash Free |
| Long context (huge repos/logs) | Kimi K3.1 Pro (1M) / DeepSeek V4.1 Flash (cheapest cache) | DeepSeek V4.1 Flash Free |
| Bulk edits / tests / explore | MiniMax M3.1 Flash / Claude Haiku 5.5 | GLM-5.3-Flash Free (AA 42 at $0) |
| General intelligence / research | Kimi K3.1 Pro (55.1) / Gemini 4 Argon (53) | MiniMax M3.1 Flash |
| Data / ML notebooks | Kimi K3.1 Pro / MiniMax M3.1 Flash | DeepSeek V4.1 Flash |
| **Systems: overclock / ROM / drivers / homelab** | Kimi K3.1 Pro / Grok 4.7 | DeepSeek V4.1 Flash + frontier for brick-risk steps |
| Voicebot / realtime telephony | DeepSeek V4.1 Flash (integration/debug loops) | MiMo-V2.6-Flash |

→ [Full task playbook + routing for this machine](./analysis/03-task-playbook.md)

### 4. How long can you program continuously?
Measured from **your actual history** (12,973 requests on DeepSeek V4.1 Flash @ max, Sep 15–Oct 1). The fresh v2 DB (Oct 25: 8.2k in / 1.25k out / 153k cache per request) is within ~5% of the frozen profile:

| Window | Your peak | Cap | Used |
|---|---|---|---|
| 5-hour rolling | $5.99 | $16 | **37%** ← why it "feels unlimited" |
| 7-day rolling | $24.77 | $40 | **62%** |
| Monthly pace | ~$45–73/mo | $80 | **under cap except crunch months** |

At your token profile (7.8k input + 146k cache + 1.1k output per request), DeepSeek V4.1 Flash gives **~25,500 requests/month**, not the 173,000 the docs estimate (your requests are ~6.8× heavier). Premium models are **minutes per 5h and tasks/week**: **Kimi K3.1 Pro ~269/mo**, Kimi K3 ~179, Grok 4.7 ~158, Qwen3.8 Max ~256, GLM-5.3 ~279, **Gemini 4 Argon ~728**, **MiniMax M3.1 Flash ~4,975** (the only premium-tier model with real daily capacity).
**Cheat code:** DeepSeek is 50% off off-peak (after ~15:30 IST + weekends) → doubles your effective cap. **Free cheat code 2.0:** **DeepSeek V4.1 Flash Free** and **GLM-5.3-Flash Free** are zero-retention and cost nothing — an unlimited floor after caps bind.
→ [Full limits & burn-rate analysis](./analysis/04-limits-and-burn-rate.md)

### 5. Intelligence per dollar
| Metric | Winner |
|---|---|
| AA points per limit-$ | **Muse Spark 1.3 Contributor — 37,152** (privacy caveat: trains) |
| Best free (zero-retention) | **GLM-5.3-Flash Free — AA 42 at $0/req**, then DeepSeek V4.1 Flash Free (AA 39) |
| Best sustainable paid | **DeepSeek V4.1 Flash — 12,426 pts/$**, 25.5k req/mo (1017 checkpoint: 14,516) |
| Best paid quality/value | **MiniMax M3.1 Flash — 10,697 pts/$**, AA 43, 4,975 req/mo |
| Best premium capacity | **Gemini 4 Argon — 1,286 pts/$**, AA 53, 728 req/mo, **ZDR** |
| Highest intelligence on Go | **Kimi K3.1 Pro — AA 55.1 at 988 pts/$**, 269 req/mo |
| Worst value on Go | Grok 4.7 (483 pts/$), Kimi K3 (526) — ~158–179 req/mo |

The jump from 39 (DeepSeek) to 43–46 (M3.1 Flash / K3 / Grok / MiMo-Pro) costs **1.3–31× per request** for **+4–7 AA**. The two big exceptions: **Argon** (+14 AA, 728 req/mo, now ZDR) and the **free twins** (AA 39–42 at $0). Beyond Go, Claude Opus 5.5 is **AA 58 (+19)**, for must-not-fail work only.
→ [Full value & tier analysis](./analysis/05-intelligence-per-dollar.md)

### 6. Tier structure ("pay more for a jump")
| Tier | Models | Verdict |
|---|---|---|
| **T0 Free** | **GLM-5.3-Flash Free, DeepSeek V4.1 Flash Free (both zero-retention)**, Beam Free, Flint 40B (may train), MiMo-Flash Free, Nemotron free, Big Pickle | Unlimited-ish while windows last; only the two zero-retention twins can carry real work |
| **T1 Workhorses** | DeepSeek V4.1 Flash, MiMo-V2.6-Flash, **MiniMax M3.1 Flash**, GLM-5.3-Flash, Muse Spark*, LongCat-2.0, Hy3, Qwen3.8 Flash, Claude Haiku 5.5, Step 5 ($15) | Drive 90% of work here. *Muse trains on data |
| **T2 Premium $15–30** | MiMo-V2.6-Pro, **Gemini 4 Argon ($30, ZDR)**, GPT 6 Luna, GPT 5.6 Luna, Hy4 preview | Best quality/call: planning, hard debug, OCR verify |
| **T3 Rations $15** | **Kimi K3.1 Pro (55.1)**, Kimi K3, GLM-5.3, Qwen3.8 Max, Grok 4.7 | 1–5 big tasks/week each; the hard 5% |
| **T4 Beyond Go** | Opus 5.5 (58), GPT-6 Astra/Fable 5.1 (53), Muse Wonder (52–56) | Copilot/Zen; must-not-fail only |

**Go Plus ($40):** 2×–8× limits. Great for GLM-5.3 (8×), the $15 rations (4×), Argon ($30→$120), M3.1 Flash ($20→$80); poor for DeepSeek V4.1 Flash/MiMo-Flash/Muse Spark (2×). For a DeepSeek-heavy workflow, **Go + $30 Zen overflow beats Go Plus**.

### 7. Go vs going direct
Go's per-token prices are essentially the **same as direct** for almost every model. What $10 buys is a bundle of **prepaid allowances worth $15–$80 per model** — a 1.5×–8× multiplier, siloed per model. **Go wins** if you use several models or a high-multiplier one (DeepSeek 8×, MiMo-Flash/GLM-Flash 6×); **direct or a specialist plan wins** below the single-model break-even or when you need provider features. Break-even at your profile: **K3.1 Pro 179 req/mo · Argon 243 · GLM-5.3 186 · Step 5 394 · Grok 105 · M3.1 Flash 2,500 · DeepSeek 3,226**. → [Full per-model break-even](./analysis/12-opencode-vs-direct.md)

### 8. India availability — and the best-value plans
**OpenCode Go is the only plan with documented UPI**, no phone gate, and 29 models behind one key — the clear India-first buy. **StepFun Step Plan** is the raw-value wildcard (verify credits), **Z.ai Lite** the GLM specialist, **Xiaomi Lite** the cheap MiMo entry, **Kimi Code** the K3.1 Pro subscription, **MiniMax M Plan** the opaque one. **Alibaba Token Plan (Singapore-only) and Meta Muse Code (US-first) are blocked from India.** → [India matrix](./analysis/14-india-availability.md) · [Best-value plan ranking](./analysis/13-best-value-coding-plans.md)

| # | Plan | Price | Heavy req/mo (verified model) | India |
|---|---|---|---|---|
| 1 | **OpenCode Go** | **$10** | 269 K3.1 Pro · 728 Argon · 4,975 M3.1 Flash · 25,484 DeepSeek | 🟢 **UPI** |
| 2 | StepFun Step Plan Pro | $29 | ~45,000 Step 5 *if credit math holds* | 🟢 Stripe |
| 3 | Z.ai GLM Coding Plan Lite | $18 | 1,319 GLM-5.3 peak / 2,639 off-peak | 🟢 Card/PayPal |
| 4 | Xiaomi MiMo Token Plan Lite | $6 | 3,173 Flash / 1,218 Pro | 🟢 Overseas email + Waffo |
| 5 | Kimi Code Plus | $19 | Opaque (K3.1 Pro included) | 🟢/🟡 Card |
| 6 | MiniMax M Plan Go | $22 | Opaque (1×/3×/7.5×) | 🟡 Stripe |
| — | Alibaba Token Plan | $6–68 | — | 🔴 Blocked |
| — | Meta Muse Code | $5–200 | — | 🔴 Blocked |

---

## The recommended setup

```jsonc
// OpenCode v2.1.4 (what this machine runs). The same model IDs work on v1.19.4.
{
  "$schema": "https://opencode.ai/config.json",
  "model": "opencode-go/deepseek-v4.1-flash",
  "small_model": "opencode-go/mimo-v2.6-flash",
  "agent": {
    "plan":    { "model": "opencode-go/gemini-4-argon" },    // ZDR; or kimi-k3.1-pro for AA 55.1
    "explore": { "model": "opencode-go/claude-haiku-5-5" },  // free lane alt: opencode/glm-5.3-flash-free
    "build":   { "model": "opencode-go/deepseek-v4.1-flash" },
    "value":   { "model": "opencode-go/minimax-m3.1-flash" }
  }
}
```

**India settings:** pay Go/Plus with **UPI** (card/Link/Alipay/WeChat also listed; top-ups add 4.6% + $0.31). In Go's model settings set **DeepSeek → Regions = Global** (the default allowed regions are Europe & US). Enable **"Allow paid endpoints that train on request data"** only for Muse Spark on non-client work — leave it off everywhere else.

Free-tier routing note: `opencode/deepseek-v4.1-flash-free` and `opencode/glm-5.3-flash-free` are zero-retention free models that keep working after Go limits — use them as the bulk/free floor.

Escalate per task: `Kimi K3.1 Pro` (hardest 5%) · `Qwen3.8 Max` (visual QA) · `Gemini 4 Argon` (planning/agentic, ZDR) · `Muse Spark 1.3` (design/general, non-client) · `MiMo-V2.6-Pro` (hard reasoning, cheap) · Copilot `Opus 5.5` (must-not-fail).
→ [Full configs + workflow](./analysis/07-recommended-config.md)

---

## Files

| File | Contents |
|---|---|
| **[opencode-go-analysis.html](./opencode-go-analysis.html)** | Interactive single-page report: searchable/sortable tables, charts, all tiers (start here) |
| [analysis/01-go-roster-and-limits.md](./analysis/01-go-roster-and-limits.md) | Roster, plans, exact pricing/limit mechanics, free models, roster history |
| [analysis/02-benchmarks.md](./analysis/02-benchmarks.md) | Every model's benchmarks (AA v4.3.2, SWE-bench, Terminal-Bench, OSWorld, LMArena, MMLU/MLE…) with sources and confidence ratings |
| [analysis/03-task-playbook.md](./analysis/03-task-playbook.md) | Best model per task + personalized routing for this machine's projects, privacy and contract constraints |
| [analysis/04-limits-and-burn-rate.md](./analysis/04-limits-and-burn-rate.md) | Your measured usage, per-model capacity at your token profile, continuous-hours math, off-peak strategy, Go Plus math |
| [analysis/05-intelligence-per-dollar.md](./analysis/05-intelligence-per-dollar.md) | Value tables, AA points/$, cognitive throughput, tier structure, jump economics, Go vs BYOK |
| [analysis/06-free-models-and-privacy.md](./analysis/06-free-models-and-privacy.md) | Data policies (training/retention) per route, free models, local LLM options |
| [analysis/07-recommended-config.md](./analysis/07-recommended-config.md) | Copy-paste configs (v2-first, v1 notes), role matrix, workflow patterns |
| [analysis/08-oh-my-opencode.md](./analysis/08-oh-my-opencode.md) | Oh My OpenCode guide: agents, categories, hooks, loops + **Go model map for very heavy work** |
| [analysis/09-opencode-v1-vs-v2.md](./analysis/09-opencode-v1-vs-v2.md) | v1 vs v2 differences, pros/cons, migration checklist, OMO compatibility |
| [analysis/10-plugins-and-stacks.md](./analysis/10-plugins-and-stacks.md) | Best plugins, ranked MCPs, skills/rules, 3 copy-paste stacks, anti-recommendations |
| [analysis/11-amazing-additions.md](./analysis/11-amazing-additions.md) | Personalized power-ups: Azure autonomy, browser/RPA, memory, safety, scheduler, voicebot, OCR |
| **[analysis/12-opencode-vs-direct.md](./analysis/12-opencode-vs-direct.md)** | **NEW — per-model Go vs direct break-even, multipliers, privacy/features** |
| **[analysis/13-best-value-coding-plans.md](./analysis/13-best-value-coding-plans.md)** | **NEW — best-value coding plans ranked, plan math, decision table** |
| **[analysis/14-india-availability.md](./analysis/14-india-availability.md)** | **NEW — India matrix: signup, phone, payment, model access + pre-payment checklist** |
| **[analysis/15-all-token-plans.md](./analysis/15-all-token-plans.md)** | **NEW — every token plan compared (Copilot, Claude, ChatGPT, Gemini, Cursor, Windsurf, Kiro, Chinese + aggregators), best deals ranked** |
| **[analysis/16-cursor-windsurf-ide-plans.md](./analysis/16-cursor-windsurf-ide-plans.md)** | **NEW — Cursor/Windsurf/Kiro/IDE tools deep-dive: pricing, India availability, OpenCode compatibility** |
| [RESEARCH-GUIDE.md](./RESEARCH-GUIDE.md) | How this was researched and how to update it |

---

## New: Oct 25 refresh — K3.1 Pro + M3.1 Flash, Argon ZDR, India + plan rankings

- **Kimi K3.1 Pro joined Go (AA 55.1):** the highest intelligence ever listed on Go — 1M context, vision, Vals v2.2 **62.52%**, **$2.11 per AA task**, **$2/$10/$0.20** (cache write $2) and a **$15 cap** → **~269 heavy req/mo** (5h 54, week 134). It is a scalpel, not a driver. Upstream OmO 5.1.47 added K3.1 Pro-specific Sisyphus/Atlas prompts.
- **MiniMax M3.1 Flash joined Go (AA 43):** 112.8 tok/s, 1.35s TTFT, **$0.22/AA task**, 180M verbosity, **$0.15/$0.60/$0.015** with a **$20 cap** → **~4,975 req/mo** and **10,697 pts/$**. It dominates GLM-5.3-Flash on both price and quality at the paid tier.
- **Gemini 4 Argon correction:** the SKU is now plain **`gemini-4-argon`** (not Contributor) at **$2/$10/$0.10**, **$30 cap (50% off through Nov 30)**, ~728 req/mo. Go's privacy table documents **Not used / 0 days** — the Oct 16 "trains on your data" warning is **withdrawn**. Vals v2.2: **69.24%, #3 overall and #1 among Go models** (Sonnet 5.5 70.85 and Opus 5.5 70.18 lead).
- **Step 5 promo ended:** back to a **$15 cap** (~591 req/mo), still AA 44 and open-weight.
- **Roster removals:** **Space Bunny** and **LongCat 2.5 Preview Free** left Go. Go is still **29 models**.
- **DeepSeek 1017 checkpoint:** AA now measures **45** (169.1 tok/s, TTFT 1.18s, $0.26/task, 210M verbosity) versus 39 for the original — same Go ID and price. Keep **39 as the conservative baseline**, treat 45 as upside until routing is consistent.
- **Privacy refresh:** only **Muse Spark 1.3/1.2 Contributor** still trains. Grok/GPT/Haiku/Beam are 30-day retention, no training. DeepSeek ZDR is valid **through Oct 31, 2026**. Free-list churn: Space Bunny, LongCat 2.5, LL Alpha, Muse free and Exo are gone; **Flint 40B Free** is new (30-day + may train).
- **Benchmark corrections:** **Vals v2.2** puts Argon 69.24% (#3 overall), K3.1 Pro 62.52%, DeepSeek 1017 61.26%, GLM-5.3 59.73%, M3.1 Flash 53.78%. **LMArena Vision: Qwen3.8 is #9, not #2.**
- **This machine runs OpenCode v2.1.4** (v1 **1.19.4**): 2.1.0 Windows PTYs/todo/5-min hang fix, 2.1.2 `OPENCODE_DISABLE_FREE_MODELS=1`, 2.1.3 Bun 1.4.4 security + voice models, 2.1.4 MCP input forms, `experimental.background_compaction`, `opencode debug heap-dump`, TUI tools.
- **OmO 5.1.48 (Oct 25):** `senpi 2026.10.25-2`; **748-skill startup 83s → 1.4s**; nested task session trees. **OpenCode v2 dual-host is still not shipped** — PR #9391 is open with `mergeable_state: dirty`, last updated Oct 15.
- **Telemetry (week to Oct 25):** DeepSeek V4.1 Flash **119T** (#1, +39%), MiniMax M3.1 Flash **37T** (#2, +92%), GLM-5.3-Flash 8.9T (+69%), Muse Spark 7.6T (−76%), MiMo-Flash 7.2T (−35%), Beam 5.3T (+86%), DeepSeek 1017 1.3T new, iceman 661B new.
- **New analyses:** **[12 — Go vs direct](./analysis/12-opencode-vs-direct.md)**, **[13 — best-value plans](./analysis/13-best-value-coding-plans.md)**, **[14 — India availability](./analysis/14-india-availability.md)**, **[15 — all token plans](./analysis/15-all-token-plans.md)**. Alibaba Token Plan and Meta Muse Code are **excluded from the rankings** because they are not practically available in India. Analysis 15 extends the comparison to every subscription, credit bundle and PAYG option found across Copilot, Claude, ChatGPT, Gemini, Cursor, Windsurf, Kiro, StepFun, Z.ai, Xiaomi, Kimi, MiniMax, plus DeepSeek, Alibaba, Tencent, Zhipu, Mistral, DeepInfra, Together, Fireworks, Groq, Cerebras, AWS, Azure and Vertex.

## New: Oct 16 refresh — Argon on Go, Step 5 paid + open weights, free-model explosion, v2 migration

- **Gemini 4 Argon Contributor joined Go (Oct 13):** the AA 53 frontier model arrived at $4/$20/$0.20 with a **$60/mo cap (2× promo)**, ~728 req/mo at your profile. Highest intelligence ever on Go at the time, Vals #1 of 41 (68.9%), AutomationBench #1 (51.3%). ⚠️ The Oct 16 Contributor/training terms were **superseded on Oct 25** — the current SKU is ZDR/not trained.
- **Step 5 Preview free → paid:** now $1.00/$2.70/$0.10 with a **$60/mo 4× promo**; its free window ended Oct ~15 and **open weights shipped Oct 15** (BF16 + FP8). On Oct 25 the promo ended and the cap returned to **$15**.
- **Beam Free (Oct 12, limited time/regions):** Reflection AI's 501B/23B MoE, text-only, Apache-2.0 weights, AA 30 — 30-day retention, **no training**. Regional exclusions do **not** include India.
- **Zen free-model explosion:** **DeepSeek V4.1 Flash Free** (AA 39) and **GLM-5.3-Flash Free** (AA 42) — both **zero-retention, no training** — plus stealth models. The free floor became stronger than the paid workhorse tier was in September.
- **Roster removals:** Grok 4.6, Kimi K2.6, MiniMax M2.7 removed from Go; DeepSeek V4 Flash retired. Go was 29 models then and is 29 now with different composition.
- **Privacy changes:** Go docs list **Grok 4.7 at 30-day retention** (no training); Muse Spark Contributors train; Beam/LL Alpha 30-day; DeepSeek ZDR renewed **through Oct 31**.
- **v2 migration:** this machine moved to v2.0.31 (now v2.1.4). v1 is 1.19.x with explicit 1.x pinning and **session sharing discontinued**.
- **OmO 5.1.34 (Oct 16):** Gemini 4 Argon (high) inserted into `oracle` / `momus` / `plan-reviewer` chains; `omo login/logout/whoami` disabled until accounts open; senpi defaults Opus 5.5 / MiMo V2.6 Pro.

## New: Oct 13 roster refresh (Haiku 5.5, Step 5, cap changes, legacy cleanup)

- **Claude Haiku 5.5 (Oct 7, on Go at $15/mo):** Anthropic's fastest model, 1M ctx, adjustable effort, TB4.0 39.2% at max, OSWorld 2.1 72.4%. The default for explore/subagent/quick slots. 30-day retention.
- **Step 5 Preview Free (Oct 8, on Go free):** StepFun 600B/27B-active MoE, AA 44, DeepSWE 67.7, TB4.0 33.3, open weights Oct 15. The best free coder on Go while the preview lasted.
- **DeepSeek V4.1 Flash $60→$80/mo:** ~25.5k req/mo at your profile; weekly binding eased 83%→62%; monthly cap binds only in crunch months. ZDR renewed through Oct 31 ✅.
- **Space Bunny free→paid** ($0.15/$0.60, $30/mo); removed from Go on Oct 25.
- **Legacy demotion:** DeepSeek V4 Pro / V4 Flash / Vision Exp, GLM-5.2, MiMo-V2.5/Pro, Kimi K2.6 moved out of recommendations into Legacy notes.

## New: Oh My OpenCode, v1 vs v2, plugins, power-ups (Oct 1, 2026 — second wave)

- **Oh My OpenCode is now `oh-my-openagent` (OmO)**: Ultimate (OpenCode plugin), Light (Codex), Native (standalone). Sisyphus orchestrator + background agents + Ralph loops **multiply request volume 3–5×**. On Oct 25 the Go map is: **Kimi K3.1 Pro (max) as primary** (K3.1-specific prompts since 5.1.47), **MiMo-V2.6-Pro** on reasoning slots, Flash tiers on explore/librarian/quick, Grok 4.7 for consults. Three configs in `08`.
- **v1 vs v2**: v2 is a rewrite (shared server, multi-tab, synced clients) but **breaks all v1 plugins, kills LSP runtime, share removed, history migrator gaps**. OmO has no shipped v2 support — **stay on v1.19.4 for OmO Ultimate**; OmO Native 5.1.48 is the safe v2-era path. Full comparison + migration checklist in `09`.
- **Plugins**: sweet spot is 3–6 MCPs (Context7, Playwright scoped, one search MCP, grep.app, ADO, read-only DB). Standouts: OMO, dynamic-context-pruning, notify, wakatime, vibeguard, worktree/multiplexer, morph-fast-apply. Full catalog + stacks in `10`.
- **Your power-ups**: ADO MCP on `azcli` + skill → nightly build-health → browser-ops skill → failure auto-triage → PHI-safe permissions → AGENTS.md sweep → ARI/Kafka/Redis/DI skills → OMO. Full recipes in `11`.

---

## Method (short)

- **Three waves of parallel web-research agents** (roster/benchmarks/value; OmO/v1-v2/plugins/power-ups; then India availability, Go-vs-direct, and plan value) plus vendor docs, billing pages and leaderboards fetched directly. Live docs were re-checked on **Oct 25** for roster, caps, prices, privacy and restricted-model settings.
- **Local calibration:** aggregate token/cost stats were computed from the local OpenCode session database (no session content, no client data). This is what makes the limit math real rather than hand-wavy.
- **Cross-checks:** every crucial number has a source URL; vendor claims are marked vs independent runs; benchmark version/harness caveats are explicit. 🟢 official · 🟡 proxy/partial · 🔴 vendor-only.
- **Privacy:** no client names, no PHI, no session content in this repo. Only aggregate usage numbers.

## Caveats

- Everything is a **snapshot** (Oct 1, 2026; roster/caps/value refreshed **Oct 25**). Model rosters, prices and limits changed ~weekly in Sep–Oct 2026.
- The **local calibration data is still the Sep 15 – Oct 1 history** (primary machine's v1 DB); the Oct 25 v2 DB is a consistency check (8.2k / 1.25k / 153k per request), not a new baseline.
- AA Intelligence Index is **v4.3.2**; Vals is **v2.2**. Older quoted scores are not comparable.
- Vendor benchmarks are self-reported; independent coverage gaps remain (METR/Epoch have almost no Go-model data; K3.1 Pro has no Design Arena/OSWorld entry yet).
- Limits math uses **your** token profile; a lighter user gets several× more requests per cap.
- Data policies change; re-verify before sending client/PHI data. **Oct 25:** Argon is ZDR; Muse Spark Contributor still trains; Grok 4.7 is 30-day retention; DeepSeek ZDR expires **Oct 31, 2026**.
- India verdicts mix official docs (🟢) and community/third-party evidence (🟡). Payment methods and regional availability can change at checkout — use the 2-minute checklist in `14` before paying.
