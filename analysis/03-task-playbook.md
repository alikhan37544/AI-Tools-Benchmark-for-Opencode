# 03 — Task Playbook: Best Model for Each Kind of Work

> **Snapshot: October 1, 2026; refreshed October 13, 16 and 25, 2026.** Picks are for the **Go** roster (still **29 models**, but the composition changed: **+Kimi K3.1 Pro, +MiniMax M3.1 Flash; −Space Bunny, −LongCat 2.5 Preview Free**). **Step 5 Preview is paid** ($15 cap). **Gemini 4 Argon is no longer a Contributor/training SKU** — Go documents it as **not used / 0-day retention**, so the old “trains on your data” warning is withdrawn. Where the true best model is not on Go, that’s noted and the best Go alternative is given.
> Evidence symbols: 🟢 independent · 🟡 mixed/vendor+partial · 🔴 vendor-only.
>
> 🆕 **Oct 25 — the new stuff:** **Kimi K3.1 Pro (AA 55.1)** is the highest-intelligence model ever listed on Go, with 1M context, vision, and a **269 req/mo** heavy-user allowance. **MiniMax M3.1 Flash (AA 43)** is the new value workhorse — **4,975 req/mo at $0.0020/request** on the $10 plan, and it dominates GLM-5.3-Flash on price/quality. **DeepSeek V4.1 Flash’s 1017 checkpoint scores AA 45** at the same price (the original checkpoint is 39; treat 39 as the conservative baseline). On the independent side, **Vals v2.2** now has **Argon 69.24% (#3 overall, #1 Go model)**, **K3.1 Pro 62.52%**, **DeepSeek 1017 61.26%**, and **M3.1 Flash 53.78%**.

---

## 0. The master table

| # | Task category | Best on Go | Runner-up | Best value pick | Best overall (not on Go) | Key evidence |
|---|---|---|---|---|---|---|
| 1 | **Backend/API, refactors, migrations** | **Kimi K3.1 Pro** (hard/marathon) / **DeepSeek V4.1 Flash** (daily) | Gemini 4 Argon / GLM-5.3 | **MiniMax M3.1 Flash** (AA 43, 4,975 req/mo) | Claude Opus 5.5 | K3.1 Pro AA 55.1, Vals 62.52%; DS 1017 AA 45, DeepSWE 74.2 🟡; Argon Vals 69.24% 🟢 |
| 2 | **Frontend/UI (React, Tailwind, shadcn)** | **Muse Spark 1.3** | Kimi K3.1 Pro / Kimi K3 | **GLM-5.3-Flash** | GPT-6 Astra / Fable 5.1 | Design Arena website #1 (1365), K3 #3 (1345) 🟢; K3.1 Pro unmeasured on Design Arena 🟡 |
| 3 | **Database / SQL** | **GLM-5.3** | DeepSeek V4.1 Flash | **MiniMax M3.1 Flash** | Gemini-3-Pro + agent harness | Spider 2.0-Lite #1 agent used GLM-5.2 lineage (76.2) 🟡 |
| 4 | **Integration (3rd-party APIs, auth, webhooks, Kafka)** | **Kimi K3.1 Pro** | Hy4 preview | **DeepSeek V4.1 Flash** | Claude Opus 5 | MCP-Atlas: K3 84.2, Hy4 83.7, Opus 5 85.7 🟡; Toolathlon Hy4 74.1 🟡 |
| 5 | **Agentic terminal / DevOps / git / deploy** | **Gemini 4 Argon** (Vals #1 Go, 69.24%) / **Kimi K3.1 Pro** (AA 55.1) | Grok 4.7 / GLM-5.3 (TB4.0 41.9) | **MiniMax M3.1 Flash / DeepSeek V4.1 Flash** | GPT-6 Astra / Opus 5.5 | Vals v2.2: Argon 69.24% (#3 overall, #1 Go), K3.1 Pro 62.52%, DS 1017 61.26% 🟢; DS TB4.0 26.8 🟡 |
| 6 | **Long-horizon autonomy (multi-hour, self-directed)** | **Kimi K3.1 Pro** | Step 5 Preview (paid, TB4.0 33.3) | **DeepSeek V4.1 Flash / M3.1 Flash** | Claude Opus 4.6+ (METR ~12h) | Legacy LHTB #1 was retired DS V4 Flash 0.602; K3 0.378; K3.1 Pro inherits K3 lineage but has no published marathon figure yet 🟡 |
| 7 | **Visual QA / browser + GUI agents (Playwright)** | **Qwen3.8 Max** | Kimi K3.1 Pro / Kimi K3 | Qwen3.8 Flash | GPT-6 Astra (grounding) | OSWorld-Verified: Qwen3.8 Max 86.1 (#1 overall), K3 84.8 🟢; K3.1 Pro not measured 🟡 |
| 8 | **Image analysis / OCR / charts / screenshot→code** | **Qwen3.8 Max** | Kimi K3.1 Pro / MiMo-V2.6-Pro | Qwen3.8 Flash / DeepSeek V4.1 Flash | GPT-6 Astra / Gemini 3.x | MMMU-Pro 82.3 🟢; **LMArena Vision: Qwen3.8 #9** (not #2 — corrected Oct 25) 🟢; DS DocVQA 95.6 🟡 |
| 9 | **Planning / architecture reasoning** | **Kimi K3.1 Pro (AA 55.1)** / **Gemini 4 Argon (AA 53, Vals #1 Go)** | Grok 4.7 / Muse Spark 1.3 | **MiniMax M3.1 Flash / GLM-5.3-Flash** | GPT-6 Astra | AA v4.3.2: K3.1 Pro 55.1, Argon 53; Vals v2.2: Argon 69.24, K3.1 Pro 62.52 🟢; Argon is **ZDR/not trained** now |
| 10 | **Debugging / root-cause analysis** | **Kimi K3.1 Pro** (honesty lineage) / Grok 4.7 (edge cases) | DeepSeek V4.1 Flash | **MiniMax M3.1 Flash / GLM-5.3-Flash Free** | Claude Opus 5.5 | honesty battery: K3 0/12 false “done”; K3.1 Pro inherits the family behavior 🟡; GLM-Flash Free is $0 |
| 11 | **Long context (huge repos, logs)** | **Kimi K3.1 Pro** (1M native) / DeepSeek V4.1 Flash (1M, cheapest cache) | Gemini 4 Argon (1M, ZDR) / Step 5 (AA-LCR 88.3) | **DeepSeek V4.1 Flash / M3.1 Flash** | GPT-6 Astra / Opus 4.6 | K3 AA-LCR 74.7 🟢; K3.1 Pro 1M ctx 🟢; retired DS V4 Pro MRCR-1M 83.5 🟢 |
| 12 | **Fast/cheap bulk edits, boilerplate, tests** | **MiniMax M3.1 Flash** | MiMo-V2.6-Flash / DeepSeek V4.1 Flash / Claude Haiku 5.5 | **GLM-5.3-Flash Free (AA 42, $0)** | GPT-6 Luna ($0.07/task) | M3.1 Flash: AA 43, 112.8 tok/s, 1.35s TTFT, $0.22/AA task, 4,975 req/mo 🟢; MiMo-Flash 33k req/mo 🟢 |
| 13 | **General intelligence / research / explanation** | **Kimi K3.1 Pro (55.1)** | Gemini 4 Argon (53) / Muse Spark 1.3 (48) / MiMo-V2.6-Pro / Grok 4.7 (46) | **MiniMax M3.1 Flash / GLM-5.3-Flash Free** | Claude Opus 5.5 (58) / GPT-6 Astra (53) | AA v4.3.2 🟢; Argon AA-Omniscience lowest hallucination 🟢; Vals: Argon 69.24 > K3.1 Pro 62.52 for agentic coding |
| 14 | **Data / analysis / ML notebooks (pandas, XGBoost, SHAP)** | **Kimi K3.1 Pro** / MiniMax M3.1 Flash | Qwen3.8 Flash | DeepSeek V4.1 Flash | Gemini-3-Pro agents | MLE-bench Lite M2.7 66.6% medal 🟡 (retired); official board Gemini-led 🟢 |
| 15 | **Systems/hardware (overclocking, ROMs, drivers, homelab)** | **Kimi K3.1 Pro** / Grok 4.7 | MiMo-V2.6-Pro | DeepSeek V4.1 Flash | GPT-6 Sol / Opus 5.5 | Grok EEBench 64.0 🟡; MiMo Pro 23/23 hidden checks vs Opus 5 in OpenCode 🟡 |
| 16 | **Voicebot / realtime / telephony debugging** | DeepSeek V4.1 Flash | Kimi K3.1 Pro | MiMo-V2.6-Flash | — (audio models are separate) | no dedicated bench; integration + debugging proxies |
| 17 | **Repo Q&A / explore subagent (cheap, high volume)** | **Claude Haiku 5.5 / MiMo-V2.6-Flash** | GLM-5.3-Flash | **DeepSeek V4.1 Flash Free / GLM-5.3-Flash Free ($0)** | — | Haiku: fastest Claude, 1M ctx, $0.0028/req; MiMo-Flash 33k req/mo, $0.0018/req |
| 18 | **Spec/plan writing before implementation** | **Kimi K3.1 Pro / Gemini 4 Argon** | Grok 4.7 / Muse Spark 1.3 | MiniMax M3.1 Flash | Opus 5.5 | planning = GPQA/ARC plus AA-Briefcase; K3.1 Pro AA 55.1 is the new ceiling |

---

## 1. Category notes and caveats

### Backend / API / refactors
- **DeepSeek V4.1 Flash** is still the best daily driver: 209–232 tok/s, 1M ctx, native vision, 96% cache ratio, and a DeepSWE 74.2 vendor run. **The 1017 checkpoint now scores AA 45** (169.1 tok/s, TTFT 1.18s, $0.26/task, 210M verbosity) versus 39 for the original — same Go ID and price. Treat **39 as the conservative baseline** and 45 as upside until the router consistently serves 1017. Its honest weakness is hard long-horizon benchmarks: AA’s standardized TB4.0 gives it only 26.8. Short-to-medium agent loops: excellent. Multi-hour marathon: escalate.
- **Kimi K3.1 Pro** is the new hard-task pick: AA 55.1, 1M ctx, vision, Vals 62.52. It replaces Kimi K3 at the top of the Go ladder for refactors and multi-file work. Caveat: harness must preserve reasoning history; high verbosity (150M) and only ~269 heavy requests/mo.
- **Gemini 4 Argon** is the independent agentic leader among Go models (Vals 69.24%, #3 overall) and is now **ZDR/not trained** — a genuine change from the Oct 16 advice. It also has 728 req/mo, 2.7× K3.1 Pro’s capacity. For most planning/agentic work, Argon is the better *workhorse*; K3.1 Pro is the higher-AA *ceiling*.
- **MiniMax M3.1 Flash** is the value pick: AA 43, 112.8 tok/s, 1.35s TTFT, $0.22/AA task, 4,975 req/mo. It is the best “good enough” backend model per dollar on Go.

### Frontend / UI
- **Muse Spark 1.3** still tops Design Arena’s website board (1365) and is #5 by lab on WebDev Arena; **Kimi K3** is #3 (1345), and **K3.1 Pro** is likely at least as strong but has no Design Arena entry yet 🟡. Treat the gap as small and the data as stale.
- **GLM-5.3-Flash** ranks top-20 in WebDev frontend at $0.15/$0.50 with a $60 allowance — the “good enough frontend at 9.8k requests/month” pick. **M3.1 Flash** is the new alternative if you want AA 43 at 4.9k req/mo.
- GPT-6 Astra (1800 WebDev) is the true leader; Fable 5.1/Opus 5.5 (1758/1687) follow.

### Database / SQL
- Spider 2.0’s board ranks *agent systems*, not raw models. The #1 Lite entry used the **GLM-5.2 lineage**; Snow entries use Gemini-3-Pro and Claude Sonnet agents. GLM-5.3 inherits 5.2’s strengths (Terminal-Bench 81.0, SWE-bench Pro 62.1) plus better reasoning. (GLM-5.2 itself is superseded — use 5.3.)
- Practical rule: for schema/migration reasoning use GLM-5.3; for query iteration loops use DeepSeek V4.1 Flash or M3.1 Flash (cheap + fast); always run migrations through the plan agent with the DB MCP/tool, not freehand.

### Integrations
- **MCP-Atlas** is the closest proxy: Kimi K3 84.2, Hy4 preview 83.7, DS V4 Pro 82.5, GLM-5.3/Qwen3.8 Max 81.9, Opus 5 85.7. Hy4’s **Toolathlon-Verified 74.1** is the best Go tool-use signal. K3.1 Pro has no MCP-Atlas entry yet; assume K3-class or better 🟡.
- For auth/webhook debugging there is no dedicated benchmark; model quality on code + tool use is the proxy. K3.1 Pro/Hy4 first, DeepSeek/M3.1 Flash for volume.

### Agentic terminal / DevOps / git / deploy
- The independent split: **Gemini 4 Argon** leads Vals v2.2 among Go models (69.24%, #3 overall behind Sonnet 5.5 and Opus 5.5); **Kimi K3.1 Pro** is second (62.52%) and higher on AA (55.1); **Grok 4.7** carries the verified Grok generation forward; **GLM-5.3** wins standardized TB4.0 (41.9); **DeepSeek V4.1 Flash** wins vendor TB2.1 (90.6) and throughput, but drops to 26.8 on TB4.0.
- For **Azure CLI / `az ssh` / Docker / CI pipelines**, favor models that are strong in terminal loops *and* cheap enough to iterate: DeepSeek V4.1 Flash (or its free twin) for the loop, Argon or K3.1 Pro for the planning step. Never auto-run destructive deploy commands without permission gates (see `07-recommended-config.md`).

### Long-horizon autonomy
- The cleanest public signal was **LHTB** (Long-Horizon Task Benchmark): retired DeepSeek V4 Flash #1 (0.602 mean reward), Grok 4.5 0.505, MiniMax M3 0.385, Kimi K3 0.378, Kimi K2.7 0.367. Caveat: custom harness, and the winner is retired upstream — treat as historical signal only.
- **Kimi K3.1 Pro** inherits K3’s marathon lineage (SWE-Marathon 42.0, FrontierSWE 81.2 for K3) but **no independent 3.1 marathon figure exists yet** 🟡. It is the best *available* Go pick for multi-hour work; **Step 5 Preview** (TB4.0 33.3, AA-LCR 88.3) remains the cheap paid capacity pick at $15.
- METR’s time-horizon evals show the true frontier at ~12h p50 (Opus 4.6) and **no Go model has a published measurement**. If a task is truly “walk away for 8 hours,” budget for escalation to a frontier non-Go model.

### Visual QA / browser agents
- **Qwen3.8 Max is the #1 model in the world on OSWorld-Verified (86.1)**, above Fable 5/Mythos 5 (85). Its ScreenSpot-Pro 84.5 is the top Go result. **LMArena Vision rank is #9, not #2** — corrected Oct 25.
- Kimi K3 (84.8 OSWorld) and MiMo-V2.6-Pro (82.0) follow. K3.1 Pro is multimodal but has no OSWorld entry; treat K3’s 84.8 as the floor 🟡. For Playwright screenshot-diff loops, Qwen3.8 Max is worth its small $15 allowance for final verification runs; run the bulk loop on Qwen3.8 Flash or DeepSeek vision.

### Image analysis / OCR
- **Qwen3.8 Max** (MMMU-Pro 82.3, DocVQA-class vision, LMArena Vision #9) is the best Go vision model; **Qwen3.8 Flash** is the 6B-active value version; **MiMo-V2.6-Pro** accepts image+video+speech and has 1M ctx; **Kimi K3.1 Pro** adds 1M-context vision.
- For document OCR at volume, **DeepSeek V4.1 Flash** (DocVQA 95.6, 96% cache ratio, $0.60/M output, native vision) is the cheapest competent option. (The old `deepseek-v4-flash-vision-exp` route is retired upstream — use V4.1 Flash.)
- For Arabic OCR/translation, no public benchmark separates models; test candidates on your own corpus (Qwen3.8 Max/Flash, MiMo, K3.1 Pro).

### Planning / architecture
- **Kimi K3.1 Pro** is the new AA ceiling (55.1). **Gemini 4 Argon** is the independent agentic leader (Vals 69.24%) and now **ZDR/not trained**, with 728 req/mo — for most planning work, Argon’s capacity and independent evidence make it the better default; K3.1 Pro is the escalation for the hardest architecture.
- **Grok 4.7** remains the privacy-safe reasoning alternative (it inherits the Grok 4.6 generation’s GPQA 95.0 / ARC-AGI-2 67.1 profile). Muse Spark 1.3 leads the privacy-flagged AA index at 48; MiMo-V2.6-Pro is the value pick.
- Use the `plan` agent with a premium model, then hand the plan to a cheap model for execution (see config).

### Debugging / RCA
- The **agent-honesty battery** is the most relevant small study: Kimi K3 had 0/12 false “fixed” claims and 0/6 silent compliance; Grok 4.6 never lied but silently obeyed contradictory instructions 5/6 times; retired DeepSeek V4 Flash and superseded GLM-5.2 each had 1/12 (historical signal). K3.1 Pro inherits K3’s family behavior; no separate 3.1 battery yet 🟡.
- Practical: K3.1 Pro for root-cause honesty; Grok 4.7 for edge-case precision; DeepSeek V4.1 Flash or M3.1 Flash for the cheap iteration loop; the free GLM-5.3-Flash lane as the $0 second opinion.

### Long context
- Current 1M-context picks: **Kimi K3.1 Pro** (native 1M, vision), **DeepSeek V4.1 Flash** (1M, cheapest cache-reads), **Gemini 4 Argon** (1M, ZDR), **Step 5 Preview** (AA-LCR 88.3 🟡, paid). Muse Spark 1.3 self-reports 98.1 on MRCR v2 8-needle 512K–1M (no independent track). (Historical: retired DeepSeek V4 Pro MRCR-1M 83.5.)
- Beware: long contexts burn cache-reads; DeepSeek’s $0.003/M cache makes it the cheapest way to feed a huge repo — and the free twin makes it $0.

### Data / ML
- MiniMax M2.7’s MLE-bench Lite 66.6% medal rate is the best historical Go signal, but its AA index is 23 and it is retired; the official MLE-bench leaderboard is dominated by Gemini-3-Pro agent frameworks. For XGBoost/SHAP/metric pipelines, **K3.1 Pro** or **M3.1 Flash** will usually beat the old specialist end-to-end; use DeepSeek for the cheap loop.

### Systems / hardware (overclocking, ROMs, drivers, homelab)
- **No serious benchmark exists** for PC overclocking, Android ROM/AOSP/kernel work, or homelab tuning. Best proxies: GPQA/EEBench (Grok 4.7 EEBench 64.0), general coding, and long-horizon tool use.
- Community evidence: AOSP/ROM developers use Claude/GPT as a “velocity engine” but treat output as untrusted; MiMo-V2.6-Pro matched Opus 5 on 23/23 hidden checks in OpenCode for ~$0.03 vs $1.03 in one test, but failed 2/3 Kubernetes manifests in an independent DevOps test.
- Practical ladder: plan with **K3.1 Pro** or **Grok 4.7**, execute scripts with **DeepSeek V4.1 Flash**, escalate anything that can brick a device to a frontier non-Go model + explicit human verification. For your Mac PPM power-budget overclocking experiments, use the plan agent to generate stress/rollback scripts, and never let an agent auto-run a reboot or SMC/NVRAM-touching command.

---

## 2. Personalized routing for this machine’s workload

Observed profile (last 60 days of local OpenCode history): TypeScript/Node + Python FastAPI services, MySQL/Oracle/Postgres/Redis/Memgraph, Azure services and Azure Pipelines, Docker, Playwright/Selenium/Puppeteer RPA, OCR/document AI (including Arabic documents), voicebot/telephony (Kafka, Asterisk ARI), insurance/healthcare domain with strict privacy, some ML (XGBoost/SHAP), and Apple-Silicon power/thermal experiments.

### Recommended role assignment

| Role | Model | Why |
|---|---|---|
| **Daily driver / build** | `deepseek-v4.1-flash` (max) | Proven at your volume; ~25.5k req/mo at your profile ($80 cap); 96% cache hit; native vision; 1017 checkpoint may serve AA 45 |
| **Free workhorse (bulk)** | `deepseek-v4.1-flash-free` / `glm-5.3-flash-free` | Zero-retention free twins; AA 39/42; keep working after Go limits |
| **Explore / repo Q&A / subagents** | `claude-haiku-5-5` or `mimo-v2.6-flash` | Haiku: fastest Claude, 1M ctx, Sonnet-class coding; MiMo-Flash: 33k req/mo, $0.0018/req |
| **Free bulk coding** | `glm-5.3-flash-free` (AA 42) or `beam-free` (AA 30) | Best free intelligence with zero-retention (GLM) or no-training/30-day (Beam) |
| **Bulk edits / boilerplate / tests** | `minimax-m3.1-flash` / `glm-5.3-flash` | M3.1 Flash: AA 43, 4,975 req/mo, $0.0020/req plan-effective; GLM-Flash: 9.8k req/mo |
| **Plan / architecture** | `gemini-4-argon` (728 req/mo, ZDR) or `kimi-k3.1-pro` (AA 55.1, 269 req/mo) | Argon: Vals #1 Go, independent; K3.1 Pro: AA ceiling |
| **Hard debugging** | `kimi-k3.1-pro` | Honesty lineage + 1M context + AA 55.1 |
| **Frontend / design review** | `muse-spark-1.3-contributor` (non-client) or `kimi-k3.1-pro` | Design Arena #1 / K3 #3; K3.1 Pro likely at least K3-class |
| **Visual QA from screenshots** | `qwen3.8-max` (verification) + `qwen3.8-flash` (loop) | OSWorld #1 overall / cheap sibling |
| **OCR / document AI** | `deepseek-v4.1-flash` or `qwen3.8-flash` | Cheap native vision; Qwen flash is the quality step-up |
| **Marathon autonomous refactor** | `kimi-k3.1-pro`, escalate to Claude Opus 5.5 via Copilot if it must be one-shot | K3 lineage marathon strength; K3.1 Pro is the new ceiling |
| **General research / explanation** | `kimi-k3.1-pro` / `gemini-4-argon` / `muse-spark-1.3-contributor` / `grok-4.7` | AA 55.1 / 53 / 48 / 46 |
| **Frontier escalation (5% hardest)** | Claude Opus 5.5 / GPT-6 Astra via your GitHub Copilot access, or Zen `claude-opus-5-5` / `gpt-6-astra` | AA 58 / 53; not on Go |

### Hard constraints to respect

1. **Client contract disallows OpenAI models** for at least one computer-vision project → keep GPT-6/5.6 Luna and GPT-6 Astra out of that pipeline; use Gemini/local YOLO/Qwen as configured there.
2. **PHI/medical/insurance data**: avoid models whose provider trains on inputs — **Muse Spark Contributor, Big Pickle, MiMo free, NVIDIA free, Flint 40B Free**. **Gemini 4 Argon is now documented “Not used / 0 days”** and the old training warning is withdrawn — but re-verify before PHI work. Prefer GLM/MiMo paid/Kimi/Qwen/DeepSeek routes — **the free DeepSeek/GLM twins state zero-retention**. DeepSeek’s zero-retention is **renewed through October 31, 2026** ✅. Claude Haiku 5.5 has 30-day retention (frontier-API standard) — fine for non-PHI, and it is Anthropic (not OpenAI), so the CV client contract’s OpenAI ban doesn’t cover it — verify with the client anyway.
3. **Never start servers autonomously** (per your own GEMINI.md rule) — encode this in agent permissions, not in the prompt.
4. **Azure DevOps is your CI** (no GitHub Actions in your repos) — give the agent `az`/`az devops` CLI tools explicitly and keep PAT handling in the environment.
5. **Arabic OCR**: benchmark the top-3 vision models on your own `curenure_ocr_ar` corpus before switching; public benchmarks under-sample Arabic.
6. **This machine runs OpenCode v2.1.4** — v1-only tooling (OmO Ultimate) needs the OmO Native path or staying pinned on v1.19.4 until the dual-host plugin ships.

---

## 3. The escalation ladder (how to actually use this)

```
Task arrives
 ├─ Routine edit / question / explore  → MiMo-V2.6-Flash / Claude Haiku 5.5 (or the free twins)
 ├─ Free agentic coding                 → GLM-5.3-Flash Free / DeepSeek V4.1 Flash Free (zero-retention)
 ├─ Normal feature/build work          → DeepSeek V4.1 Flash (max)
 ├─ Cheap quality step-up              → MiniMax M3.1 Flash (AA 43, 4,975 req/mo)
 ├─ Frontend-heavy visual work         → Muse Spark 1.3 / GLM-5.3-Flash (non-client)
 ├─ Needs planning or design           → Gemini 4 Argon (ZDR, 728 req/mo) / Kimi K3.1 Pro (AA 55.1)
 ├─ Hard bug / marathon / 1M context   → Kimi K3.1 Pro (ration: ~269 req/mo)
 ├─ Visual QA / OCR verification       → Qwen3.8 Max (ration: ~256 req/mo)
 └─ Must-not-fail / frontier-level     → Copilot Opus 5.5 / Astra (or Zen overflow)
```

Splitting work this way keeps the expensive allowances for the ~5% of requests that actually need them. In practice: a `plan` call on Argon (ZDR) or K3.1 Pro, a `build` loop on DeepSeek V4.1 Flash, an `explore` agent on Haiku 5.5 / MiMo-Flash, M3.1 Flash for the cheap quality lane, one K3.1 Pro review per difficult PR, and the free twins carrying bulk work.

---

**Next:** [04 — Limits & Burn Rate](./04-limits-and-burn-rate.md) · [05 — Intelligence per Dollar](./05-intelligence-per-dollar.md)
