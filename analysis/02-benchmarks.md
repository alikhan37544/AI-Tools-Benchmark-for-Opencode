# 02 — Model Benchmark Dossier (Go Roster)

> **Snapshot: October 1, 2026.** This is the evidence base for every recommendation elsewhere in this repo.
> **Confidence legend:** 🟢 independent multi-source · 🟡 vendor + partial independent · 🔴 vendor-only / unverified.

**The single most important caveat:** benchmark scores are only comparable **within the same version and harness**. Artificial Analysis re-baselined its Intelligence Index to **v4.3.2** in late September 2026; scores quoted from the older v4.1.1 (e.g. Grok 4.6 "61", GLM-5.3-Flash "57") are **not comparable** to today's numbers. Likewise Terminal-Bench 2.1 ≠ 3.0 ≠ 4.0, and every TB4.0 score swings by 10+ points depending on scaffold (vendor agent vs Terminus 2 vs AA harness).

---

## 1. Master table — Intelligence Index v4.3.2 (Artificial Analysis)

Only models with an independent AA run are listed; extras from vendor/other sources are in the per-model sections.

| Model | AA Index v4.3.2 | Speed (tok/s) | TTFT | Cost / AA task | Verbosity | Context | Vision |
|---|---|---|---|---|---|---|---|
| **Muse Spark 1.3** | **48** 🟡 | — | — | — | — | 1M | ✅ |
| **MiMo-V2.6-Pro** | **46** 🟢 | 41.7 | 4.20s | **$0.13** | 140M | 1M | ✅ omni |
| **Grok 4.7** (xhigh) | **46** 🟢 | 72.8 | 44.0s | $3.74 | 240M (verbose) | 500K | ✅ |
| **GLM-5.3** (max) | **45** 🟢 | 67.8 | 3.32s | $2.01 | 71K/task | 1M | ❌ |
| **Qwen3.8 Max** (0902) | **45** 🟢 | 39.1 | 2.94s | $5.41 | — | 1M | ✅ |
| **Kimi K3** (max) | **44** 🟢 | 34.4 | 4.49s | $2.00 | 160M | 1M | ✅ |
| **Grok 4.6** (high) | **44** 🟢 | 67–69 | 42.1s | $1.86 | 36–38K/task | 500K | ✅ |
| **GLM-5.3-Flash** | **42** 🟢 | ~45–200 (provider-dependent) | 3.33s | ~$0.25 | — | 1M | ✅ (in) |
| **DeepSeek V4.1 Flash** (max) | **39** 🟢 | **209–232** | 0.99s | $0.27 | 250M (verbose) | 1M | ✅ |
| **GPT 6 Luna** (max) | **37–38** 🟢 | 125–145 | 109–118s¹ | **$0.07** | 140M | 1.05M | ✅ |
| **DeepSeek V4 Pro 0813** (max) | **36** 🟢 | 96.0 | 1.67s | $0.67 | 160M | 1M | ❌ |
| **GPT 5.6 Luna** | **~35–37** 🟢 | 112 | 0.77s¹ | $0.18 | — | 1.05M | ✅ |
| **GLM-5.2** | **34** 🟢 | 81.5 | 3.13s | $1.47 | — | 1M | ❌ |
| **Hy3** | **~34** 🟡 | — | — | — | — | 256K | ❌ |
| **DeepSeek V4 Flash 0731** | **34–41**² 🟢 | **209** | — | $0.22 | — | 1M | ❌ |
| **MiniMax M3** | **29** 🟢 | 91.2 | 1.56s | $0.51 | — | 1M | ✅ |
| **MiMo-V2.5-Pro** | **26** 🟢 | — | — | — | — | 1M | ✅ omni |
| **Kimi K2.7 Code** | **26** 🟢 | — | — | — | — | 256K | ✅ |
| **MiMo-V2.5** | **25** 🟢 | — | — | — | — | 1M | ✅ omni |
| **Qwen3.7 Plus** | **25** 🟢 | 56.1 | — | $0.22 | — | 1M | ✅ |
| **MiniMax M2.7** | **23** 🟢 | 46.9 | 1.62s | — | — | 205K | ❌ |

