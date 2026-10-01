# 03 — Task Playbook: Best Model for Each Kind of Work

> **Snapshot: October 1, 2026.** Picks are for the **Go** roster. Where the true best model is not on Go, that's noted and the best Go alternative is given.
> Evidence symbols: 🟢 independent · 🟡 mixed/vendor+partial · 🔴 vendor-only.

---

## 0. The master table

| # | Task category | Best on Go | Runner-up | Best value pick | Best overall (not on Go) | Key evidence |
|---|---|---|---|---|---|---|
| 1 | **Backend/API, refactors, migrations** | Kimi K3 (marathon) / DeepSeek V4.1 Flash (daily) | GLM-5.3 | **DeepSeek V4.1 Flash** | Claude Opus 5.5 | DS: DeepSWE 74.2, TB2.1 90.6 🟡; K3: SWE-Marathon 42.0, FrontierSWE 81.2 🟡 |
| 2 | **Frontend/UI (React, Tailwind, shadcn)** | **Muse Spark 1.3** | Kimi K3 | GLM-5.3-Flash | GPT-6 Astra / Fable 5.1 | Design Arena website #1 (1365), K3 #3 (1345) 🟢 |
| 3 | **Database / SQL** | GLM-5.3 / GLM-5.2 | DeepSeek V4.1 Flash | GLM-5.3-Flash | Gemini-3-Pro + agent harness | Spider 2.0-Lite #1 agent used GLM-5.2 (76.2) 🟡 |
| 4 | **Integration (3rd-party APIs, auth, webhooks, Kafka)** | Kimi K3 | Hy4 preview | DeepSeek V4.1 Flash | Claude Opus 5 | MCP-Atlas: K3 84.2, Hy4 83.7, Opus 5 85.7 🟡; Toolathlon Hy4 74.1 🟡 |
| 5 | **Agentic terminal / DevOps / git / deploy** | Grok 4.6 (verified) / DeepSeek V4.1 Flash (volume) | GLM-5.3 (best TB4.0: 41.9) | **GLM-5.3-Flash** | GPT-6 Astra / Opus 5.5 | Vals: Grok 4.6 SWE-bench 95.6, TB2.1 78.3; DS TB2.1 90.6 🟡 |
| 6 | **Long-horizon autonomy (multi-hour, self-directed)** | Kimi K3 | DeepSeek V4 Flash | DeepSeek V4.1 Flash | Claude Opus 4.6+ (METR ~12h) | LHTB #1 DS V4 Flash 0.602; K3 0.378; METR has no Go model 🟡 |
| 7 | **Visual QA / browser + GUI agents (Playwright)** | **Qwen3.8 Max** | Kimi K3 | Qwen3.8 Flash | GPT-6 Astra (grounding) | OSWorld-Verified: Qwen3.8 Max 86.1 (#1 overall), K3 84.8 🟢 |
| 8 | **Image analysis / OCR / charts / screenshot→code** | **Qwen3.8 Max** | Kimi K3 / MiMo-V2.6-Pro | Qwen3.8 Flash / DeepSeek V4 Flash Vision | GPT-6 Astra / Gemini 3.x | LMArena Vision Qwen3.8 #2, MMMU-Pro 82.3 🟢 |
| 9 | **Planning / architecture reasoning** | Grok 4.6 | Muse Spark 1.3 / MiMo-V2.6-Pro | GLM-5.3-Flash | GPT-6 Astra | GPQA-D Grok 4.6 95.0 (#5); ARC-AGI-2 67.1 🟢 |
| 10 | **Debugging / root-cause analysis** | Kimi K3 (honesty) / Grok 4.7 (edge cases) | DeepSeek V4.1 Flash | GLM-5.3-Flash | Claude Opus 5.5 | honesty battery: K3 0/12 false "done"; Grok 4.6 0/12 but 5/6 silent compliance 🟡 |
| 11 | **Long context (huge repos, logs)** | DeepSeek V4 Pro (MRCR-1M 83.5 🟢) | Kimi K3 (1M native, AA-LCR 74.7) / Muse Spark 1.3 (MRCR 98.1 self-report 🟡) | DeepSeek V4.1 Flash | GPT-6 Astra / Opus 4.6 | MRCR-1M: V4 Pro 83.5, V4 Flash 78.7 🟢 |
| 12 | **Fast/cheap bulk edits, boilerplate, tests** | **MiMo-V2.6-Flash / DeepSeek V4.1 Flash** | GLM-5.3-Flash | either | GPT-6 Luna ($0.07/task) | session cost: MiMo-Flash $0.0034, DS $0.078 🟢 (OpenCode telemetry) |
| 13 | **General intelligence / research / explanation** | Muse Spark 1.3 (48) | MiMo-V2.6-Pro / Grok 4.7 (46) | GLM-5.3-Flash | Claude Opus 5.5 (58) / GPT-6 Astra (53) | AA v4.3.2 🟢 |
| 14 | **Data / analysis / ML notebooks (pandas, XGBoost, SHAP)** | MiniMax M2.7 (MLE-bench) / Kimi K3 | Qwen3.8 Flash | DeepSeek V4.1 Flash (Python) | Gemini-3-Pro agents | MLE-bench Lite M2.7 66.6% medal 🟡; official board led by Gemini agents 🟢 |
| 15 | **Systems/hardware (overclocking, ROMs, drivers, homelab)** | Grok 4.6 / Kimi K3 | MiMo-V2.6-Pro | DeepSeek V4.1 Flash | GPT-6 Sol / Opus 5.5 | Grok EEBench 64.0 🟡; MiMo Pro 23/23 hidden checks vs Opus 5 in OpenCode 🟡 |
| 16 | **Voicebot / realtime / telephony debugging** | DeepSeek V4.1 Flash | Kimi K3 | MiMo-V2.6-Flash | — (audio models are separate) | no dedicated bench; integration + debugging proxies |
| 17 | **Repo Q&A / explore subagent (cheap, high volume)** | **MiMo-V2.6-Flash** | GLM-5.3-Flash | either | — | 33k req/mo capacity at your profile; $0.0018/req |
| 18 | **Spec/plan writing before implementation** | Grok 4.6 | Muse Spark 1.3 | GLM-5.3-Flash | Opus 5.5 | planning = GPQA/ARC plus AA-Briefcase |

---

## 1. Category notes and caveats

### Backend / API / refactors
- **DeepSeek V4.1 Flash** is the best daily driver: 209–232 tok/s, 1M ctx, native vision, 96% cache ratio, and a DeepSWE 74.2 vendor run that edges Opus 5's 74.0 in the same table. Its honest weakness is hard long-horizon benchmarks: AA's standardized TB4.0 gives it only 26.8. Short-to-medium agent loops: excellent. Multi-hour marathon: escalate.
- **Kimi K3** is the marathon pick (SWE-Marathon 42.0 beat Fable 5 35 and GPT-5.6 Sol 39). Caveat: harness must preserve reasoning history.
- **GLM-5.3** is the best *standardized* Terminal-Bench 4.0 performer on Go (41.9) — the pick when "it must survive a hard harness."

### Frontend / UI
- **Muse Spark 1.3** tops Design Arena's website board and is #5 by lab on WebDev Arena; Kimi K3 is within ~15–20 Elo and stronger on complex app code. Both use vendor agent settings; treat the gap as small.
- **GLM-5.3-Flash** ranks top-20 in WebDev frontend at $0.15/$0.50 with a $60 allowance — the "good enough frontend at 30k requests/month" pick.
- GPT-6 Astra (1800 WebDev) is the true leader; Fable 5.1/Opus 5.5 (1758/1687) follow.

### Database / SQL
- Spider 2.0's board ranks *agent systems*, not raw models. The #1 Lite entry used **GLM-5.2**; Snow entries use Gemini-3-Pro and Claude Sonnet agents. GLM-5.3 inherits 5.2's strengths (Terminal-Bench 81.0, SWE-bench Pro 62.1) plus better reasoning.
- Practical rule: for schema/migration reasoning use GLM-5.3; for query iteration loops use DeepSeek V4.1 Flash (cheap + fast); always run migrations through the plan agent with the DB MCP/tool, not freehand.

### Integrations
- **MCP-Atlas** is the closest proxy: Kimi K3 84.2, Hy4 preview 83.7, DS V4 Pro 82.5, GLM-5.3/Qwen3.8 Max 81.9, Opus 5 85.7. Hy4's **Toolathlon-Verified 74.1** is the best Go tool-use signal.
- For auth/webhook debugging there is no dedicated benchmark; model quality on code + tool use is the proxy. Kimi K3/Hy4 first, DeepSeek for volume.

### Agentic terminal / DevOps / git / deploy
- The independent split: **Grok 4.6** wins Vals-style harnesses (SWE 95.6, TB2.1 78.3); **GLM-5.3** wins standardized TB4.0 (41.9); **DeepSeek V4.1 Flash** wins vendor TB2.1 (90.6) and throughput, but drops to 26.8 on TB4.0.
- For **Azure CLI / `az ssh` / Docker / CI pipelines**, favor models that are strong in terminal loops *and* cheap enough to iterate: DeepSeek V4.1 Flash for the loop, GLM-5.3 or Grok 4.6 for the planning step. Never auto-run destructive deploy commands without permission gates (see `07-recommended-config.md`).

### Long-horizon autonomy
- The cleanest public signal is **LHTB** (Long-Horizon Task Benchmark): DeepSeek V4 Flash #1 (0.602 mean reward), Grok 4.5 0.505, MiniMax M3 0.385, Kimi K3 0.378, Kimi K2.7 0.367. Caveat: custom harness.
- METR's time-horizon evals show the true frontier at ~12h p50 (Opus 4.6) and **no Go model has a published measurement**. If a task is truly "walk away for 8 hours," budget for escalation to a frontier non-Go model.

### Visual QA / browser agents
- **Qwen3.8 Max is the #1 model in the world on OSWorld-Verified (86.1)**, above Fable 5/Mythos 5 (85). Its ScreenSpot-Pro 84.5 is the top Go result; LMArena Vision #2.
- Kimi K3 (84.8 OSWorld) and MiMo-V2.6-Pro (82.0) follow. For Playwright screenshot-diff loops, Qwen3.8 Max is worth its small $15 allowance for final verification runs; run the bulk loop on Qwen3.8 Flash or DeepSeek vision.

### Image analysis / OCR
- **Qwen3.8 Max** (MMMU-Pro 82.3, DocVQA-class vision, LMArena Vision #2) is the best Go vision model; **Qwen3.8 Flash** is the 6B-active value version; **MiMo-V2.6-Pro** accepts image+video+speech and has 1M ctx.
- For document OCR at volume, **DeepSeek V4.1 Flash** (DocVQA 95.6, 96% cache ratio, $0.60/M output) is the cheapest competent option — and note Go's `deepseek-v4-flash-vision-exp` now effectively aliases the V4.1 family after DeepSeek's Sep 10 API consolidation.
- For Arabic OCR/translation, no public benchmark separates models; test candidates on your own corpus (Qwen3.8 Max/Flash, MiMo, Kimi K3).

### Planning / architecture
- Grok 4.6 has the strongest independent reasoning evidence (GPQA 95.0, ARC-AGI-2 67.1). Muse Spark 1.3 leads the AA index and is strong at brief-writing; MiMo-V2.6-Pro is the value pick.
- Use the `plan` agent with a premium model, then hand the plan to a cheap model for execution (see config).

### Debugging / RCA
- The **agent-honesty battery** is the most relevant small study: Kimi K3 had 0/12 false "fixed" claims and 0/6 silent compliance; Grok 4.6 never lied but silently obeyed contradictory instructions 5/6 times; DeepSeek V4 Flash and GLM-5.2 each had 1/12.
- Practical: Kimi K3 for root-cause honesty; Grok 4.7 for edge-case precision; DeepSeek V4.1 Flash for the cheap iteration loop.

### Long context
- Independently tracked 1M retrieval: DeepSeek V4 Pro MRCR-1M **83.5**, V4 Flash 78.7. Muse Spark 1.3 self-reports 98.1 on MRCR v2 8-needle 512K–1M (no independent track). Kimi K3 has native 1M + AA-LCR 74.7.
- Beware: long contexts burn cache-reads; DeepSeek's $0.003/M cache makes it the cheapest way to feed a huge repo.

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
| **Daily driver / build** | `deepseek-v4.1-flash` (max) | Already proven at your volume; 19k req/mo capacity at your profile; 96% cache hit; native vision |
| **Explore / repo Q&A / subagents** | `mimo-v2.6-flash` | 33k req/mo capacity, $0.0018/req, 95% cache ratio, 1M ctx |
| **Bulk edits / boilerplate / tests** | `glm-5.3-flash` or `mimo-v2.6-flash` | Huge allowances; GLM-Flash has the best cheap automation score (AA AutomationBench 60.4) |
| **Plan / architecture** | `grok-4.6` or `mimo-v2.6-pro` | Best independent reasoning (GPQA 95.0, ARC 67.1) / AA 46 at $0.13/task |
| **Hard debugging** | `kimi-k3` | Honesty + SWE-Marathon + 1M context |
| **Frontend / design review** | `muse-spark-1.3-contributor` (non-client work) or `kimi-k3` | Design Arena #1 / #3 |
| **Visual QA from screenshots** | `qwen3.8-max` (verification) + `qwen3.8-flash` (loop) | OSWorld #1 overall / cheap sibling |
| **OCR / document AI** | `deepseek-v4-flash-vision-exp` or `qwen3.8-flash` | Cheap native vision; Qwen flash is the quality step-up |
| **Marathon autonomous refactor** | `kimi-k3`, escalate to Claude Opus 5.5 via Copilot if it must be one-shot | Verified marathon strength |
| **General research / explanation** | `muse-spark-1.3-contributor` or `grok-4.7` | AA 48 / 46 |
| **Frontier escalation (5% hardest)** | Claude Opus 5.5 / GPT-6 Astra via your GitHub Copilot access, or Zen `claude-opus-5-5` / `gpt-6-astra` | AA 58 / 53; not on Go |

### Hard constraints to respect

1. **Client contract disallows OpenAI models** for at least one computer-vision project → keep GPT-6/5.6 Luna and GPT-6 Astra out of that pipeline; use Gemini/local YOLO/Qwen as configured there.
2. **PHI/medical/insurance data**: avoid models whose provider trains on inputs — **Muse Spark Contributor, Big Pickle, MiMo free, NVIDIA free, Ling free**. Prefer GLM/MiMo paid/Kimi/Qwen/DeepSeek routes, and re-verify DeepSeek's zero-retention renewal (its ZDR page listed validity "through September 30, 2026").
3. **Never start servers autonomously** (per your own GEMINI.md rule) — encode this in agent permissions, not in the prompt.
4. **Azure DevOps is your CI** (no GitHub Actions in your repos) — give the agent `az`/`az devops` CLI tools explicitly and keep PAT handling in the environment.
5. **Arabic OCR**: benchmark the top-3 vision models on your own `curenure_ocr_ar` corpus before switching; public benchmarks under-sample Arabic.

---

## 3. The escalation ladder (how to actually use this)

```
Task arrives
 ├─ Routine edit / question / explore  → MiMo-V2.6-Flash  (free-ish volume)
 ├─ Normal feature/build work          → DeepSeek V4.1 Flash (max)
 ├─ Frontend-heavy visual work         → Muse Spark 1.3 / GLM-5.3-Flash (non-client)
 ├─ Needs planning or design           → Grok 4.6 / MiMo-V2.6-Pro (plan agent)
 ├─ Hard bug / marathon / 1M context   → Kimi K3 (ration: ~180 req/mo)
 ├─ Visual QA / OCR verification       → Qwen3.8 Max (ration: ~250 req/mo)
 └─ Must-not-fail / frontier-level     → Copilot Opus 5.5 / Astra (or Zen overflow)
```

Splitting work this way keeps the expensive allowances for the ~5% of requests that actually need them. In practice: a `plan` call on Grok 4.6, a `build` loop on DeepSeek V4.1 Flash, an `explore` agent on MiMo-V2.6-Flash, and one Kimi K3 review per difficult PR is close to the ideal Go workflow.

---

**Next:** [04 — Limits & Burn Rate](./04-limits-and-burn-rate.md) · [05 — Intelligence per Dollar](./05-intelligence-per-dollar.md)
