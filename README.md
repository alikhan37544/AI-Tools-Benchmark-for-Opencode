# AI Tools Benchmark for OpenCode — Go Plan Deep Dive

> **Full refresh: October 1, 2026.** 30 Go models · 18 task categories · every major benchmark source · **calibrated to this machine's real OpenCode usage history**.
> 🌐 **Live site (GitHub Pages): https://alikhan37544.github.io/AI-Tools-Benchmark-for-Opencode/**
> Interactive report: **[opencode-go-analysis.html](./opencode-go-analysis.html)** — searchable, sortable, with charts.

This repo answers six questions with evidence, not vibes:

1. Which models are on OpenCode Go?
2. How good is each one — across benchmarks, independent labs, HuggingFace, and real user feedback?
3. Which model is best for each specific task (backend, frontend, DB, integrations, agentic deploy, git, visual QA, image analysis, planning, hardware/ROM/general intelligence)?
4. How long can you program continuously before limits bite?
5. What is the best intelligence-per-dollar overall and per task?
6. What are the "pay a little more → huge intelligence jump" tiers?

---

## TL;DR — the six answers

### 1. The roster (30 models, Oct 1, 2026)
Grok 4.7/4.6 · GLM-5.3/5.3-Flash/5.2 · GPT 6 Luna, GPT 5.6 Luna · Kimi K3/K2.7 Code/K2.6 · DeepSeek V4.1 Flash/V4 Pro/V4 Flash/V4 Flash Vision Exp · MiMo-V2.6-Pro/Flash, MiMo-V2.5/Pro · MiniMax M3/M2.7 · Qwen3.8 Max/Flash, Qwen3.7 Plus · LongCat-2.0 · Hy4 preview, Hy3 · Muse Spark 1.3/1.2 Contributor · **free:** Space Bunny, LongCat 2.5 Preview.
Plans: **Go $10/mo**, **Go Plus $40/mo**. Per-model dollar caps; 5h = 20% of monthly, weekly = 50%, monthly = 100%. → [Full details](./analysis/01-go-roster-and-limits.md)

### 2. Best models overall
| | Winner | Why |
|---|---|---|
| **Highest intelligence on Go** | **Muse Spark 1.3 Contributor** (AA 48) | Design Arena #1, strong long-context — but trains on your data |
| **Best verified agentic coder** | **Grok 4.6** | SWE-bench 95.6 (Vals), GPQA 95.0, ARC-AGI-2 67.1 |
| **Best premium value** | **MiMo-V2.6-Pro** (AA 46) | #1 open-weight class, $0.13/AA task (15× cheaper than Kimi K3 per task) |
| **Best marathon/1M-context** | **Kimi K3** (AA 44) | SWE-Marathon 42.0, FrontierSWE 81.2, frontend #1, OSWorld 84.8 |
| **Best visual/OS agent** | **Qwen3.8 Max** (AA 45) | **#1 model in the world on OSWorld 86.1**, LMArena Vision #2, SWE-bench Pro 67.7 (best Go) |
| **Best daily driver at volume** | **DeepSeek V4.1 Flash** (AA 39) | 209–232 tok/s, native vision, 19.1k req/mo at your real token profile |
| **Best budget workhorse** | **GLM-5.3-Flash** (AA 42) | AA AutomationBench 60.4% (best Go), MIT, 9.8k req/mo at your profile |
| **Biggest sleeper** | **MiMo-V2.6-Flash** | No AA score yet, near-Pro vendor numbers, 33k req/mo, $0.0018/req |

→ [Full benchmark dossier](./analysis/02-benchmarks.md)