¹ Non-reasoning mode TTFT; reasoning TTFT is 109–178s at max effort. ² AA model page says 41; an AA comparison snapshot says 34; a July article said 50. Version drift — treat as ~34–41.
Context scores: Claude Opus 5.5 = 58, Claude Fable 5.1 / GPT-6 Astra / Gemini 4 Argon = 53.

**What this means:** the **best Go model is ~10–12 AA points behind the best model money can buy** (48 vs 58), and the **best cheap Go model is ~9 points behind the best Go model** (39 vs 48). The entire Go premium tier (44–46) sits within noise of each other.

---

## 2. Agentic coding consensus (the table that matters most)

Triangulated across Vals AI, AA, LMArena, Terminal-Bench/vendor harnesses, SWE-bench runs, and the OpenHands Index. Harnesses differ; deltas within ~3 points are noise.

| Rank | Model | Best independent evidence | Notable vendor numbers |
|---|---|---|---|
| 🥇 | **Grok 4.6** | Vals Index 71.8, **SWE-bench Verified 95.6%**, TB2.1 78.3 (Vals) / 88.4 (AA) | DeepSWE 65.2, CursorBench 40.4 |
| 🥈 | **Kimi K3** | **Terminal-Bench 2.1 88.3** (verified), DeepSWE 67.5 (verified), SWE-bench 93.4, SWE-Marathon 42, OSWorld 84.8 | FrontierSWE 81.2, BrowseComp 91.2, MCP-Atlas 84.2 |
| 🥉 | **GLM-5.3 (max)** | TB2.1 88.2, **standardized TB4.0 41.9 (best Go)**, DeepSWE 66.9 | CyberGym 84.5, Z.ai Code Bench 34.5 |
| 4 | **DeepSeek V4.1 Flash** | Vendor DeepSWE 74.2 / TB2.1 90.6; **AA TB4.0 only 26.8** | AutomationBench 54.8, CyberGym 88.1 |
| 5 | **GPT 5.6 Luna** | Vals SWE-bench 93.0, TB2.1 84.7, AA Coding Agent Index 71.5, DeepSWE 67.2 | cheap; weak on TB4.0 |
| 6 | **MiMo-V2.6-Pro** | Table stakes all vendor: TB2.1 89.9, DeepSWE 71.9, AutomationBench 53.1 | AA AutomationBench high; tool-call repetition bug (fixed Sep 25) |
| 7 | **GLM-5.3-Flash** | AA AutomationBench 60.4% (highest Go), AA index 42 | TB2.1 84.3 vendor vs 62.9 Vals — harsh harness gap |
| 8 | **Qwen3.8 Max** | SWE-bench Pro **67.7** (best Go, verified), OSWorld 86.1 (#1 overall) | Terminal-Bench 2.1 86.6 |
| 9 | **LongCat-2.0** | Vendor SWE-bench Pro 59.5, SWE Multilingual 77.3 | completely absent from Western independent boards |
| 10 | **Hy4 preview** | Vendor SWE-bench Pro **65.7**, Toolathlon 74.1 | no AA score yet |
| — | **GPT 6 Luna** | AA TB4.0 13.6, Vals TB4.0 13.6, ProgramBench 0.5 — agentically weak | Vals Index 51.2, cheap |
| — | **Kimi K2.7 Code** | **All six headline benchmarks are first-party**; independent KernelBench showed regression vs K2.6 | treat with suspicion until third-party runs appear |

**The one-line summary:** for *verified* agentic coding, **Grok 4.6, Kimi K3 and GLM-5.3** are the Go frontier; **DeepSeek V4.1 Flash** is the best price/performance agent by a wide margin; **MiMo-V2.6-Pro** is the best "intelligence per dollar at low volume."

---

## 3. Per-model dossier

### 3.1 DeepSeek

**V4.1 Flash** (Sep 10, 2026) — 552B backbone + 196B Engram, 8B active prefill / 16B decode, Causal Encoder-Decoder, CSA2 attention, 890 bytes KV/token (¼ of V4 Flash), 1M ctx, 384K max output, reasoning effort 1–100, native vision, MIT. Trained 45T tokens. [HF card](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash)

| Benchmark | Score | Verdict |
|---|---|---|
| Terminal-Bench 2.1 | **90.6** (DeepSeek card; verified by evals.report) | Best-in-class on TB2.1 |
| Terminal-Bench 3.0 / 4.0 | 30.0 / 31.2 vendor; **26.8 AA** | Hard-harness reality check |
| DeepSWE v1.1 | **74.2** vendor (beats Opus 5's 74.0 in the same table); 65.5 on OpenCode scaffold | Scaffold-sensitive |
| CyberGym | 88.1 | Security/exploit capable (Enclave.ai: "best hacking model") |
| HLE | 36.8 no-tools / **63.9 with tools** | Strong tool-augmented reasoning |
| GPQA-D / Codeforces / AIME-style | 90.9 / 3471 / MathArena Apex 65.6 | |
| Vision | MMMU-Pro 56.5, DocVQA 95.6, Chartography 78.9 | Native multimodal |
| AA Index | **39** | #7 in class; 209–232 tok/s (#3 overall) |

**V4 Pro 0813** (Aug 13) — 1.6T/49B MoE, 1M ctx, MIT, no vision. AA **36**, 96 tok/s, $0.67/task. Vendor: SWE-bench Verified 80.6, SWE Pro 55.4, TB2.0 67.9 / TB2.1 87.9, HLE 42.7/60.0 tools, MRCR-1M 83.5, MMLU-Pro 87.5, LiveCodeBench 93.5, BrowseComp 83.4. **DeepSeek retired V4 Pro from its own API on Sep 14 and routed traffic to V4.1 Flash**; Go still lists it separately, but verify what is actually served.

**V4 Flash 0731** (Jul 31) — 284B/13B, text-only, upstream-retired Sep 10. AA 34–41, 209 tok/s. Vendor TB2.1 82.7, DeepSWE 54.4.

**V4 Flash Vision Exp** (Aug 21) — experimental vision variant, also retired upstream Sep 10, but still on Go at a $15 allowance. Vendor TB2.1 83.9, NL2Repo 57.7, DeepSWE 59.3.

**Community:** launch thread very positive ("better than V4 Pro"), but users note the reasoning-token burn; pricing rose sharply vs the old V4 Flash. Enclave.ai's security team adopted it. OpenCode telemetry shows it as the #2 model by tokens across the entire user base — it is the crowd's workhorse.

---

### 3.2 Xiaomi MiMo

**MiMo-V2.6-Pro** (Sep 21) — 1.02T/42B sparse MoE, 70 layers, 1M ctx, **native text+image+video+speech**, MIT. AA Intelligence Index **46 — #1 of all open-weight models in its class**; $0.13/AA task (cheapest frontier-class), 41.7 tok/s (slow), 4.2s TTFT.

Vendor table (with Opus 5 / GPT-5.6 Sol in the same table): DeepSWE 71.9, **TB2.1 89.9**, TB4.0 34.9, ProgramBench 26.5, AutomationBench 53.1, OSWorld 82.0, GDPval-AA 2.1 1673, CyberGym 94.0.

⚠️ **Known issue:** Xiaomi's own Sept 27 post documents **tool-call repetition** (OpenCode: Flash 1.02%, Pro 0.54% of turns; up to 41.7% of replayed MiMo-Code samples flooded with ≥10 tool calls/turn). Fixed via MOPD distillation, API updated Sept 25. Also poor p95 TTFT (9.1s) on Xiaomi's API. [Post](https://mimo.xiaomi.com/blog/mimo-v2-6-tool-call-repetition)

**MiMo-V2.6-Flash** — smaller RL sibling; 67.9 DeepSWE, 87.6 TB2.1 (vendor), narrowly beat its Pro sibling on an 8-task hands-on KingBench (7.25 vs 6.94). **No AA score yet — the biggest unmeasured value on the roster** ($60 cap, $0.28/M output).

**MiMo-V2.5 / Pro** — previous generation; V2.5-Pro is far behind (DeepSWE 19.0 vs 71.9), AA 25/26. Only useful as volume filler.

---

### 3.3 Z.ai GLM

**GLM-5.3** (Aug 18; weights Aug 28) — 753B/40B MoE, same base as 5.2 + post-training, 1M ctx, **text-only**, always-on reasoning (low/high/max, default max), commercial-restricted license. AA **45** (#2 open weights), 67.8 tok/s, $2.01/task.

| Benchmark | 5.3 | 5.2 |
|---|---|---|
| Terminal-Bench 2.1 | — | 81.0 vendor |
| Terminal-Bench 3.0 (vendor) | **28.3** | 4.6 |
| TB 3.0 on AA-equivalent scale | 41.9 standardized (best Go) | — |
| DeepSWE v1.1 | 66.9 | 46.2 |
| SWE-bench Pro | — | 62.1 |
| CyberGym | 84.5 | 77.2 |
| Agents' Last Exam | 28.5 | 23.8 |
| Z.ai Code Bench | 34.5 @75K tok | 23.4 @96K |
| LMArena text | 1479 (#26) | 1475 (#32) |

⚠️ NIST/CAISI (via Anthropic) named GLM-5.3 "the most cyber-capable open-weight model released to date," ~4 months behind the US frontier. Strengths: terminal/agentic + cyber. Weaknesses: no vision, always-reasoning (expensive), verbose, 7%+ hallucination per HN users.

**GLM-5.3-Flash** (Aug 26) — 320B/18B MoE, **MIT**, native multimodal (text/image/video/file in), sparse+linear attention, ~4.4× smaller KV cache. AA **42** at ~$0.25/task, **AA AutomationBench 60.4%** (highest of any Go model), vendor TB2.1 84.3 but Vals only 62.9 — provider quantization/harness variance is the caveat. Fast (up to 200 tok/s on FlashX). This is the **best cheap generalist on the roster**.

**GLM-5.2** (Jun 16) — 753B/40B, MIT, 1M ctx; AA 34. Superseded; only interesting for its documented Terminal-Bench/SWE-bench Pro numbers.

---

### 3.4 xAI Grok

**Grok 4.7** (Sep 21) — proprietary, 500K ctx, vision, reasoning low→xhigh (default high), encrypted reasoning on Responses API. AA **46**; but 44s TTFT, 81K output tokens/index task (240M total — "very verbose"), $3.74/task. Vendor: CursorBench 4.0 46.3, DeepSWE 71.0, TB4.0 37.6 (xAI) / 33 (AA), EEBench 64.0 (electrical engineering), Harvey Legal 19.6, HealthBench Prof 56.7. **LMArena ranks it BELOW Grok 4.6** (1442 vs 1453); Design Arena 1224 (weak). Reads as a reasoning/knowledge specialist that over-spends tokens.

**Grok 4.6** (Aug 12) — likely the **best all-round Go agent**: AA 44, Vals Index **71.8**, **SWE-bench Verified 95.6** (Vals), TB2.1 78.3 Vals / 88.4 AA, LiveCodeBench 88.2, GPQA Diamond **95.0** (#5 globally), **ARC-AGI-2 67.1** (#2 among Go), GDPval-AA 1605–1773. Weaknesses: 42s TTFT at high effort, 500K ctx (smaller than 1M rivals), noisier serving.

**Grok 4.5** (context, not on Go) — AA 39, LMArena #48.

---

### 3.5 Moonshot Kimi

**Kimi K3** (Jul 16) — **2.8T total / 104B active** (16 of 896 experts), 93 layers (KDA + Gated MLA), MoonViT-V2 vision, 1M ctx, MXFP4 QAT, always-thinking (low/high/max), open weights under the Kimi K3 license (commercial restrictions; >$20M MaaS needs a deal). [HF card](https://huggingface.co/moonshotai/Kimi-K3) — **1.27M downloads/month, 11.6k likes, 53 quantizations.**

Highlights (max): GPQA 93.5, HLE 43.5/56.0 tools, DeepSWE 67.5, TB2.1 88.3, **SWE-Marathon 42.0** (ahead of Fable 5 35, Opus 4.8 40, GPT-5.6 Sol 39), FrontierSWE 81.2, BrowseComp 91.2, OSWorld 84.8, MMMU-Pro 81.6, MCP-Atlas 84.2, Toolathlon 76.5, **#1 Front-end Code Arena (1679)**, ARC-AGI-2 60.4. AA **44** but slow (34.4 tok/s), $2.00/task, verbose (160M tokens).

Author-declared weaknesses: **sensitivity to thinking history** (harness must return all `reasoning_content` or quality destabilizes), "excessive proactiveness," and an explicit "noticeable gap in user experience" vs Fable 5 / GPT-5.6 Sol. Community: enormous HN reception; Moonshot suspended new subscriptions due to demand; UK AISI/CAISI published a preliminary cyber assessment.

**Kimi K2.7 Code** (Jun 12) — 1T/32B, 256K ctx, thinking-only, ~30% fewer thinking tokens than K2.6. Vendor deltas: Kimi Code Bench v2 62.0 (vs 50.9), Program Bench 53.6 (48.3), MCP Atlas 76.0 (69.4). **But:** no independent runs, and an independent KernelBench-Hard test showed *regression* vs K2.6 (0.157 vs 0.222) — "more honest but not more capable."

**Kimi K2.6** (Apr 20) — 1T-class/32B, 256K. HLE 54.0 no-tools, GPQA 88.4, AIME 2026 93.3, SWE-bench Pro 58.6, TB2.0 66.7. Solid but superseded.

---

### 3.6 Alibaba Qwen

**Qwen3.8 Max** (Aug 3; 0902 snapshot) — 2.4T/95B, 1M ctx, text+image(+video), reasoning xhigh/medium/low. Prices: $2/$6. AA **45** but **39 tok/s and $5.41/task — the most expensive Go model per unit of work**. Verified highlights: **SWE-bench Pro 67.7 (best Go)**, Terminal-Bench 2.1 86.6, **OSWorld 86.1 (#1 overall model on the benchmark)**, MMMU-Pro 82.3, IFBench 82.8, LMArena WebDev **1688 (#2)**, LMArena Vision **1302 (#2)**, ScreenSpot-Pro 84.5 (top Go). Vendor long-horizon demos: 16-day autonomous repo (265 commits), 24h contest beating 458/526 human teams.

**Qwen3.8 Flash** (Aug 26) — 125B + 51B N-gram embeddings, **6B active**, 262K native → 1M, multimodal, "preview of Qwen4 architecture," ~1/9 the training compute of 3.7 Plus. Vendor: AndroidWorld 84.5, RealWorldQA 88.5, MathVision 90.6, CharXiv 84.6, CoWorkBench 73.9. **No independent AA score or official benchmark table yet** — promising, unproven.

**Qwen3.7 Plus** (May 31) — 1M ctx, multimodal. AA 25. LMArena WebDev 1541, LMArena 1474. Volume model.

---

### 3.7 OpenAI GPT Luna

**GPT 6 Luna** (Sep 22) — 1.05M ctx, 128K out, effort none→max, vision, computer-use, hosted shell. $0.10/$0.50. AA **37–38**, **$0.07/AA task (cheapest frontier-lab model)**, 125–145 tok/s. Vendor: DeepSWE 66.6, AutomationBench 20.7, Agents' Last Exam 50.9, FrontierCode 42.4, OSWorld 52.7, factual error rate 7.6%. Vals: index 51.2, **TB4.0 13.6, ProgramBench 0.5** — agentically weak.

**GPT 5.6 Luna** (Jul 9) — AA ~35–37, Vals SWE-bench **93.0**, TB2.1 84.7, AA Coding Agent Index 71.5, DeepSWE 67.2, HLE 39, ARC-AGI-2 59.5, AIME high. Community on r/opencode: "not good for long tasks / large codebase"; some prefer DeepSeek V4 Flash. Good as a cheap second opinion, not a marathon agent.

**Context (not on Go):** GPT-6 Astra (AA 53, ARC-AGI-2 95, WebDev 1792, Design Arena 64% win rate), GPT-6 Sol (AA 47–48), GPT-6.1 Sol (AA 52). These are the "pay for the jump" targets via Zen.

---

### 3.8 Meta Muse Spark

**Muse Spark 1.3 Contributor** (Sep 2) — proprietary, 1M ctx, multimodal (video/images/docs), max reasoning. AA **48 — the highest-rated model available on Go** (per two independent aggregation sources; medium confidence). Design Arena **Website #1 (1362–1365)**, LMArena WebDev 1623 AutoEval, LMArena text ~1537, **MRCR v2 8-needle 512K–1M = 98.1** (self-reported), OSWorld 2.0 strong, JobBench 64.9, GDPval-AA 1754 (vs Opus 5 1824, GPT-5.6 Sol 1710). [Meta model page](https://dev.meta.ai/models/muse-spark)

⚠️ **Contributor tier trains on your prompts/completions.** Not suitable for client/PHI work.

**Muse Spark 1.2** (Aug 5) — AA ~45–46, Design Arena 1318, LMArena coding 1533.

---

### 3.9 Tencent Hunyuan

**Hy4 preview** (Aug 28) — 770B/49B + 10B MTP, 78 layers, 1M ctx, **Apache 2.0**, thinking defaults high. Official blind eval: 2.99 avg vs GLM-5.3 2.92 and Kimi K3 2.94 (203 tasks, 163 Tencent experts). Vendor card: **SWE-bench Pro 65.7 (#9)**, MCP-Atlas 83.7, Toolathlon 74.1, GPQA 92.3 (unverified), SWE Multilingual 82.9 (unverified). **No AA score.** Official known issues: over-reasoning and over-verification. At $0.834/$2.501 it is the most expensive cheap-tier model on Go.

**Hy3** (Apr 22) — 295B/21B, 256K, community license. GPQA 87.2, **SWE-bench Verified 74.4**, TB2.0 54.4, HLE 30. AA ~34. Old but proven; good volume filler.

---

### 3.10 Meituan LongCat

**LongCat-2.0** (Jun 30) — 1.6T/~48B + 135B N-gram embedding params, LongCat Sparse Attention, native 1M ctx, **MIT**. Vendor: TB2.1 70.8, **SWE-bench Pro 59.5, SWE Multilingual 77.3**, FORTE 73.2, BrowseComp 79.9, GPQA-D 88.9. Trained entirely on a 50k-card domestic AI-ASIC superpod. No AA score, no Western independent runs. Cheap ($0.30/$1.20, $0.006 cache).

**LongCat 2.5 Preview** — free on Go/Zen, zero-retention per OpenCode. **No public model card, benchmarks, or even provider announcement** as of Oct 1.

---

### 3.11 MiniMax

**MiniMax M3** (Jun 1) — 428B/23B, MSA sparse attention, 1M ctx, open weights (community license, commercial-restricted), multimodal. Vendor: SWE-bench Pro 59.0, TB2.1 66.0, BrowseComp 83.5, **OSWorld-Verified 70.06**, PostTrainBench 37.1 (#3 behind Opus 4.7/GPT-5.5), 24h CUDA FP8 GEMM 9.4× speedup. **AA only 29** — vendor claims far outrun independent measurement. Low hallucination reputation (HN: 18% vs ~30% for Grok/GLM/Muse).

**MiniMax M2.7** (Mar 18) — 230B/10B, non-commercial license, 205K ctx. Vendor: SWE-Pro 56.2, SWE Multilingual 76.5, TB2 57.0, **MLE-bench Lite 66.6% medal rate (best Go data/ML signal)**, GDPval-AA 1495. AA 23. Niche use: data science workflows.

---

### 3.12 Stealth models

**Space Bunny (Free)** — #1 model by tokens on all of OpenCode (58T/week), +596% growth. 1M ctx, multimodal, mandatory reasoning. Fingerprint analysis (3 independent tests) points to **MiniMax family, possibly M3.1-Flash-Preview**; community also speculates Gemini 3.8 Flash (a Google logo appeared in Go's provider list). OpenCode route: zero-retention/no-training; OpenRouter route differs. Users report strong web design, speed, reliability — and a tool-param wrapping bug. [OrcaRouter write-up](https://www.orcarouter.ai/blog/space-bunny), [OpenRouter listing](https://openrouter.ai/stealth/space-bunny-alpha).

**Big Pickle** (Zen only) — stealth, **data used for training during free period**. arXiv audit (Aug 31) suggests a GLM-5/5.1 pool with 200K context; other evidence points at DeepSeek routing. Unknown; do not trust with sensitive code.

---

## 4. Benchmark-source health (as of Oct 1, 2026)

| Source | Status | Notes |
|---|---|---|
| Artificial Analysis | 🟢 healthy | v4.3.2 re-baselined; best cross-vendor scale |
| LMArena | 🟢 healthy | Text/coding/WebDev/Vision updates; overall Sep 28 snapshot |
| Vals AI | 🟢 healthy | Independent; strong on TB/Code Migration |
| SWE-bench official | 🟡 partial | JS board only renders headers for many rows; numbers circulate via mirrors |
| Terminal-Bench official | 🟡 partial | TB2.1 renders; **TB4.0 table empty** |
| Aider Polyglot | 🔴 frozen | No new entries since Aug 2025 — useless for current models |
| LiveCodeBench official | 🔴 broken | "Loading leaderboard data…" indefinitely; mirrors used |
| METR time-horizon | 🟡 stale | Last update May 8, 2026; **no Go model measured**; >16h unreliable |
| Epoch AI | 🟡 partial | Only GLM-5.3 among Go models has a public run |
| OpenHands Index | 🟡 lagging | Latest is GLM-5.1/MiniMax M3/Kimi K2.6 era |
| Design Arena / WebDev Arena | 🟢 healthy | Go models rank very well here |
| ARC Prize | 🟢 healthy | Covers Grok/Kimi/GPT-Luna; missing GLM/Qwen/DeepSeek |
| HuggingFace Open LLM Leaderboard | 🔴 archived | Final snapshot; use HF model cards/downloads instead |

---

## 5. Final consensus rankings

**Overall intelligence (Go only):**
1. Muse Spark 1.3 (48) 🟡 · 2. MiMo-V2.6-Pro / Grok 4.7 (46) · 4. GLM-5.3 / Qwen3.8 Max (45) · 6. Kimi K3 / Grok 4.6 (44) · 8. GLM-5.3-Flash (42) · 9. DeepSeek V4.1 Flash (39) · 10. GPT 6 Luna (37–38) · 11. GPT 5.6 Luna (35–37) · 12. DeepSeek V4 Pro (36) · then GLM-5.2/Hy3/DeepSeek V4 Flash (~34), MiniMax M3 (29), MiMo-V2.5 (25–26), Kimi K2.7 (26), Qwen3.7 Plus (25), MiniMax M2.7 (23).

**Agentic coding (Go only, independent-evidence weighted):**
1. Grok 4.6 · 2. Kimi K3 · 3. GLM-5.3 · 4. DeepSeek V4.1 Flash (value king) · 5. GPT 5.6 Luna · 6. Qwen3.8 Max · 7. MiMo-V2.6-Pro · 8. GLM-5.3-Flash.

**Design/frontend:** Muse Spark 1.3 > Kimi K3 > GLM-5.3 > MiMo-V2.6-Pro > Qwen3.8 Max. **Value:** GLM-5.3-Flash.

**Vision/visual QA:** Qwen3.8 Max (OSWorld #1, LMArena Vision #2, ScreenSpot 84.5) > Kimi K3 > Muse Spark 1.3 > MiMo-V2.6-Pro > Qwen3.8 Flash. For OCR specifically: Qwen3.8 Max/Flash, DeepSeek V4.1 Flash (DocVQA 95.6).

---

**Next:** [03 — Task Playbook](./03-task-playbook.md) · [04 — Limits & Burn Rate](./04-limits-and-burn-rate.md)
