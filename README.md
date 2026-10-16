# AI Tools Benchmark for OpenCode — Go Plan Deep Dive

> **Full refresh: October 1, 2026 · roster refreshes: October 13 and 16, 2026.** 29 Go models · 18 task categories · every major benchmark source · **calibrated to this machine's real OpenCode usage history**.
> 🌐 **Live site (GitHub Pages): https://alikhan37544.github.io/AI-Tools-Benchmark-for-Opencode/**
> Interactive report: **[opencode-go-analysis.html](./opencode-go-analysis.html)** — searchable, sortable, with charts.
>
> **🆕 Oct 16 (latest):** +**Gemini 4 Argon Contributor** (AA 53 — highest intelligence ever on Go, but trains on your data) · **Step 5 Preview free→paid** ($60/mo 4× promo; open weights released Oct 15) · +**Beam Free** (Reflection AI, AA 30) · **Zen free-model explosion: free DeepSeek V4.1 Flash, free GLM-5.3-Flash, Space Bunny Free, LL Alpha stealth** · Grok 4.6 / Kimi K2.6 / MiniMax M2.7 removed from Go · **this machine migrated to OpenCode v2.0.31** (v1 = 1.19.3, sharing discontinued; OmO 5.1.34, v2 dual-host still in review).
> **Oct 13:** +**Claude Haiku 5.5** (fastest Claude, subagent star) and +**Step 5 Preview Free** (AA 44 Kimi-class) · **DeepSeek V4.1 Flash cap $60→$80** · **Space Bunny free→paid** (now also free again on Zen as a stealth).

This repo answers six questions with evidence, not vibes:

1. Which models are on OpenCode Go?
2. How good is each one — across benchmarks, independent labs, HuggingFace, and real user feedback?
3. Which model is best for each specific task (backend, frontend, DB, integrations, agentic deploy, git, visual QA, image analysis, planning, hardware/ROM/general intelligence)?
4. How long can you program continuously before limits bite?
5. What is the best intelligence-per-dollar overall and per task?
6. What are the "pay a little more → huge intelligence jump" tiers?

---

## TL;DR — the six answers

### 1. The roster (29 models, Oct 16, 2026)
Grok 4.7 · GLM-5.3/5.3-Flash/5.2 · GPT 6 Luna, GPT 5.6 Luna · Claude Haiku 5.5 · **Gemini 4 Argon Contributor (NEW)** · Kimi K3/K2.7 Code · DeepSeek V4.1 Flash/V4 Pro · MiMo-V2.6-Pro/Flash, MiMo-V2.5/Pro · MiniMax M3 · Qwen3.8 Max/Flash, Qwen3.7 Plus · LongCat-2.0 · Hy4 preview, Hy3 · Muse Spark 1.3/1.2 Contributor · Space Bunny (paid on Go) · Step 5 Preview (now paid) · **free:** Beam Free (NEW), LongCat 2.5 Preview. Removed from Go: Grok 4.6, Kimi K2.6, MiniMax M2.7, DS V4 Flash.
Plans: **Go $10/mo**, **Go Plus $40/mo**. Per-model dollar caps; 5h = 20% of monthly, weekly = 50%, monthly = 100%. → [Full details](./analysis/01-go-roster-and-limits.md)

### 2. Best models overall
| | Winner | Why |
|---|---|---|
| **Highest intelligence on Go** | **Gemini 4 Argon Contributor** (AA 53) | Vals #1 of 41 (68.9%), AutomationBench #1 (51.3%), lowest hallucination — but Contributor terms train Google on your data |
| **Best privacy-safe intelligence** | **MiMo-V2.6-Pro** (AA 46) / **Grok 4.7** (AA 46) | #1 open-weight class, $0.13/AA task; Grok 4.7 is the strongest verified Grok left on Go (Grok 4.6 removed) |
| **Best verified agentic coder** | **Grok 4.7** / **Kimi K3** | Grok 4.7: SWE-bench-class verified; K3: TB2.1 88.3, SWE-Marathon 42.0, OSWorld 84.8 |
| **Best marathon/1M-context** | **Kimi K3** (AA 44) | SWE-Marathon 42.0, FrontierSWE 81.2, frontend #1, OSWorld 84.8 |
| **Best visual/OS agent** | **Qwen3.8 Max** (AA 45) | **#1 model in the world on OSWorld 86.1**, LMArena Vision #2, SWE-bench Pro 67.7 (best Go) |
| **Best daily driver at volume** | **DeepSeek V4.1 Flash** (AA 39) | 209–232 tok/s, native vision, 25.5k req/mo ($80 cap) — and now a **free twin on Zen** |
| **Best free coder** | **GLM-5.3-Flash Free** (AA 42, zero-retention) | AA 42 at $0/req; the best free-model deal OpenCode has ever had — free DeepSeek V4.1 Flash (AA 39) is the runner-up |
| **Best free agentic bulk** | **Beam Free** (AA 30) | Reflection AI 501B/23B MoE, Apache-2.0 weights; fast, token-efficient; 30-day retention (no training) |
| **Best subagent / quick-task** | **Claude Haiku 5.5** | Fastest Claude, TB4.0 39.2% max, matched Sonnet 5 in Copilot tests |
| **Best budget workhorse** | **DeepSeek V4.1 Flash Free / GLM-5.3-Flash** | Free zero-retention lanes for 90% of work; paid DS for reliability |