### 3. Best model per task (Go roster)
| Task | Best on Go | Value pick |
|---|---|---|
| Backend / API / refactors | Kimi K3 (marathon) / DeepSeek V4.1 Flash (daily) | DeepSeek V4.1 Flash |
| Frontend / UI | Muse Spark 1.3 | GLM-5.3-Flash |
| Database / SQL | GLM-5.3 (GLM-5.2 lineage won Spider 2.0-Lite) | GLM-5.3-Flash |
| Integrations / auth / webhooks | Kimi K3 / Hy4 preview (Toolathlon 74.1) | DeepSeek V4.1 Flash |
| Agentic terminal / DevOps / git / deploy | Grok 4.6 (verified) / GLM-5.3 (TB4.0 41.9) | GLM-5.3-Flash |
| Long-horizon autonomy | Kimi K3 | DeepSeek V4 Flash (LHTB #1) |
| Visual QA / Playwright | **Qwen3.8 Max (OSWorld #1 worldwide)** | Qwen3.8 Flash |
| Image / OCR / Arabic docs | Qwen3.8 Max | Qwen3.8 Flash / DeepSeek Vision |
| Planning / architecture | **Grok 4.6** | MiMo-V2.6-Pro |
| Debugging / RCA | Kimi K3 (honesty) / Grok 4.7 (edge cases) | DeepSeek V4.1 Flash |
| Long context (huge repos/logs) | DeepSeek V4 Pro (MRCR-1M 83.5) | DeepSeek V4.1 Flash |
| Bulk edits / tests / explore | MiMo-V2.6-Flash | MiMo-V2.6-Flash |
| General intelligence / research | Muse Spark 1.3 (48) | GLM-5.3-Flash |
| Data / ML notebooks | MiniMax M2.7 (MLE), Kimi K3 | DeepSeek V4.1 Flash |
| **Systems: overclock / ROM / drivers / homelab** | Grok 4.6 / Kimi K3 (no dedicated bench; reasoning + tool use) | DeepSeek V4.1 Flash + frontier for brick-risk steps |
| Voicebot / realtime telephony | DeepSeek V4.1 Flash (integration/debug loops) | MiMo-V2.6-Flash |

→ [Full task playbook + routing for this machine](./analysis/03-task-playbook.md)

### 4. How long can you program continuously?
Measured from **your actual history** (12,973 requests on DeepSeek V4.1 Flash @ max, Sep 15–Oct 1):

| Window | Your peak | Cap | Used |
|---|---|---|---|
| 5-hour rolling | $5.99 | $12 | **50%** ← why it "feels unlimited" |
| 7-day rolling | $24.77 | $30 | **83%** ⚠️ |
| Monthly pace | ~$45–73/mo | $60 | **on track to hit the cap day 22–26** |

At your token profile (7.8k input + 146k cache + 1.1k output per request), DeepSeek V4.1 Flash gives **~19,100 requests/month**, not the 130,000 the docs estimate (your requests are 5–6× heavier than their assumed profile). Premium models are **minutes per 5h and 1–3 tasks/week**: Kimi K3 ~179 req/mo, Grok 4.6 ~158, Qwen3.8 Max ~256, GLM-5.3 ~279.
**Cheat code:** DeepSeek is 50% off off-peak (after ~15:30 IST + weekends) → doubles your effective cap.
→ [Full limits & burn-rate analysis](./analysis/04-limits-and-burn-rate.md)

### 5. Intelligence per dollar
| Metric | Winner |
|---|---|
| AA points per limit-$ | **Muse Spark 1.3 Contributor — 37,152** (privacy caveat) |
| Best sustainable | **DeepSeek V4.1 Flash — 12,426 pts/$** and 19.1k req/mo |
| Best premium | **MiMo-V2.6-Pro — 9,428 pts/$**, AA 46 |
| Best quality/capacity balance | **GLM-5.3-Flash** (AA 42, 9.8k req/mo) |
| Worst value on Go | Grok 4.7 (483 pts/$), Grok 4.6 (462), Kimi K3 (526) — capacities of 158–179 req/mo |

The jump from 39 (DeepSeek) to 44–46 (Kimi K3/Grok/MiMo Pro) costs **17–31× per request and 99% of capacity** for **+5–7 AA**. Going to Muse Spark is the exception: **+9 AA, cheaper per request, more capacity** (if the data policy is OK). Beyond Go, Claude Opus 5.5 is **AA 58 (+19)**, for must-not-fail work only.
→ [Full value & tier analysis](./analysis/05-intelligence-per-dollar.md)

### 6. Tier structure ("pay more for a jump")
| Tier | Models | Verdict |
|---|---|---|
| **T0 Free** | Space Bunny, LongCat 2.5 Preview | Unlimited until they end; non-sensitive only |
| **T1 Workhorses** | DeepSeek V4.1 Flash, MiMo-V2.6-Flash, GLM-5.3-Flash, Muse Spark*, MiMo-V2.5, LongCat-2.0, Hy3, Qwen3.8 Flash | Drive 90% of work here. *Muse trains on data |
| **T2 Premium $15–30** | MiMo-V2.6-Pro, GPT 6 Luna, DS V4 Pro, Vision Exp | Best quality/call: planning, hard debug, OCR verify |
| **T3 Rations $15** | Grok 4.6/4.7, Kimi K3, GLM-5.3, Qwen3.8 Max | 1–3 big tasks/week each; the hard 5% |
| **T4 Beyond Go** | Opus 5.5 (58), GPT-6 Astra/Fable 5.1 (53) | Copilot/Zen; must-not-fail only |

**Go Plus ($40):** 2×–8× limits. Great for GLM-5.3 (8×) and $15 rations (4×); poor for DeepSeek V4.1 Flash/MiMo-Flash/Muse Spark (2×). For a DeepSeek-heavy workflow, **Go + $30 Zen overflow beats Go Plus**.

---

## The recommended setup

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "model": "opencode-go/deepseek-v4.1-flash",
  "small_model": "opencode-go/mimo-v2.6-flash",
  "agent": {
    "plan":    { "model": "opencode-go/grok-4.6" },
    "explore": { "model": "opencode-go/mimo-v2.6-flash" },
    "build":   { "model": "opencode-go/deepseek-v4.1-flash" }
  }
}
```

Escalate per task: `Kimi K3` (marathon/bug) · `Qwen3.8 Max` (visual QA) · `Muse Spark 1.3` (design/general, non-client) · `MiMo-V2.6-Pro` (hard reasoning, cheap) · Copilot `Opus 5.5` (must-not-fail).
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
| [analysis/07-recommended-config.md](./analysis/07-recommended-config.md) | Copy-paste `opencode.json` configs, role matrix, workflow patterns |
| [analysis/08-oh-my-opencode.md](./analysis/08-oh-my-opencode.md) | Oh My OpenCode guide: agents, categories, hooks, loops + **Go model map for very heavy work** |
| [analysis/09-opencode-v1-vs-v2.md](./analysis/09-opencode-v1-vs-v2.md) | v1 vs v2 differences, pros/cons, migration checklist, OMO compatibility |
| [analysis/10-plugins-and-stacks.md](./analysis/10-plugins-and-stacks.md) | Best plugins, ranked MCPs, skills/rules, 3 copy-paste stacks, anti-recommendations |
| [analysis/11-amazing-additions.md](./analysis/11-amazing-additions.md) | Personalized power-ups: Azure autonomy, browser/RPA, memory, safety, scheduler, voicebot, OCR |
| [RESEARCH-GUIDE.md](./RESEARCH-GUIDE.md) | How this was researched and how to update it |

---

## New: Oh My OpenCode, v1 vs v2, plugins, power-ups (Oct 1, 2026 — second wave)

- **Oh My OpenCode is now `oh-my-openagent` (OmO)**: Ultimate (OpenCode plugin), Light (Codex), Native (standalone). Sisyphus orchestrator + background agents + Ralph loops **multiply request volume 3–5×** — so the Go map is: **Kimi K3 (max) as primary** (only validated Go orchestrator), **MiMo-V2.6-Pro** on reasoning slots (AA 46), Flash tiers on explore/librarian/quick, Grok 4.7 for consults, DeepSeek Vision for `look_at`. Two full configs (max-intelligence + sustainable) in `08`.
- **v1 vs v2**: v2 is a rewrite (shared server, multi-tab, synced clients) but **breaks all v1 plugins, kills LSP runtime, share unimplemented, history migrator gaps**. OMO has no official v2 support yet — **stay on v1.18.x for production OMO**; OmO Native is the safe v2-era path. Full comparison + migration checklist in `09`.
- **Plugins**: sweet spot is 3–6 MCPs (Context7, Playwright scoped, one search MCP, grep.app, ADO, read-only DB). Standouts: OMO, dynamic-context-pruning, notify, wakatime, vibeguard, worktree/multiplexer, morph-fast-apply. Full catalog + stacks in `10`.
- **Your power-ups** (ranked by wow-per-hour): ADO MCP on `azcli` + skill → nightly build-health → browser-ops skill → failure auto-triage → PHI-safe permissions → AGENTS.md sweep → ARI/Kafka/Redis/DI skills → OMO. Full recipes in `11`.

---

## Method (short)

- **Two waves of parallel web-research agents** (first: roster, per-vendor benchmarks, independent evaluators, task-specific, value/community, project scan; second: Oh My OpenCode, v1-vs-v2, plugins/tooling, Azure autonomy, browser/RPA, memory/safety/telecom/OCR) + vendor docs and leaderboards fetched directly.
- **Local calibration:** aggregate token/cost stats were computed from the local OpenCode session database (no session content, no client data). This is what makes the limit math real rather than hand-wavy.
- **Cross-checks:** every crucial number has a source URL; vendor claims are marked vs independent runs; benchmark version/harness caveats are explicit.
- **Privacy:** no client names, no PHI, no session content in this repo. Only aggregate usage numbers.

## Caveats

- Everything is a **snapshot** (Oct 1, 2026). Model rosters, prices and limits changed ~weekly in Sep 2026.
- AA Intelligence Index re-baselined to v4.3.2 in late Sep; older quoted scores are not comparable.
- Vendor benchmarks are self-reported; independent coverage gaps remain (METR/Epoch have almost no Go-model data).
- Limits math uses **your** token profile; a lighter user gets several× more requests per cap.
- Data policies change; re-verify before sending client/PHI data.
