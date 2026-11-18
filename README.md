# AI Tools Benchmark for OpenCode — Go Plan Deep Dive

> **Full refresh: October 1, 2026 · roster refreshes: October 13, 16, 25 and November 17, 2026.** 32 Go models · 18 task categories · every major benchmark source · **calibrated to this machine's real OpenCode usage history**.
> 🌐 **Live site (GitHub Pages): https://alikhan37544.github.io/AI-Tools-Benchmark-for-Opencode/**
> Interactive report: **[opencode-go-analysis.html](./opencode-go-analysis.html)** — searchable, sortable, with charts.
>
> **🆕 Nov 18 (latest):** **usage re-pulled: 35,013 req / $73.41 / 30d** (DS $0.00210/req at 28.7% peak → **47,619 req/mo**; Nov 17 = new #1 day 9,320/$18.70; meter **84.0%** $50.38/$60, resets Nov 24; frisky access ended Oct 31) · **GLM-5.3 caps $200/$400/$205 (20×, 3,331 req/mo — bulk AA-32 lane)** · **Argon retention corrected to 55-day** (was 0-day; K3.1 Pro is the privacy-safe escalation) · **M3.1 Flash Free deprecated Nov 17** (free twins = DS + GLM only) · frontier **GPT-6.2 Astra 62** (new #2) · Vals leader **Fable 5.2 71.31%** (verifiable, incl. Qwen4 Max 63.20%, DS 61.26%, GLM-5.3 59.85%) · tooling **OpenCode v2.3.2 / v1.19.6** (this machine still v2.3.0 — upgrade pending) · OmO 5.1.75, dual-host PR #9391 still open.
> **🆕 Nov 17 (history, incl. evening source re-verification):** **OpenCode v2.3.0** (background subagents, `/goal`, image gen, worktree runs, Claude Code provider; v1 = 1.19.5) · **OmO 5.1.75** (accounts + remote sessions live) · roster **29 → 34 → 32 models** (MiMo-V2.5/-Pro dropped Nov 17): +**Qwen4 Max** (AA 43, new board), +**Hy4** GA, +**Iceman Contributor Free** (trains), +**LongCat 2.5 Free** (back), +**Hy4 flash Free** · **DeepSeek V4.1 Flash cap $80 → $100** (was 52,632 measured req/mo on the Nov 17 blend, 10× multiplier; catalog SKU is literally “DeepSeek V4.1 Flash 1017” — the 1017 checkpoint is the served product) · **limit mechanics corrected: the paid models share one allowance** (per-model limits = solo-usage coverage; mixing shares proportionally — see [01 §2](./analysis/01-go-roster-and-limits.md)) · request estimates now Console-published (Argon 566/5h) · third zero-retention free twin on Zen: **MiniMax M3.1 Flash Free** (deprecated Nov 17 — history) · Argon 50% discount **ends Nov 30** · AA re-baselined to **v5.0.1** (Fable 5.1 scored: 50 xhigh/49 max; Fable 5.2 leads at 65) — repo re-based in the **Nov 17 late refresh** below (old v4.3.2 scores kept as labeled history).
> **Oct 25:** +**Kimi K3.1 Pro** (AA 55.1 (v4.3.2) — the highest intelligence ever on Go) · +**MiniMax M3.1 Flash** (AA 43 (v4.3.2) at $0.22/AA task — the new paid value anchor) · **Gemini 4 Argon is now ZDR/not trained** (the old Contributor warning is withdrawn) · **Step 5 back to a $15 cap** (4× promo ended) · **Space Bunny / LongCat 2.5 Preview Free removed** · OpenCode v2.1.4 / OmO 5.1.48. **Analyses: [India availability](./analysis/14-india-availability.md) · [Go vs direct](./analysis/12-opencode-vs-direct.md) · [best-value plans](./analysis/13-best-value-coding-plans.md).**
> **Oct 16:** +Gemini 4 Argon (AA 53 (v4.3.2)) · Step 5 free→paid · +Beam Free · Zen free twins (DeepSeek/GLM) · Grok 4.6 / Kimi K2.6 / MiniMax M2.7 removed · v2.0.31 migration.
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

### 1. The roster (32 models, Nov 17, 2026 — 29 → 34 → 32: MiMo-V2.5/-Pro dropped Nov 17)
**Qwen4 Max (NEW)** · Kimi K3.1 Pro · Gemini 4 Argon · Grok 4.7 · GLM-5.3/5.3-Flash/5.2 · GPT 6 Luna, GPT 5.6 Luna · Claude Haiku 5.5 · Kimi K3/K2.7 Code · DeepSeek V4.1 Flash/V4 Pro · MiMo-V2.6-Pro/Flash · MiniMax M3.1 Flash, MiniMax M3 · Qwen3.8 Max/Flash, Qwen3.7 Plus · LongCat-2.0 · **Hy4 (NEW)**, Hy4 preview, Hy3 · Muse Spark 1.3/1.2 Contributor · Step 5 Preview (paid) · **free:** Beam Free, **LongCat 2.5 Free (back)**, **Hy4 flash Free (NEW)**, **Iceman Contributor Free (NEW — trains)**. **Removed since Oct 1:** Space Bunny, Grok 4.6, Kimi K2.6, MiniMax M2.7, DS V4 Flash, MiMo-V2.5/-Pro (Nov 17).
Plans: **Go $10/mo**, **Go Plus $40/mo**, **Go Teams $20/member/mo** (2-member minimum — $40/mo; +$5 per model cap). **One shared allowance across the paid models**, normalized per model (each limit = solo-usage coverage); 5h = 20% of monthly, weekly = 50%, monthly = 100% of the shared allowance. → [Full details](./analysis/01-go-roster-and-limits.md)

### 2. Best models overall
| | Winner | Why |
|---|---|---|
| **Highest intelligence on Go** | **Gemini 4 Argon** (AA 50) | The **v5.0.1 ceiling** — K3.1 Pro (46) is now #2, Qwen4 Max (43) #3; 1M ctx, vision, 862 measured req/mo, **55-day retention (corrected Nov 18)** |
| **Best independent agentic coder** | **Gemini 4 Argon** (AA 50) | Vals v2.2 launch **69.24% (#3 overall at launch, #1 Go)**, 862 measured req/mo, **55-day retention (corrected Nov 18 — not ZDR)** |
| **Best privacy-safe intelligence** | **Kimi K3.1 Pro** (AA 46, 0-day, not trained) / **MiMo-V2.6-Pro** (AA 30) / **Grok 4.7** (AA 35, 30-day) | K3.1 Pro is the highest-AA 0-day model on Go (191 req/mo); MiMo-Pro is the cheapest of the ZDR reasoning tier |
| **Best marathon / 1M-context** | **Kimi K3.1 Pro** (AA 46) | K3 lineage: SWE-Marathon 42.0, FrontierSWE 81.2, OSWorld 84.8; 3.1 adds 1M ctx + vision |
| **Best visual/OS agent** | **Qwen3.8 Max** (AA 34, 0902 snapshot) | **#1 model in the world on OSWorld 86.1**; LMArena Vision **#9** (corrected Oct 25) |
| **Best daily driver at volume** | **DeepSeek V4.1 Flash** (AA 33 — the catalog SKU is literally “DeepSeek V4.1 Flash 1017”, so the 1017 checkpoint is the served product) | 177.3 tok/s, native vision, **47,619 measured req/mo** ($100 cap; **$0.00210/req** Nov 18 pull), **10× multiplier** — free twin on Zen |
| **Best paid value workhorse** | **MiniMax M3.1 Flash** (AA 29) | 5,025 measured req/mo at $0.0017/req plan-effective; 141.3 tok/s, 1.25s TTFT, **7,286 pts/$** |
| **Best free coder** | **GLM-5.3-Flash Free** (AA 28, zero-retention) | AA 28 at $0/req; DeepSeek V4.1 Flash Free is the high-capacity runner-up |
| **Best free agentic bulk** | **Beam Free** (AA 18) | Reflection AI 501B/23B MoE, Apache-2.0 weights; 30-day retention, no training |
| **Best subagent / quick-task** | **Claude Haiku 5.5** (AA 36) | Fastest Claude, TB4.0 35.35% max (earlier pass), 1M ctx; the strongest cheap-lab model on v5.0.1 |

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
| Planning / architecture | **Kimi K3.1 Pro (46)** / Gemini 4 Argon (50, 55-day) | MiniMax M3.1 Flash |
| Debugging / RCA | Kimi K3.1 Pro / Grok 4.7 (edge cases) | GLM-5.3-Flash Free |
| Long context (huge repos/logs) | Kimi K3.1 Pro (1M) / DeepSeek V4.1 Flash (cheapest cache) | DeepSeek V4.1 Flash Free |
| Bulk edits / tests / explore | MiniMax M3.1 Flash / Claude Haiku 5.5 | GLM-5.3-Flash Free (AA 28 at $0) |
| General intelligence / research | Gemini 4 Argon (50) / Kimi K3.1 Pro (46) | MiniMax M3.1 Flash |
| Data / ML notebooks | Kimi K3.1 Pro / MiniMax M3.1 Flash | DeepSeek V4.1 Flash |
| **Systems: overclock / ROM / drivers / homelab** | Kimi K3.1 Pro / Grok 4.7 | DeepSeek V4.1 Flash + frontier for brick-risk steps |
| Voicebot / realtime telephony | DeepSeek V4.1 Flash (integration/debug loops) | MiMo-V2.6-Flash |

→ [Full task playbook + routing for this machine](./analysis/03-task-playbook.md)

### 4. How long can you program continuously?
Measured from **your actual history** (12,973 requests on DeepSeek V4.1 Flash @ max, Sep 15–Oct 1). The fresh v2 DB (Oct 25: 8.2k in / 1.25k out / 153k cache per request) is within ~5% of the frozen profile:

| Window | Your peak | Cap | Used |
|---|---|---|---|
| 5-hour rolling | $5.99 | $20 | **30%** ← why it "feels unlimited" |
| 7-day rolling | $24.77 | $50 | **50%** |
| Monthly pace | ~$45–73/mo | $100 | **under cap except crunch months** |

At the **measured fleet profile** (3,457 input + 198,806 cache + 799 output per request; provider-side logs, both Go accounts, 35,013 requests/30d — Nov 18 pull; the frozen heavy mix 7.8k/146k/1.1k remains the conservative secondary), DeepSeek V4.1 Flash gives **~47,619 requests/month** (32,258 at the heavy mix; $0.00210/req), not the ~216,500 the Console estimate implies (43,300/5h, week/month derived ×2.5/×5 — the docs no longer publish the tables, they defer to console/go#pricing & console/go#limits as of Nov 17; your requests are several× heavier). Premium models at the measured profile: **Kimi K3.1 Pro ~191/mo**, Kimi K3 ~155, Grok 4.7 ~135, Qwen3.8 Max ~203, **GLM-5.3 ~3,331 (20× — bulk lane since the $200 cap)**, **Gemini 4 Argon ~862 (55-day retention)**, **MiniMax M3.1 Flash ~5,025** (the only premium-tier model with real daily capacity).
**Cheat code:** DeepSeek is 50% off off-peak (after ~15:30 IST + weekends) → doubles your effective cap. **Free cheat code 2.0:** **DeepSeek V4.1 Flash Free** and **GLM-5.3-Flash Free** are zero-retention and cost nothing — an unlimited floor after caps bind. (MiniMax M3.1 Flash Free was deprecated Nov 17 — past-tense.)
→ [Full limits & burn-rate analysis](./analysis/04-limits-and-burn-rate.md)

### 5. Intelligence per dollar
| Metric | Winner |
|---|---|
| AA points per limit-$ | **Muse Spark 1.3 Contributor — 40,969** (privacy caveat: trains) |
| Best free (zero-retention) | **GLM-5.3-Flash Free — AA 28 at $0/req**, then DeepSeek V4.1 Flash Free |
| Best sustainable paid | **DeepSeek V4.1 Flash — 15,714 pts/$** (AA 33 — the served 1017 checkpoint; catalog SKU “DeepSeek V4.1 Flash 1017”), **47,619 measured req/mo** |
| Best paid quality/value | **MiniMax M3.1 Flash — 7,286 pts/$**, AA 29, 5,025 measured req/mo |
| Best premium capacity | **Gemini 4 Argon — 1,437 pts/$**, AA 50, 862 measured req/mo, **55-day retention** |
| Highest intelligence on Go | **Gemini 4 Argon — AA 50**; K3.1 Pro #2 at 46 (585 pts/$, 191 req/mo) |
| Worst value on Go | Grok 4.7 (315 pts/$), Kimi K3 (175) — ~135–155 req/mo |

*(All AA = v5.0.1; pts/$ = AA ÷ measured-profile $/req. The old v4.3.2 figures are kept as labeled history in [05](./analysis/05-intelligence-per-dollar.md).)*

**The cheap tier is compressed:** Step 5 / M3.1 Flash / Qwen3.8 Flash = 29, GLM-5.3-Flash / GPT 6 Luna = 28, MiMo-Flash = 27 — within ±3 pts = measurement noise. Pick on capacity/price/speed/privacy, not AA. Above that, the jump from DeepSeek (33) to the 35–46 tier (Hy4 GA / Grok / Haiku / Qwen4 Max / K3.1 Pro) costs **≈1.6–53× per request**. The two big exceptions: **Argon** (+17 AA over DeepSeek, 862 req/mo, 55-day retention) and the **free twins** (AA 27–29-tier models at $0). Beyond Go, Claude Fable 5.2 leads the board at **65** (Vals 71.31%) with **GPT-6.2 Astra 62** as the new #2, and Claude Opus 5.5 is **AA 59** — for must-not-fail work only.
→ [Full value & tier analysis](./analysis/05-intelligence-per-dollar.md)

### 6. Tier structure ("pay more for a jump")
| Tier | Models | Verdict |
|---|---|---|
| **T0 Free** | **GLM-5.3-Flash Free, DeepSeek V4.1 Flash Free (both zero-retention)**, Beam Free, Flint 40B (may train), MiMo-Flash Free, Nemotron free, Big Pickle | Unlimited-ish while windows last; only the two zero-retention twins can carry real work |
| **T1 Workhorses** | DeepSeek V4.1 Flash, MiMo-V2.6-Flash, **MiniMax M3.1 Flash**, **GLM-5.3 ($200 cap, 20× — bulk AA-32 lane)**, GLM-5.3-Flash, Muse Spark*, LongCat-2.0, Hy3, Qwen3.8 Flash, Claude Haiku 5.5, Step 5 ($15) | Drive 90% of work here. *Muse trains on data |
| **T2 Premium $15–30** | MiMo-V2.6-Pro, **Gemini 4 Argon ($30, 55-day)**, GPT 6 Luna, GPT 5.6 Luna, Hy4 preview | Best quality/call: planning (non-client), hard debug, OCR verify |
| **T3 Rations $15** | **Kimi K3.1 Pro (46, privacy-safe)**, Kimi K3, Qwen3.8 Max, Grok 4.7 | 1–5 big tasks/week each; the hard 5% |
| **T4 Beyond Go** | Claude Fable 5.2 (65, board leader, Vals 71.31%), **GPT-6.2 Astra (62, new #2)**, Opus 5.5 (59), GPT-6 Astra (57, earlier), Muse Wonder Full (50) | Copilot/Zen; must-not-fail only |

**Go Plus ($40):** 2×–8× limits (GLM-5.3 now 2× at $200→$400). Great for the $15 rations (4×), Argon ($30→$120), M3.1 Flash ($20→$80); decent for DeepSeek V4.1 Flash (2×, $100→$200); poor for MiMo-Flash/Muse Spark (2×). **Go Teams ($20/member, 2-member minimum — $40/mo; the second seat covers the next member at no extra charge)** just adds $5 per model cap per member (Extra Usage on by default). For a DeepSeek-heavy workflow, **Go + $30 Zen overflow beats Go Plus**.

### 7. Go vs going direct
Go's per-token prices are essentially the **same as direct** for almost every model. What $10 buys is **one shared allowance with per-model normalization** — each model's $15–$200 limit is **solo-usage coverage** (a 1.5×–20× multiplier vs the $10 price: 20× = solo GLM-5.3 coverage, 10× = solo DeepSeek coverage), and mixing models draws from the same pool proportionally — the pools are **not** additive. **Go wins** when your usage concentrates on a high-multiplier lane (GLM-5.3 20×, DeepSeek 10×, MiMo-Flash/GLM-Flash/Hy4 GA 6×); **direct or a specialist plan wins** below the single-model break-even or when you need provider features. Break-even at the measured profile: **K3.1 Pro 127 req/mo · Argon 287 · GLM-5.3 167 · Step 5 392 · Grok 90 · M3.1 Flash 2,513 · DeepSeek 4,762**. → [Full per-model break-even](./analysis/12-opencode-vs-direct.md)

### 8. India availability — and the best-value plans
**OpenCode Go is the only plan with documented UPI**, no phone gate, and 32 models behind one key — the clear India-first buy. **StepFun Step Plan** is the raw-value wildcard (verify credits), **Z.ai Lite** the GLM second-pool play (Go's $200/20× cap leads), **Xiaomi Lite** the cheap MiMo entry, **Kimi Code** the K3.1 Pro subscription, **MiniMax M Plan** the opaque one. **Alibaba Token Plan (Singapore-only) and Meta Muse Code (US-first) are blocked from India.** → [India matrix](./analysis/14-india-availability.md) · [Best-value plan ranking](./analysis/13-best-value-coding-plans.md)

| # | Plan | Price | Req/mo, measured profile (verified model) | India |
|---|---|---|---|---|
| 1 | **OpenCode Go** | **$10** | 191 K3.1 Pro · 862 Argon · 5,025 M3.1 Flash · 3,331 GLM-5.3 · **47,619** DeepSeek | 🟢 **UPI** |
| 2 | StepFun Step Plan Pro | $29 | ~45,000 Step 5 *if credit math holds* | 🟢 Stripe |
| 3 | Z.ai GLM Coding Plan Lite | $18 | 1,319 GLM-5.3 peak / 2,639 off-peak | 🟢 Card/PayPal |
| 4 | Xiaomi MiMo Token Plan Lite | $6 | 3,173 Flash / 1,218 Pro | 🟢 Overseas email + Waffo |
| 5 | Kimi Code Plus | $19 | Opaque (K3.1 Pro included) | 🟢/🟡 Card |
| 6 | MiniMax M Plan Go | $22 | Opaque (1×/3×/7.5×) | 🟡 Stripe |
| — | Alibaba Token Plan | $6–68 | — | 🔴 Blocked |
| — | Meta Muse Code | $5–200 | — | 🔴 Blocked |

*Go figures are measured-profile capacity (provider-side logs); competitor plan figures are heavy-mix credit-math estimates from [13](./analysis/13-best-value-coding-plans.md) — compare across rows only as an approximation.*

---

## The recommended setup

```jsonc
// OpenCode v2.3.2 (this machine still runs v2.3.0 — upgrade pending). The same model IDs work on v1.19.6.
{
  "$schema": "https://opencode.ai/config.json",
  "model": "opencode-go/deepseek-v4.1-flash",
  "small_model": "opencode-go/mimo-v2.6-flash",
  "agent": {
    "plan":    { "model": "opencode-go/gemini-4-argon" },    // 55-day retention — non-client only; or kimi-k3.1-pro for the 1M-ctx marathon lane (AA 46)
    "explore": { "model": "opencode-go/claude-haiku-5-5" },  // free lane alt: opencode/glm-5.3-flash-free
    "build":   { "model": "opencode-go/deepseek-v4.1-flash" },
    "value":   { "model": "opencode-go/minimax-m3.1-flash" }
  }
}
```

**India settings:** pay Go/Plus with **UPI** (card/Link/Alipay/WeChat also listed; top-ups add 4.6% + $0.31). In Go's model settings set **DeepSeek → Regions = Global** (the default allowed regions are Europe & US). Enable **"Allow paid endpoints that train on request data"** only for Muse Spark on non-client work — leave it off everywhere else.

Free-tier routing note: `opencode/deepseek-v4.1-flash-free` and `opencode/glm-5.3-flash-free` are zero-retention free models that keep working after Go limits — use them as the bulk/free floor. (MiniMax M3.1 Flash Free was deprecated Nov 17.)

Escalate per task: `Kimi K3.1 Pro` (hardest 5%, privacy-safe) · `Qwen3.8 Max` (visual QA) · `Gemini 4 Argon` (planning/agentic non-client work, 55-day retention) · `GLM-5.3` (bulk AA-32 lane, 20×) · `Muse Spark 1.3` (design/general, non-client) · `MiMo-V2.6-Pro` (hard reasoning, cheap) · Copilot `Opus 5.5` / `GPT-6.2 Astra` (must-not-fail).
→ [Full configs + workflow](./analysis/07-recommended-config.md)

---

## Files

| File | Contents |
|---|---|
| **[opencode-go-analysis.html](./opencode-go-analysis.html)** | Interactive single-page report: searchable/sortable tables, charts, all tiers (start here) |
| [analysis/01-go-roster-and-limits.md](./analysis/01-go-roster-and-limits.md) | Roster, plans, exact pricing/limit mechanics, free models, roster history |
| [analysis/02-benchmarks.md](./analysis/02-benchmarks.md) | Every model's benchmarks (AA v5.0.1, SWE-bench, Terminal-Bench, OSWorld, LMArena, MMLU/MLE…) with sources and confidence ratings |
| [analysis/03-task-playbook.md](./analysis/03-task-playbook.md) | Best model per task + personalized routing for this machine's projects, privacy and contract constraints |
| [analysis/04-limits-and-burn-rate.md](./analysis/04-limits-and-burn-rate.md) | Your measured usage, per-model capacity at your token profile, continuous-hours math, off-peak strategy, Go Plus math |
| [analysis/05-intelligence-per-dollar.md](./analysis/05-intelligence-per-dollar.md) | Value tables, AA points/$, cognitive throughput, tier structure, jump economics, Go vs BYOK |
| [analysis/06-free-models-and-privacy.md](./analysis/06-free-models-and-privacy.md) | Data policies (training/retention) per route, free models, local LLM options |
| [analysis/07-recommended-config.md](./analysis/07-recommended-config.md) | Copy-paste configs (v2-first, v1 notes), role matrix, workflow patterns |
| [analysis/08-oh-my-opencode.md](./analysis/08-oh-my-opencode.md) | Oh My OpenCode guide: agents, categories, hooks, loops + **Go model map for very heavy work** |
| [analysis/09-opencode-v1-vs-v2.md](./analysis/09-opencode-v1-vs-v2.md) | v1 vs v2 differences, pros/cons, migration checklist, OMO compatibility **(archived)** |
| [analysis/10-plugins-and-stacks.md](./analysis/10-plugins-and-stacks.md) | Best plugins, ranked MCPs, skills/rules, 3 copy-paste stacks, anti-recommendations |
| [analysis/11-amazing-additions.md](./analysis/11-amazing-additions.md) | Personalized power-ups: Azure autonomy, browser/RPA, memory, safety, scheduler, voicebot, OCR |
| **[analysis/12-opencode-vs-direct.md](./analysis/12-opencode-vs-direct.md)** | **NEW — per-model Go vs direct break-even, multipliers, privacy/features** |
| **[analysis/13-best-value-coding-plans.md](./analysis/13-best-value-coding-plans.md)** | **NEW — best-value coding plans ranked, plan math, decision table** |
| **[analysis/14-india-availability.md](./analysis/14-india-availability.md)** | **NEW — India matrix: signup, phone, payment, model access + pre-payment checklist** |
| **[analysis/15-all-token-plans.md](./analysis/15-all-token-plans.md)** | **NEW — every token plan compared (Copilot, Claude, ChatGPT, Gemini, Cursor, Windsurf, Kiro, Chinese + aggregators), best deals ranked** |
| **[analysis/16-cursor-windsurf-ide-plans.md](./analysis/16-cursor-windsurf-ide-plans.md)** | **NEW — Cursor/Windsurf/Kiro/IDE tools deep-dive: pricing, India availability, OpenCode compatibility** |
| [RESEARCH-GUIDE.md](./RESEARCH-GUIDE.md) | How this was researched and how to update it |

---

## New: Nov 18 refresh — usage re-pull, GLM-5.3 caps, Argon 55-day, M3.1 Flash Free deprecated

- **Usage re-pulled (Nov 18): 35,013 requests / $73.41 list / 30d** (both Go accounts; DS $0.00210/req at 28.7% peak → **47,619 req/mo measured**; fleet triple 3,457/799/198,806). **Nov 17 = new #1 day: 9,320 req / $18.70** (beats Nov 9's 6,819/$10.33); Nov 18 partial (2,700/$10.73) is peak-heavy — kept as a separate blend. MTD 31,752/$65.93. **frisky.business.now access ended Oct 31** (cancelAtPeriodEnd/payment_failed) — single active account; billing $25.00 unchanged.
- **Meters (Nov 18): 5h 53.9% ($6.47/$12) · week 62.7% ($18.82/$30) · month 84.0% ($50.38/$60)**, resets Nov 24. Limit still $60 vs docs' $100 — discrepancy persists (meter/MTD-list ratio now 76%; bug anomalyco/opencode#43032).
- **GLM-5.3 caps raised ~13×: Go $200 / Plus $400 / Teams $205** — 3,331 req/mo measured (3,720 heavy), **20× multiplier** (break-even 167, 533 pts/$); console est 198→2,640/5h. Rewritten from "ration / worst value" to bulk AA-32 lane in [05](./analysis/05-intelligence-per-dollar.md) and [12](./analysis/12-opencode-vs-direct.md) (Z.ai Lite demoted to second-pool play).
- **Argon retention corrected to 55-day** (docs/go privacy table + Google-terms footnote; discount unchanged 50% off through Nov 30) — worst retention on the roster; "Argon ZDR" claims corrected everywhere; privacy-safe escalation is **K3.1 Pro (0-day, not trained)**.
- **MiniMax M3.1 Flash Free deprecated Nov 17, 2026** (PAYG deprecated-models table) — free twins are two again (DS + GLM-5.3-Flash); past-tensed everywhere. **/docs/zen/ → 301 → /docs/console/models/** — links replaced.
- **Frontier: GPT-6.2 Astra 62 (max/xhigh) is the new #2 / OpenAI ref** (Astra-57 demoted to history); GPT-6.2 Sol 57; Muse Ember 36 max / 34 xhigh noted as cheapest 36-pt context. **Vals renders server-side — "(earlier pass)" lifted**: Fable 5.2 **71.31% #1** (new leader), Carbon 70.45%, GPT-6.2 Astra 67.66% #7, Qwen4 Max 63.20% #11, DS 1017 61.26%, GLM-5.3 59.85%, Hy4 59.35%, Grok 58.62%, MiMo-Pro 57.81%, Step 5 54.76%, Haiku 54.31% #16, M3.1 Flash 53.78%, Beam 43.42%, K3.1 Pro 62.52% confirmed.
- **Tooling: OpenCode v2.3.2** (Nov 18: GPT-6.2 prompt caching on Responses routes + webfetch structured-output fix; v2.3.1: timed-out shell → background, background compaction summary, GPT-6.2 models in ChatGPT picker, plugin updates from Settings, comment-on-selection, read/glob/grep/Code-Mode shapes) · **v1.19.6** (Nov 17: v1 offers upgrade to v2.0, sessions/projects kept, v1 plugins need update). This machine still runs v2.3.0 (upgrade pending). OmO still 5.1.75; PR #9391 still open.

## New: Nov 17 late refresh — AA v5.0.1 re-baseline

- **Full AA re-baseline to v5.0.1** (v5.0 went live Oct 27, v5.0.1 Nov 3): the Go ceiling **reversed** — **Gemini 4 Argon 50** is now #1, **Kimi K3.1 Pro 46** #2, **Qwen4 Max 43** #3 — and the cheap tier compressed to **27–29** (Step 5 / M3.1 Flash / Qwen3.8 Flash 29, GLM-5.3-Flash / GPT 6 Luna 28, MiMo-Flash 27 = measurement noise). Old v4.3.2 scores are **kept as labeled history** (retired scale, never mixed in one comparison).
- **Value/capacity math re-based to the measured profile** from provider-side logs (**both Go accounts, all machines; history: 24,160 requests/30d in the Nov 17 pull — superseded Nov 18: 35,013 requests, 3,457 in / 799 out+reasoning / 198,806 cache read per request**). Headline: **DeepSeek V4.1 Flash = 47,619 measured req/mo at the 10× multiplier** (32,258 at the frozen heavy mix — kept as the conservative secondary).
- **Hy4 GA vs Hy4 preview split:** they are **separate SKUs** at identical token prices ($0.834/$2.501/$0.042) — GA carries the $60 cap (~5,088 measured req/mo on the Nov 17 basis; **4,535 on the Nov 18 basis**), preview $30 (~2,544 then; **2,268 now**).
- **Go Teams documented:** **$20/member/mo, 2-member minimum ($40/month)** — the second seat covers the next member at no extra charge; per-member limits, **+$5 on every model cap**, **Extra Usage on by default**.
- **Meter discrepancy flagged, not resolved:** the console meter shows a **$60** monthly limit while the docs list DeepSeek's cap at **$100** (known meter bug anomalyco/opencode#43032). Plan on the docs' $100; treat the meter as approximate.
- **analysis/09 (v1 vs v2) is archived** — the migration is complete fleet-wide (all machines on v2.3.0+); OmO Ultimate dual-host (PR #9391) was still unmerged as of OmO 5.1.75.
- **Site rebuilt** (`opencode-go-analysis.html`) with the re-based figures.

*Refresh-log entries below this line are dated history: the AA scores they quote are on the scale current at the time (v4.3.2 unless noted) — retired scale, kept for reference, not comparable with the v5.0.1 figures above.*

## New: Nov 17 refresh — OpenCode 2.3.0, roster 29→34 (settled at 32), DeepSeek cap $100, OmO 5.1.75

*(Correction, Nov 17 evening: the roster settled at **32** — `mimo-v2.5` and `mimo-v2.5-pro` were dropped from the live catalog the same day. Dated "34" figures below are as-published history.)*

- **This machine runs OpenCode v2.3.0** (v1 is **1.19.5**): the 2.2.x line landed ten releases in three weeks — **2.2.0** desktop plugins + per-provider cache TTLs, **2.2.1–2.2.2** `/goal` objective loops, `experimental.image_generate`, scheduled prompts, **2.2.3 Claude Code as a provider**, **2.2.4** persistent terminals + `experimental.artifacts` + **Go DeepSeek limits raised (#60625)**, **2.2.5** percentage compaction buffer (`"compaction": {"buffer": "20%"}`), **2.2.6** shared MCP connections + `opencode run -w` worktrees + `--archived`, **2.2.7** GitHub Copilot Auto + `read` negative offset, **2.3.0 background subagents by default** + quieter transcripts + MCP events + `session.fork` hook.
- **Go roster 29 → 34** (settled at **32** the same day — MiMo-V2.5/-Pro dropped Nov 17): +**Qwen4 Max** ($1.50/$4.50/$0.075, $15 cap, ~543 heavy req/mo; **AA 43 on the new v5-era board** — not comparable with our v4.3.2 column), +**Hy4** GA (same price as preview, $60 cap → ~3,900 req/mo), +**Iceman Contributor Free** (**trains on prompts/completions — never on real work**), +**LongCat 2.5 Free** (returned; ZDR/no training, China-hosted, needs Regions=Global), +**Hy4 flash Free** (ZDR/no training). **Step 5 is now listed as “Step 5 Preview”** (same $15 cap).
- **DeepSeek V4.1 Flash cap $80 → $100** (Go Plus $200): **~52,632 measured req/mo** (~32,258 heavy; was 25,484), 5h $16→$20, weekly $40→$50 — now a **10× face-value multiplier**, the biggest on Go. Off-peak doubling implies well past 50k req/mo.
- **Zen free floor upgraded:** +**MiniMax M3.1 Flash Free** — the third **zero-retention, no-training** free twin (AA 43 paid sibling, v4.3.2-era scores below), alongside DeepSeek V4.1 Flash Free (AA 39) and GLM-5.3-Flash Free (AA 42). LongCat 2.5 Free and Hy4 flash Free are ZDR too. New training/retention exceptions: Iceman Free, Inkling 2 Small Free. Crouton/Pulse Alpha Free deprecated.
- **Gemini 4 Argon 50% discount ends Nov 30** (then $4/$20/$0.20 at a $60 cap — same ~728 req/mo, 6× multiplier instead of 3×).
- **DeepSeek ZDR renewed through Nov 30, 2026** (renewed monthly — re-verify).
- **AA re-baselined to v5.0.1** (Claude Fable 5.2 leads at 65). All AA figures in this repo remain **v4.3.2-generation** and are internally comparable; cross-generation scores (Qwen4 Max 43) are flagged and excluded from pts/$. *(Superseded by the Nov 17 late refresh above — the repo is now re-based to v5.0.1, with v4.3.2 kept as labeled history.)*
- **OmO 5.1.75 (Nov 16):** accounts are open — `omo login` signs in and enables **remote sessions/devices** (thread gateway can wake a session on another device), memory sync across devices, computer-use v3 scaffolding (not user-visible yet). **OpenCode v2 dual-host is still not shipped**: PR #9391 remains open (tools/hooks + agents slices now on the branch, parity 13 live / 13 todo); OmO Ultimate stays on v1.19.5, OmO Native 5.1.75 is the v2 path.

## New: Oct 25 refresh — K3.1 Pro + M3.1 Flash, Argon privacy correction, India + plan rankings

- **Kimi K3.1 Pro joined Go (AA 55.1):** the highest intelligence ever listed on Go — 1M context, vision, Vals v2.2 **62.52%**, **$2.11 per AA task**, **$2/$10/$0.20** (cache write $2) and a **$15 cap** → **~269 heavy req/mo** (5h 54, week 134). It is a scalpel, not a driver. Upstream OmO 5.1.47 added K3.1 Pro-specific Sisyphus/Atlas prompts.
- **MiniMax M3.1 Flash joined Go (AA 43):** 112.8 tok/s, 1.35s TTFT, **$0.22/AA task**, 180M verbosity, **$0.15/$0.60/$0.015** with a **$20 cap** → **~4,975 req/mo** and **10,697 pts/$**. It dominates GLM-5.3-Flash on both price and quality at the paid tier.
- **Gemini 4 Argon correction:** the SKU is now plain **`gemini-4-argon`** (not Contributor) at **$2/$10/$0.10**, **$30 cap (50% off through Nov 30)**, ~728 req/mo. Go's privacy table documents **Not used / 0 days** — the Oct 16 "trains on your data" warning is **withdrawn**. Vals v2.2: **69.24%, #3 overall and #1 among Go models** (Sonnet 5.5 70.85 and Opus 5.5 70.18 lead).
- **Step 5 promo ended:** back to a **$15 cap** (~591 req/mo), still AA 44 and open-weight.
- **Roster removals:** **Space Bunny** and **LongCat 2.5 Preview Free** left Go. Go stayed at **29 models** that cycle (it became 34 on Nov 17, settling at 32 the same day).
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
- **Zen free-model explosion:** **DeepSeek V4.1 Flash Free** (AA 39) and **GLM-5.3-Flash Free** (AA 42) — both **zero-retention, no training** (v4.3.2-era scores) — plus stealth models. The free floor became stronger than the paid workhorse tier was in September.
- **Roster removals:** Grok 4.6, Kimi K2.6, MiniMax M2.7 removed from Go; DeepSeek V4 Flash retired. Go was 29 models then and is 32 now (29 → 34 → 32; MiMo-V2.5/-Pro dropped Nov 17) with different composition.
- **Privacy changes:** Go docs list **Grok 4.7 at 30-day retention** (no training); Muse Spark Contributors train; Beam/LL Alpha 30-day; DeepSeek ZDR renewed **through Oct 31**.
- **v2 migration:** this machine moved to v2.0.31 (now v2.1.4). v1 is 1.19.x with explicit 1.x pinning and **session sharing discontinued**.
- **OmO 5.1.34 (Oct 16):** Gemini 4 Argon (high) inserted into `oracle` / `momus` / `plan-reviewer` chains; `omo login/logout/whoami` disabled until accounts open; senpi defaults Opus 5.5 / MiMo V2.6 Pro.

## New: Oct 13 roster refresh (Haiku 5.5, Step 5, cap changes, legacy cleanup)

- **Claude Haiku 5.5 (Oct 7, on Go at $15/mo):** Anthropic's fastest model, 1M ctx, adjustable effort, TB4.0 39.2% at max (later corrected to 35.35% max), OSWorld 2.1 72.4%. The default for explore/subagent/quick slots. 30-day retention.
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

- **Three waves of parallel web-research agents** (roster/benchmarks/value; OmO/v1-v2/plugins/power-ups; then India availability, Go-vs-direct, and plan value) plus vendor docs, billing pages and leaderboards fetched directly. Benchmark data is the **Oct 25** pass **re-based to AA v5.0.1 on Nov 17** (value math re-run on provider-side usage logs); live docs (roster, caps, prices, privacy, restricted-model settings, tooling versions) were re-verified **Nov 17**.
- **Local calibration:** aggregate token/cost stats were computed from the local OpenCode session database (no session content, no client data). This is what makes the limit math real rather than hand-wavy.
- **Cross-checks:** every crucial number has a source URL; vendor claims are marked vs independent runs; benchmark version/harness caveats are explicit. 🟢 official · 🟡 proxy/partial · 🔴 vendor-only.
- **Privacy:** no client names, no PHI, no session content in this repo. Only aggregate usage numbers.

## Caveats

- Everything is a **snapshot** (Oct 1, 2026; roster/caps/tooling/**AA re-based** **Nov 17**, earlier benchmark passes Oct 25). Model rosters, prices and limits changed ~weekly in Sep–Nov 2026.
- The **local calibration data is still the Sep 15 – Oct 1 history** (primary machine's v1 DB); the Oct 25 v2 DB is a consistency check (8.2k / 1.25k / 153k per request), not a new baseline.
- AA Intelligence Index is **v5.0.1** in this repo's headlines (re-based Nov 17, 2026); legacy **v4.3.2** figures are labeled "(retired scale)" and kept as history. Vals is **v2.2**. Scores from different generations are not comparable.
- Vendor benchmarks are self-reported; independent coverage gaps remain (METR/Epoch have almost no Go-model data; K3.1 Pro has no Design Arena/OSWorld entry yet).
- Limits math uses **your** token profile; a lighter user gets several× more requests per cap.
- Data policies change; re-verify before sending client/PHI data. **Nov 18:** Argon is 55-day retained (worst on roster); Muse Spark Contributor **and Iceman Contributor Free** train; Grok 4.7 is 30-day retention; DeepSeek ZDR is renewed monthly (**through Nov 30, 2026**).
- India verdicts mix official docs (🟢) and community/third-party evidence (🟡). Payment methods and regional availability can change at checkout — use the 2-minute checklist in `14` before paying.