→ [Full benchmark dossier](./analysis/02-benchmarks.md)

### 3. Best model per task (Go roster)
| Task | Best on Go | Value pick |
|---|---|---|
| Backend / API / refactors | Kimi K3 (marathon) / DeepSeek V4.1 Flash (daily) | DeepSeek V4.1 Flash (or its **free Zen twin**) |
| Frontend / UI | Muse Spark 1.3 | GLM-5.3-Flash |
| Database / SQL | GLM-5.3 (GLM-5.2 lineage won Spider 2.0-Lite) | GLM-5.3-Flash |
| Integrations / auth / webhooks | Kimi K3 / Hy4 preview (Toolathlon 74.1) | DeepSeek V4.1 Flash |
| Agentic terminal / DevOps / git / deploy | Grok 4.7 (verified) / Gemini 4 Argon* (Vals #1) | GLM-5.3-Flash |
| Long-horizon autonomy | Kimi K3 | Step 5 Preview (now paid, 4× promo) |
| Visual QA / Playwright | **Qwen3.8 Max (OSWorld #1 worldwide)** | Qwen3.8 Flash |
| Image / OCR / Arabic docs | Qwen3.8 Max | Qwen3.8 Flash / DeepSeek V4.1 Flash |
| Planning / architecture | **Gemini 4 Argon*** (AA 53) / Grok 4.7 | MiMo-V2.6-Pro |
| Debugging / RCA | Kimi K3 (honesty) / Grok 4.7 (edge cases) | DeepSeek V4.1 Flash |
| Long context (huge repos/logs) | Kimi K3 (AA-LCR 74.7) / DeepSeek V4.1 Flash (cheapest cache) | DeepSeek V4.1 Flash Free (zero-retention, $0) |
| Bulk edits / tests / explore | MiMo-V2.6-Flash / Claude Haiku 5.5 | GLM-5.3-Flash Free (AA 42 at $0) |
| General intelligence / research | Gemini 4 Argon* (53) / Muse Spark 1.3 (48) | GLM-5.3-Flash Free |
| Data / ML notebooks | MiniMax M3, Kimi K3 | DeepSeek V4.1 Flash |
| **Systems: overclock / ROM / drivers / homelab** | Grok 4.7 / Kimi K3 (no dedicated bench; reasoning + tool use) | DeepSeek V4.1 Flash + frontier for brick-risk steps |
| Voicebot / realtime telephony | DeepSeek V4.1 Flash (integration/debug loops) | MiMo-V2.6-Flash |

\* = trains on your data (Contributor terms) — non-client work only.

→ [Full task playbook + routing for this machine](./analysis/03-task-playbook.md)

### 4. How long can you program continuously?
Measured from **your actual history** (12,973 requests on DeepSeek V4.1 Flash @ max, Sep 15–Oct 1; a fresh v2 DB on Oct 16 shows the same pattern at ~11k in / 2.8k out / 59k cache per request):

| Window | Your peak | Cap | Used |
|---|---|---|---|
| 5-hour rolling | $5.99 | $16 | **37%** ← why it "feels unlimited" |
| 7-day rolling | $24.77 | $40 | **62%** |
| Monthly pace | ~$45–73/mo | $80 | **under cap except crunch months** |

At your token profile (7.8k input + 146k cache + 1.1k output per request), DeepSeek V4.1 Flash gives **~25,500 requests/month**, not the 173,000 the docs estimate (your requests are ~7× heavier). Premium models are **minutes per 5h and 1–3 tasks/week**: Kimi K3 ~179 req/mo, Grok 4.7 ~158, Qwen3.8 Max ~256, GLM-5.3 ~279, **Gemini 4 Argon ~728** (new — the biggest $15-$60-tier capacity on Go).
**Cheat code:** DeepSeek is 50% off off-peak (after ~15:30 IST + weekends) → doubles your effective cap. **Free cheat code 2.0:** the Zen free twins — **DeepSeek V4.1 Flash Free** and **GLM-5.3-Flash Free** — are zero-retention and cost nothing, so your workhorse tier now has an unlimited floor again (Step 5's free window ended; it is now a paid 4×-promo model).
→ [Full limits & burn-rate analysis](./analysis/04-limits-and-burn-rate.md)

### 5. Intelligence per dollar
| Metric | Winner |
|---|---|
| AA points per limit-$ | **Muse Spark 1.3 Contributor — 37,152** (privacy caveat) |
| Best free (zero-retention) | **GLM-5.3-Flash Free — AA 42 at $0/req**, then DeepSeek V4.1 Flash Free (AA 39) |
| Best sustainable paid | **DeepSeek V4.1 Flash — 12,426 pts/$**, 25.5k req/mo |
| Best premium | **MiMo-V2.6-Pro — 9,428 pts/$**, AA 46 |
| Highest intelligence on Go | **Gemini 4 Argon Contributor — AA 53 at 643 pts/$** and ~728 req/mo (trains on data) |
| Worst value on Go | Grok 4.7 (483 pts/$), Kimi K3 (526) — capacities of ~158–179 req/mo |

The jump from 39 (DeepSeek) to 44–46 (Kimi K3/Grok/MiMo Pro) costs **17–31× per request and 99% of capacity** for **+5–7 AA**. Two exceptions: **Gemini 4 Argon** (+14 AA, ~728 req/mo — capacity *higher* than the paid DS tier was in September, but trains on data), and now the **free twins** (AA 39–42 at $0). Beyond Go, Claude Opus 5.5 is **AA 58 (+19)**, for must-not-fail work only.
→ [Full value & tier analysis](./analysis/05-intelligence-per-dollar.md)

### 6. Tier structure ("pay more for a jump")
| Tier | Models | Verdict |
|---|---|---|
| **T0 Free** | **GLM-5.3-Flash Free, DeepSeek V4.1 Flash Free (both zero-retention)**, Beam Free, LongCat 2.5 Preview, Space Bunny Free, LL Alpha | Unlimited-ish while windows last; the zero-retention two can carry real work |
| **T1 Workhorses** | DeepSeek V4.1 Flash, MiMo-V2.6-Flash, GLM-5.3-Flash, Muse Spark*, LongCat-2.0, Hy3, Qwen3.8 Flash, Claude Haiku 5.5, Space Bunny ($30), Step 5 Preview ($60 4×) | Drive 90% of work here. *Muse trains on data |
| **T2 Premium $15–60** | MiMo-V2.6-Pro, Gemini 4 Argon* ($60 2×), GPT 6 Luna, DS V4 Pro, Step 5 Preview | Best quality/call: planning, hard debug, OCR verify |
| **T3 Rations $15** | Grok 4.7, Kimi K3, GLM-5.3, Qwen3.8 Max | 1–3 big tasks/week each; the hard 5% |
| **T4 Beyond Go** | Opus 5.5 (58), GPT-6 Astra/Fable 5.1 (53), Muse Wonder (52–56) | Copilot/Zen; must-not-fail only |

**Go Plus ($40):** 2×–8× limits. Great for GLM-5.3 (8×) and the $15 rations (4×); poor for DeepSeek V4.1 Flash/MiMo-Flash/Muse Spark (2×). For a DeepSeek-heavy workflow, **Go + $30 Zen overflow beats Go Plus**; a Go Plus subscriber gets Argon at $240/mo (4×), which is its strongest case.

---

## The recommended setup

```jsonc
// OpenCode v2 (what this machine now runs). On v1 the same model IDs work.
{
  "$schema": "https://opencode.ai/config.json",
  "model": "opencode-go/deepseek-v4.1-flash",
  "small_model": "opencode-go/mimo-v2.6-flash",
  "agent": {
    "plan":    { "model": "opencode-go/grok-4.7" },          // or gemini-4-argon-contributor (non-client)
    "explore": { "model": "opencode-go/claude-haiku-5-5" },  // free lane alt: opencode/glm-5.3-flash-free
    "build":   { "model": "opencode-go/deepseek-v4.1-flash" }
  }
}
```

Free-tier routing note: `opencode/deepseek-v4.1-flash-free` and `opencode/glm-5.3-flash-free` are zero-retention free models that keep working after Go limits — use them as the bulk/free floor.

Escalate per task: `Kimi K3` (marathon/bug) · `Qwen3.8 Max` (visual QA) · `Muse Spark 1.3` (design/general, non-client) · `Gemini 4 Argon Contributor` (hard planning, non-client) · `MiMo-V2.6-Pro` (hard reasoning, cheap) · Copilot `Opus 5.5` (must-not-fail).
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
| [RESEARCH-GUIDE.md](./RESEARCH-GUIDE.md) | How this was researched and how to update it |

---

## New: Oct 16 refresh — Argon on Go, Step 5 paid + open weights, free-model explosion, v2 migration

- **Gemini 4 Argon Contributor joined Go (Oct 13):** the AA 53 frontier model now has a Contributor SKU on Go at $4/$20/$0.20 with a **$60/mo cap (2× promo)**, ~728 req/mo at your profile. Highest intelligence ever on Go, Vals #1 of 41 (68.9%), AutomationBench #1 (51.3%), lowest hallucination on AA-Omniscience (15% wrong guesses vs 29% next best). ⚠️ **Contributor terms: Google trains on your prompts/completions; not ZDR.** Non-client only; never in `small_model`/defaults.
- **Step 5 Preview free → paid:** now $1.00/$2.70/$0.10 with a **$60/mo 4× promo** (~2.4k req/mo at your profile). Its free window ended Oct ~15 — and the **open weights shipped Oct 15** (BF16 + FP8, HuggingFace/ModelScope), so it is now self-hostable too.
- **Beam Free (Oct 12, limited time/regions):** the new free model is **Reflection AI's Beam** (501B/23B MoE, text-only, Apache-2.0 weights, AA 30, SWE-bench Verified 80.9 vendor) — community nickname "Cat Jam". 30-day retention, **no training**. #10 by tokens in its first week; fast and token-efficient.
- **Zen free-model explosion:** **DeepSeek V4.1 Flash Free** (AA 39) and **GLM-5.3-Flash Free** (AA 42) — both **zero-retention, no training** — plus **Space Bunny Free** (stealth again), **LL Alpha Free** (new stealth, 256K ctx, 30-day retention + may train), **Nemotron 3.5 Super VL Free** (vision). The free floor is now stronger than the paid workhorse tier was in September.
- **Roster removals:** **Grok 4.6, Kimi K2.6, MiniMax M2.7** removed from Go docs (Grok 4.6/K2.6/M2.7 remain on Zen); DeepSeek V4 Flash fully retired. Go is now **29 models**.
- **GPT Luna tier split:** GPT 6 Luna and GPT 5.6 Luna now have >272K-context pricing tiers (docs).
- **Privacy changes:** Go docs now list **Grok 4.7 at 30-day retention** (no training; was documented as ZDR by this repo); Gemini 4 Argon Contributor and both Muse Spark Contributors train; Beam/LL Alpha 30-day; DeepSeek ZDR renewed **through Oct 31**.
- **This machine migrated to OpenCode v2.0.31.** v1 is now **1.19.3** with explicit 1.x pinning (1.19.2) and **session sharing discontinued** (1.19.1). v2 added remote device pairing + provider account management (2.0.29), worktree tools (2.0.27), changed-files-by-turn + docked diffs (2.0.30). Per the repo's own advice: v2 is fine for non-OmO workflows now; **OmO Ultimate still has no shipped v2 support**.
- **OmO 5.1.34 (Oct 16):** Gemini 4 Argon (high) inserted into `oracle` / `momus` / `plan-reviewer` chains (blind-tested: beat the previous pro rung in all 16 judgments, lost to GPT heads); `omo login/logout/whoami` disabled until accounts open; senpi defaults now Opus 5.5 / MiMo V2.6 Pro. **v2 dual-host support is still in review** (PR #9391 + slice 2 #9415 open; 8-slice plan, targeting the desktop's next release).
- **Telemetry (week to Oct 16):** DS V4.1 Flash #1 at 64T tokens (+64%), Muse Spark 38T, space-bunny 20T, MiMo-Flash 10T, **Step 5 5.6T (+267% on its free launch)**, **Beam 990B in week 1 (#10)**, Claude Haiku 5.5 +237%.
- **Watch (not on Go yet):** **Muse Wonder / Muse Wonder Full** (Meta, Oct 12 — AA 52/56), still Zen/Copilot-territory candidates.

## New: Oct 13 roster refresh (Haiku 5.5, Step 5, cap changes, legacy cleanup)

- **Claude Haiku 5.5 (Oct 7, on Go at $15/mo):** Anthropic's fastest model ever, 1M ctx, adjustable effort, TB4.0 39.2% at max, OSWorld 2.1 72.4%, matched Sonnet 5 on coding tasks in Copilot tests. The new default for explore/subagent/quick slots. 30-day retention (Anthropic, not OpenAI).
- **Step 5 Preview Free (Oct 8, on Go free):** StepFun 600B/27B-active MoE, AA 44 (tied Kimi K3), DeepSWE 67.7, TB4.0 33.3, open weights Oct 15. The best free coder on Go — route bulk agentic work here while the preview lasts.
- **DeepSeek V4.1 Flash $60→$80/mo:** ~25.5k req/mo at your profile (was 19.1k); weekly binding eased 83%→62%; monthly cap now binds only in crunch months. ZDR renewed through Oct 31 ✅.
- **Space Bunny free→paid** ($0.15/$0.60, $30/mo): removed from the free floor everywhere; keeps zero-retention.
- **Legacy demotion:** DeepSeek V4 Pro / V4 Flash / Vision Exp (retired upstream), GLM-5.2, MiMo-V2.5/Pro, Kimi K2.6 (superseded) moved out of all recommendation/capacity/value tables into Legacy notes. Roster/pricing/evidence tables keep them factually with legacy tags.

## New: Oct 13 OmO heavy-coding refresh + v1/v2 switch check (4 parallel research agents)

- **OmO 5.1.32 is current** (npm still serves stale 4.19.4 — install 5.x from GitHub releases; `doctor --verbose` to confirm). Upstream chains now put `claude-haiku-5-5` in explore/librarian/quick tails and confirm `kimi-k3 → plan-consultant`, `glm-5.3/kimi-k3 → unspecified-high`, `mimo-v2.6-pro → unspecified-low`.
- **Three ready `omo.jsonc` configs in `08` (hard-researched Oct 13):** **A HEAVY-MAX** (everything maxed, burst-oriented) · **B VALUE-8H** (K3 primary ~6/day + free Step 5 bulk lane — best bang for buck for 8h heavy days, start here) · **C ECO-24** (Step 5 primary + ~129 req/h sustained lanes, runs 24/7 and never binds a cap). Effort ladder + sustained-rate math included. Bonus findings: Step 5 AA 44 / Haiku AA 43 / MiMo-Flash AA 38 / Qwen Flash AA 40 all independently confirmed; Step 5 free may end ~Oct 15 (fallback baked into configs).
- **v1↔v2 switch:** v1 **1.19.0** (Oct 11, `upgrade --major` gate — staying on 1.x is now explicit) with end-of-support signaled but **no fixed EOL date**; v2 **2.0.28** latest; LSP still intentionally missing on v2, history migrator still partial, OmO-on-v2 still **not shipped**. Stay on v1 for production OmO.
- **Beyond-Go watch:** Muse Wonder (Oct 12, Spark's successor) and Gemini 4 Argon dev API (Oct 13) posted frontier coding claims — escalation-slot candidates, not on Go yet.

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

- Everything is a **snapshot** (Oct 1, 2026; roster/caps/value refreshed **Oct 16**). Model rosters, prices and limits changed ~weekly in Sep–Oct 2026.
- The **local calibration data is still the Sep 15 – Oct 1 history** (from the primary machine's v1 DB; this box's fresh v2 DB from Oct 16 is consistent with the same per-request profile, and is used only as a sanity check).
- AA Intelligence Index re-baselined to v4.3.2 in late Sep; older quoted scores are not comparable.
- Vendor benchmarks are self-reported; independent coverage gaps remain (METR/Epoch have almost no Go-model data).
- Limits math uses **your** token profile; a lighter user gets several× more requests per cap.
- Data policies change; re-verify before sending client/PHI data. **New this cycle:** Gemini 4 Argon Contributor trains on your data; Grok 4.7 is documented at 30-day retention; the free DeepSeek/GLM twins state zero-retention.
