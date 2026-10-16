# 03 — Task Playbook: Best Model for Each Kind of Work

> **Snapshot: October 1, 2026, refreshed October 13 and October 16.** Picks are for the **Go** roster (now **29 models**: +Gemini 4 Argon Contributor, +Beam Free; Step 5 Preview now paid; Grok 4.6 / Kimi K2.6 / MiniMax M2.7 removed). Where the true best model is not on Go, that's noted and the best Go alternative is given.
> Evidence symbols: 🟢 independent · 🟡 mixed/vendor+partial · 🔴 vendor-only.
>
> 🆕 **Oct 16 — the new stuff:** **Step 5 Preview is no longer free** (it is now a paid $60/mo 4×-promo model); the free floor moved to the **Zen twins — DeepSeek V4.1 Flash Free (AA 39) and GLM-5.3-Flash Free (AA 42), both zero-retention** — plus Beam Free. **Gemini 4 Argon Contributor (AA 53, trains on data)** is the new top pick for planning/general intelligence on non-client work. Rows updated accordingly; ★ = trains on your data.

---

## 0. The master table

| # | Task category | Best on Go | Runner-up | Best value pick | Best overall (not on Go) | Key evidence |
|---|---|---|---|---|---|---|
| 1 | **Backend/API, refactors, migrations** | Kimi K3 (marathon) / DeepSeek V4.1 Flash (daily) | GLM-5.3 / Gemini 4 Argon★ | **DeepSeek V4.1 Flash Free** | Claude Opus 5.5 | DS: DeepSWE 74.2, TB2.1 90.6 🟡; K3: SWE-Marathon 42.0, FrontierSWE 81.2 🟡; Step 5: DeepSWE 67.7, TB4.0 33.3 🟡 |
| 2 | **Frontend/UI (React, Tailwind, shadcn)** | **Muse Spark 1.3** | Kimi K3 | GLM-5.3-Flash | GPT-6 Astra / Fable 5.1 | Design Arena website #1 (1365), K3 #3 (1345) 🟢 |
| 3 | **Database / SQL** | GLM-5.3 | DeepSeek V4.1 Flash | GLM-5.3-Flash | Gemini-3-Pro + agent harness | Spider 2.0-Lite #1 agent used GLM-5.2 lineage (76.2) 🟡 |
| 4 | **Integration (3rd-party APIs, auth, webhooks, Kafka)** | Kimi K3 | Hy4 preview | DeepSeek V4.1 Flash | Claude Opus 5 | MCP-Atlas: K3 84.2, Hy4 83.7, Opus 5 85.7 🟡; Toolathlon Hy4 74.1 🟡 |
| 5 | **Agentic terminal / DevOps / git / deploy** | Grok 4.7 (verified) / Gemini 4 Argon★ (Vals #1) / DeepSeek V4.1 Flash (volume) | GLM-5.3 (best TB4.0: 41.9) | **GLM-5.3-Flash Free / DeepSeek V4.1 Flash Free ($0)** | GPT-6 Astra / Opus 5.5 | Vals: Argon #1 of 41 (68.9%); DS TB2.1 90.6 🟡; Step 5 TB4.0 33.3 🟡 |
| 6 | **Long-horizon autonomy (multi-hour, self-directed)** | Kimi K3 | Step 5 Preview (paid, TB4.0 33.3) | DeepSeek V4.1 Flash | Claude Opus 4.6+ (METR ~12h) | Legacy signal: LHTB #1 was retired DS V4 Flash 0.602; K3 0.378; METR has no Go model 🟡 |
| 7 | **Visual QA / browser + GUI agents (Playwright)** | **Qwen3.8 Max** | Kimi K3 | Qwen3.8 Flash | GPT-6 Astra (grounding) | OSWorld-Verified: Qwen3.8 Max 86.1 (#1 overall), K3 84.8 🟢 |
| 8 | **Image analysis / OCR / charts / screenshot→code** | **Qwen3.8 Max** | Kimi K3 / MiMo-V2.6-Pro | Qwen3.8 Flash / DeepSeek V4.1 Flash | GPT-6 Astra / Gemini 3.x | LMArena Vision Qwen3.8 #2, MMMU-Pro 82.3 🟢 |
| 9 | **Planning / architecture reasoning** | **Gemini 4 Argon★ (AA 53)** / Grok 4.7 | Muse Spark 1.3 / MiMo-V2.6-Pro | GLM-5.3-Flash | GPT-6 Astra | Argon Vals #1 68.9%, AA 53, AutomationBench #1 🟢 (trains on data) |
| 10 | **Debugging / root-cause analysis** | Kimi K3 (honesty) / Grok 4.7 (edge cases) | DeepSeek V4.1 Flash | GLM-5.3-Flash Free (2nd opinion, $0) | Claude Opus 5.5 | honesty battery: K3 0/12 false "done"; Grok 4.6 0/12 but 5/6 silent compliance 🟡 |
| 11 | **Long context (huge repos, logs)** | Kimi K3 (1M native, AA-LCR 74.7) / DeepSeek V4.1 Flash (1M, cheapest cache) | Muse Spark 1.3 (MRCR 98.1 self-report 🟡) / Gemini 4 Argon★ (1M) | DeepSeek V4.1 Flash Free | GPT-6 Astra / Opus 4.6 | Legacy signal: retired DS V4 Pro MRCR-1M 83.5 🟢; Step 5 AA-LCR 88.3 🟡 |
| 12 | **Fast/cheap bulk edits, boilerplate, tests** | **MiMo-V2.6-Flash / DeepSeek V4.1 Flash / Claude Haiku 5.5** | GLM-5.3-Flash | **GLM-5.3-Flash Free (AA 42, $0)** | GPT-6 Luna ($0.07/task) | session cost: MiMo-Flash $0.0023, DS $0.0435 🟢 (OpenCode telemetry); GLM-Flash Free is zero-retention |
| 13 | **General intelligence / research / explanation** | **Gemini 4 Argon★ (53)** | Muse Spark 1.3 (48) / MiMo-V2.6-Pro / Grok 4.7 (46) | GLM-5.3-Flash Free | Claude Opus 5.5 (58) / GPT-6 Astra (53) | AA v4.3.2 🟢; Argon AA-Omniscience lowest hallucination |
| 14 | **Data / analysis / ML notebooks (pandas, XGBoost, SHAP)** | MiniMax M3 / Kimi K3 | Qwen3.8 Flash | DeepSeek V4.1 Flash | Gemini-3-Pro agents | MLE-bench Lite M2.7 66.6% medal 🟡; official board led by Gemini agents 🟢 |
| 15 | **Systems/hardware (overclocking, ROMs, drivers, homelab)** | Grok 4.7 / Kimi K3 | MiMo-V2.6-Pro | DeepSeek V4.1 Flash | GPT-6 Sol / Opus 5.5 | Grok EEBench 64.0 🟡; MiMo Pro 23/23 hidden checks vs Opus 5 in OpenCode 🟡 |
| 16 | **Voicebot / realtime / telephony debugging** | DeepSeek V4.1 Flash | Kimi K3 | MiMo-V2.6-Flash | — (audio models are separate) | no dedicated bench; integration + debugging proxies |
| 17 | **Repo Q&A / explore subagent (cheap, high volume)** | **Claude Haiku 5.5 / MiMo-V2.6-Flash** | GLM-5.3-Flash | **DeepSeek V4.1 Flash Free / GLM-5.3-Flash Free ($0)** | — | Haiku: fastest Claude, 1M ctx, $0.0028/req; MiMo-Flash 33k req/mo, $0.0018/req |
| 18 | **Spec/plan writing before implementation** | Gemini 4 Argon★ / Grok 4.7 | Muse Spark 1.3 | GLM-5.3-Flash | Opus 5.5 | planning = GPQA/ARC plus AA-Briefcase |

---

## 1. Category notes and caveats

### Backend / API / refactors
- **DeepSeek V4.1 Flash** is the best daily driver: 209–232 tok/s, 1M ctx, native vision, 96% cache ratio, and a DeepSWE 74.2 vendor run that edges Opus 5's 74.0 in the same table. Its honest weakness is hard long-horizon benchmarks: AA's standardized TB4.0 gives it only 26.8. Short-to-medium agent loops: excellent. Multi-hour marathon: escalate. **The free Zen twin (`deepseek-v4.1-flash-free`) is zero-retention and costs nothing** — the new default bulk lane.
- **Kimi K3** is the marathon pick (SWE-Marathon 42.0 beat Fable 5 35 and GPT-5.6 Sol 39). Caveat: harness must preserve reasoning history.
- **GLM-5.3** is the best *standardized* Terminal-Bench 4.0 performer on Go (41.9) — the pick when "it must survive a hard harness."
- **Gemini 4 Argon (Contributor)** is the new ceiling for hard refactors (AA 53, Vals #1) — but its terms train Google on your data; keep it off client repos.

### Frontend / UI
- **Muse Spark 1.3** tops Design Arena's website board and is #5 by lab on WebDev Arena; Kimi K3 is within ~15–20 Elo and stronger on complex app code. Both use vendor agent settings; treat the gap as small.
- **GLM-5.3-Flash** ranks top-20 in WebDev frontend at $0.15/$0.50 with a $60 allowance — the "good enough frontend at 30k requests/month" pick.
- GPT-6 Astra (1800 WebDev) is the true leader; Fable 5.1/Opus 5.5 (1758/1687) follow.

### Database / SQL
- Spider 2.0's board ranks *agent systems*, not raw models. The #1 Lite entry used the **GLM-5.2 lineage**; Snow entries use Gemini-3-Pro and Claude Sonnet agents. GLM-5.3 inherits 5.2's strengths (Terminal-Bench 81.0, SWE-bench Pro 62.1) plus better reasoning. (GLM-5.2 itself is superseded — use 5.3.)
- Practical rule: for schema/migration reasoning use GLM-5.3; for query iteration loops use DeepSeek V4.1 Flash (cheap + fast); always run migrations through the plan agent with the DB MCP/tool, not freehand.

### Integrations
- **MCP-Atlas** is the closest proxy: Kimi K3 84.2, Hy4 preview 83.7, DS V4 Pro 82.5, GLM-5.3/Qwen3.8 Max 81.9, Opus 5 85.7. Hy4's **Toolathlon-Verified 74.1** is the best Go tool-use signal.
- For auth/webhook debugging there is no dedicated benchmark; model quality on code + tool use is the proxy. Kimi K3/Hy4 first, DeepSeek for volume.

### Agentic terminal / DevOps / git / deploy
- The independent split: **Gemini 4 Argon** now tops Vals (68.9%, #1 of 41 — data caveat); **Grok 4.7** carries the verified Grok generation forward (Grok 4.6 was removed from Go); **GLM-5.3** wins standardized TB4.0 (41.9); **DeepSeek V4.1 Flash** wins vendor TB2.1 (90.6) and throughput, but drops to 26.8 on TB4.0.
- For **Azure CLI / `az ssh` / Docker / CI pipelines**, favor models that are strong in terminal loops *and* cheap enough to iterate: DeepSeek V4.1 Flash (or its free twin) for the loop, Grok 4.7 or GLM-5.3 for the planning step. Never auto-run destructive deploy commands without permission gates (see `07-recommended-config.md`).

### Long-horizon autonomy
- The cleanest public signal was **LHTB** (Long-Horizon Task Benchmark): retired DeepSeek V4 Flash #1 (0.602 mean reward), Grok 4.5 0.505, MiniMax M3 0.385, Kimi K3 0.378, Kimi K2.7 0.367. Caveat: custom harness, and the winner is retired upstream — treat as historical signal only.
- **Step 5 Preview** (TB4.0 33.3, 2.6× Kimi K3, AA-LCR 88.3) is built for long-horizon tool use and is now a **paid $60/mo 4×-promo model** — still the best paid capacity at AA 44+, and self-hostable since Oct 15. The free walk-away option is now the **DeepSeek V4.1 Flash Free / GLM-5.3-Flash Free** lanes.
- METR's time-horizon evals show the true frontier at ~12h p50 (Opus 4.6) and **no Go model has a published measurement**. If a task is truly "walk away for 8 hours," budget for escalation to a frontier non-Go model.

### Visual QA / browser agents
- **Qwen3.8 Max is the #1 model in the world on OSWorld-Verified (86.1)**, above Fable 5/Mythos 5 (85). Its ScreenSpot-Pro 84.5 is the top Go result; LMArena Vision #2.
- Kimi K3 (84.8 OSWorld) and MiMo-V2.6-Pro (82.0) follow. For Playwright screenshot-diff loops, Qwen3.8 Max is worth its small $15 allowance for final verification runs; run the bulk loop on Qwen3.8 Flash or DeepSeek vision.

### Image analysis / OCR
- **Qwen3.8 Max** (MMMU-Pro 82.3, DocVQA-class vision, LMArena Vision #2) is the best Go vision model; **Qwen3.8 Flash** is the 6B-active value version; **MiMo-V2.6-Pro** accepts image+video+speech and has 1M ctx.
- For document OCR at volume, **DeepSeek V4.1 Flash** (DocVQA 95.6, 96% cache ratio, $0.60/M output, native vision) is the cheapest competent option. (The old `deepseek-v4-flash-vision-exp` route is retired upstream — use V4.1 Flash.)
- For Arabic OCR/translation, no public benchmark separates models; test candidates on your own corpus (Qwen3.8 Max/Flash, MiMo, Kimi K3).

### Planning / architecture
- **Gemini 4 Argon (Contributor)** is the new top Go intelligence (AA 53; Vals #1; AutomationBench #1; lowest hallucination) — ⚠️ trains on your data, so non-client only. **Grok 4.7** remains the strongest privacy-safe reasoning evidence (it inherits the Grok 4.6 generation's GPQA 95.0 / ARC-AGI-2 67.1 profile). Muse Spark 1.3 leads the privacy-flagged AA index at 48; MiMo-V2.6-Pro is the value pick.
- Use the `plan` agent with a premium model, then hand the plan to a cheap model for execution (see config).

### Debugging / RCA
- The **agent-honesty battery** is the most relevant small study: Kimi K3 had 0/12 false "fixed" claims and 0/6 silent compliance; Grok 4.6 never lied but silently obeyed contradictory instructions 5/6 times; retired DeepSeek V4 Flash and superseded GLM-5.2 each had 1/12 (historical signal).
- Practical: Kimi K3 for root-cause honesty; Grok 4.7 for edge-case precision; DeepSeek V4.1 Flash (or the free twin) for the cheap iteration loop; the free GLM-5.3-Flash lane as the $0 second opinion (Step 5 is no longer free).

### Long context
- Current 1M-context picks: **Kimi K3** (native 1M + AA-LCR 74.7, independent), **DeepSeek V4.1 Flash** (1M, cheapest cache-reads), **Step 5 Preview** (AA-LCR 88.3 🟡, now paid), **Gemini 4 Argon** (1M, data caveat). Muse Spark 1.3 self-reports 98.1 on MRCR v2 8-needle 512K–1M (no independent track). (Historical: retired DeepSeek V4 Pro MRCR-1M 83.5.)
- Beware: long contexts burn cache-reads; DeepSeek's $0.003/M cache makes it the cheapest way to feed a huge repo — and the free twin makes it $0.

### Data / ML
- MiniMax M2.7's MLE-bench Lite 66.6% medal rate is the best Go signal, but its AA index is 23 — it's a specialist, not a generalist. The official MLE-bench leaderboard is dominated by Gemini-3-Pro agent frameworks. For your XGBoost/SHAP/metric pipelines, DeepSeek V4.1 Flash or Kimi K3 will usually beat M2.7 end-to-end.

### Systems / hardware (overclocking, ROMs, drivers, homelab)
- **No serious benchmark exists** for PC overclocking, Android ROM/AOSP/kernel work, or homelab tuning. Best proxies: GPQA/EEBench (Grok 4.7 EEBench 64.0), general coding, and long-horizon tool use.
- Community evidence: AOSP/ROM developers use Claude/GPT as a "velocity engine" but treat output as untrusted; MiMo-V2.6-Pro matched Opus 5 on 23/23 hidden checks in OpenCode for ~$0.03 vs $1.03 in one test, but failed 2/3 Kubernetes manifests in an independent DevOps test.
- Practical ladder for hardware work: plan with **Grok 4.6** or **Kimi K3**, execute scripts with **DeepSeek V4.1 Flash**, and escalate anything that can brick a device to a frontier non-Go model + explicit human verification. For your Mac PPM power-budget overclocking experiments, use the plan agent to generate stress/rollback scripts, and never let an agent auto-run a reboot or SMC/NVRAM-touching command.

---

## 2. Personalized routing for this machine's workload

Observed profile (last 60 days of local OpenCode history): TypeScript/Node + Python FastAPI services, MySQL/Oracle/Postgres/Redis/Memgraph, Azure services and Azure Pipelines, Docker, Playwright/Selenium/Puppeteer RPA, OCR/document AI (including Arabic documents), voicebot/telephony (Kafka, Asterisk ARI), insurance/healthcare domain with strict privacy, some ML (XGBoost/SHAP), and Apple-Silicon power/thermal experiments.

### Recommended role assignment

| Role | Model | Why |
|---|---|---|
| **Daily driver / build** | `deepseek-v4.1-flash` (max) | Proven at your volume; ~25.5k req/mo at your profile ($80 cap); 96% cache hit; native vision |
| **Free workhorse (bulk)** | `deepseek-v4.1-flash-free` / `glm-5.3-flash-free` | Zero-retention free twins; AA 39/42; keep working after Go limits |
| **Explore / repo Q&A / subagents** | `claude-haiku-5-5` or `mimo-v2.6-flash` | Haiku: fastest Claude, 1M ctx, Sonnet-class coding; MiMo-Flash: 33k req/mo, $0.0018/req |
| **Free bulk coding** | `glm-5.3-flash-free` (AA 42) or `beam-free` (AA 30) | Best free intelligence with zero-retention (GLM) or no-training/30-day (Beam) |
| **Bulk edits / boilerplate / tests** | `glm-5.3-flash` / `mimo-v2.6-flash` | Huge allowances; GLM-Flash has the best cheap automation score (AA AutomationBench 60.4) |
| **Plan / architecture** | `grok-4.7`, `mimo-v2.6-pro`, or `gemini-4-argon-contributor` (non-client) | Grok 4.7 verified reasoning; MiMo AA 46 at $0.13/task; Argon AA 53 ⚠️ trains |
| **Hard debugging** | `kimi-k3` | Honesty + SWE-Marathon + 1M context |
| **Frontend / design review** | `muse-spark-1.3-contributor` (non-client) or `kimi-k3` | Design Arena #1 / #3 |
| **Visual QA from screenshots** | `qwen3.8-max` (verification) + `qwen3.8-flash` (loop) | OSWorld #1 overall / cheap sibling |
| **OCR / document AI** | `deepseek-v4.1-flash` or `qwen3.8-flash` | Cheap native vision; Qwen flash is the quality step-up |
| **Marathon autonomous refactor** | `kimi-k3`, escalate to Claude Opus 5.5 via Copilot if it must be one-shot | Verified marathon strength |
| **General research / explanation** | `gemini-4-argon-contributor` (non-client) / `muse-spark-1.3-contributor` / `grok-4.7` | AA 53 / 48 / 46 |
| **Frontier escalation (5% hardest)** | Claude Opus 5.5 / GPT-6 Astra via your GitHub Copilot access, or Zen `claude-opus-5-5` / `gpt-6-astra` | AA 58 / 53; not on Go |

### Hard constraints to respect

1. **Client contract disallows OpenAI models** for at least one computer-vision project → keep GPT-6/5.6 Luna and GPT-6 Astra out of that pipeline; use Gemini/local YOLO/Qwen as configured there.
2. **PHI/medical/insurance data**: avoid models whose provider trains on inputs — **Muse Spark Contributor, Gemini 4 Argon Contributor, Big Pickle, MiMo free, NVIDIA free, LL Alpha**. Note: Contributor SKUs are the *same weights* as the standard models, but discounted SKUs whose terms forbid sensitive/confidential/personal data ([§1b](./06-free-models-and-privacy.md)). Prefer GLM/MiMo paid/Kimi/Qwen/DeepSeek routes — **and the new free DeepSeek/GLM twins state zero-retention**, unlike most free models. DeepSeek's zero-retention is **renewed through October 31, 2026** ✅. Claude Haiku 5.5 has 30-day retention (frontier-API standard) — fine for non-PHI, and it is Anthropic (not OpenAI), so the CV client contract's OpenAI ban doesn't cover it — verify with the client anyway.
3. **Never start servers autonomously** (per your own GEMINI.md rule) — encode this in agent permissions, not in the prompt.
4. **Azure DevOps is your CI** (no GitHub Actions in your repos) — give the agent `az`/`az devops` CLI tools explicitly and keep PAT handling in the environment.
5. **Arabic OCR**: benchmark the top-3 vision models on your own `curenure_ocr_ar` corpus before switching; public benchmarks under-sample Arabic.
6. **This machine now runs OpenCode v2.0.31** — v1-only tooling (OmO Ultimate) needs the OmO Native path or staying pinned on v1.19.x until the dual-host plugin ships.

---

## 3. The escalation ladder (how to actually use this)

```
Task arrives
 ├─ Routine edit / question / explore  → MiMo-V2.6-Flash / Claude Haiku 5.5 (or the free twins)
 ├─ Free agentic coding                 → GLM-5.3-Flash Free / DeepSeek V4.1 Flash Free (zero-retention)
 ├─ Normal feature/build work          → DeepSeek V4.1 Flash (max)
 ├─ Frontend-heavy visual work         → Muse Spark 1.3 / GLM-5.3-Flash (non-client)
 ├─ Needs planning or design           → Grok 4.7 / MiMo-V2.6-Pro / Gemini 4 Argon (non-client)
 ├─ Hard bug / marathon / 1M context   → Kimi K3 (ration: ~180 req/mo)
 ├─ Visual QA / OCR verification       → Qwen3.8 Max (ration: ~250 req/mo)
 └─ Must-not-fail / frontier-level     → Copilot Opus 5.5 / Astra (or Zen overflow)
```

Splitting work this way keeps the expensive allowances for the ~5% of requests that actually need them. In practice: a `plan` call on Grok 4.7 (or Argon on non-client work), a `build` loop on DeepSeek V4.1 Flash, an `explore` agent on Haiku 5.5 / MiMo-Flash, one Kimi K3 review per difficult PR, and the free twins carrying bulk work — close to the ideal Go workflow now that Step 5's free window is gone.

---

**Next:** [04 — Limits & Burn Rate](./04-limits-and-burn-rate.md) · [05 — Intelligence per Dollar](./05-intelligence-per-dollar.md)
