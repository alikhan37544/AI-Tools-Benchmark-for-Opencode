# 02 — Model Benchmark Dossier (Go Roster)

> **Snapshot: October 1, 2026; refreshed October 13, 16 and 25.** New Oct 25 sections: **§3.13 Kimi K3.1 Pro**, **§3.14 MiniMax M3.1 Flash**; Gemini 4 Argon's privacy status corrected; Space Bunny and LongCat 2.5 removed; benchmark corrections applied (Hy3, LongCat-2.0, Muse Spark 1.2); consensus rankings (§5) rebuilt.
> **Confidence legend:** 🟢 independent multi-source · 🟡 vendor + partial independent · 🔴 vendor-only / unverified. **Legacy** = retired upstream or removed from Go docs — still billed on Zen, but avoid for new work.
>
> 🆕 **Oct 25 — the new stuff:** **Kimi K3.1 Pro (AA 55.1)** is the highest-intelligence model ever listed on Go; **MiniMax M3.1 Flash (AA 43 at $0.22/task)** is the new cheap-workhorse leader. **Gemini 4 Argon** is now documented **0-day retention / not used for training** — the old Contributor-training warning was wrong.

**The single most important caveat:** benchmark scores are only comparable **within the same version and harness**. Artificial Analysis re-baselined its Intelligence Index to **v4.3.2** in late September 2026; older v4.1.1 scores (e.g. Grok 4.6 "61", GLM-5.3-Flash "57") are **not comparable**. Terminal-Bench 2.1 ≠ 3.0 ≠ 4.0, and every TB4.0 score swings by 10+ points depending on scaffold.

---

## 1. Master table — Intelligence Index v4.3.2 (Artificial Analysis)

Only models with an independent AA run are listed; vendor/other source extras are in the dossier.

| Model | AA Index v4.3.2 | Speed (tok/s) | TTFT | Cost / AA task | Verbosity | Context | Vision |
|---|---|---|---|---|---|---|---|
| **Kimi K3.1 Pro** ✨ | **55.1** 🟢 | 57.5 | 3.07s | **$2.11** | 150M | 1M | ✅ |
| **Gemini 4 Argon** | **53** 🟢 | — | — | — (50% off) | — | 1M | ✅ |
| **Muse Spark 1.3** | **48** 🟡 | — | — | — | — | 1M | ✅ |
| **MiMo-V2.6-Pro** | **46** 🟢 | 41.7 | 4.20s | **$0.13** | 140M | 1M | ✅ omni |
| **Grok 4.7** (xhigh) | **46** 🟢 | 72.8 | 44.0s | $3.74 | 240M (verbose) | 500K | ✅ |
| **GLM-5.3** (max) | **45** 🟢 | 67.8 | 3.32s | $2.01 | 71K/task | 1M | ❌ |
| **Qwen3.8 Max** (0902) | **45** 🟢 | 39.1 | 2.94s | $5.41 | — | 1M | ✅ |
| **DeepSeek V4.1 Flash (1017 ckpt)** | **45** 🟢 | 169.1 | 1.18s | **$0.26** | 210M | 1M | ✅ |
| **Kimi K3** (max) | **44** 🟢 | 34.4 | 4.49s | $2.00 | 160M | 1M | ✅ |
| **Step 5 Preview** | **44** 🟢 | ~100 | — | ~$0.34¹ | — | 1M | ✅ |
| **Claude Haiku 5.5** (Max) | **43** 🟢 | 238 | — | **$0.21** | 440M (verbose) | 1M | ✅ |
| **MiniMax M3.1 Flash** ✨ | **43** 🟢 | **112.8** | **1.35s** | **$0.22** | 180M | 1M | ✅ |
| **GLM-5.3-Flash** | **42** 🟢 | ~45–200² | 3.33s | ~$0.25 | — | 1M | ✅ (in) |
| **Qwen3.8 Flash** | **40** 🟢 | — | — | — | — | 1M | ✅ |
| **Muse Spark 1.2** | **40** 🟡 | — | — | — | — | 1M | ✅ |
| **DeepSeek V4.1 Flash** (baseline) | **39** 🟢 | **209–232** | 0.99s | $0.27 | 250M (verbose) | 1M | ✅ |
| **GPT 6 Luna** (max) | **37–38** 🟢 | 125–145 | 109–118s³ | **$0.07** | 140M | 1.05M | ✅ |
| **DeepSeek V4 Pro 0813** (legacy) | **36** 🟢 | 96.0 | 1.67s | $0.67 | 160M | 1M | ❌ |
| **GPT 5.6 Luna** | **~35–37** 🟢 | 112 | 0.77s³ | $0.18 | — | 1.05M | ✅ |
| **GLM-5.2** (legacy) | **34** 🟢 | 81.5 | 3.13s | $1.47 | — | 1M | ❌ |
| **Beam** (free) | **30** 🟢 | — | — | $0 | token-efficient | 1M | ❌ text-only |
| **MiniMax M3** | **29** 🟢 | 91.2 | 1.56s | $0.51 | — | 1M | ✅ |
| **MiMo-V2.5-Pro** (legacy) | **26** 🟢 | — | — | — | — | 1M | ✅ omni |
| **Kimi K2.7 Code** | **26** 🟢 | — | — | — | — | 256K | ✅ |
| **Hy3** | **25** 🟢 | — | — | — | — | 256K | ❌ |
| **MiMo-V2.5** (legacy) | **25** 🟢 | — | — | — | — | 1M | ✅ omni |
| **Qwen3.7 Plus** | **25** 🟢 | 56.1 | — | $0.22 | — | 1M | ✅ |
| **MiniMax M2.7** (removed) | **23** 🟢 | 46.9 | 1.62s | — | — | 205K | ❌ |
| **LongCat-2.0** | **19** 🟢 | — | — | — | — | 1M | ❌ |

¹ Step 5 agent-loop estimate from vendor list prices at a typical agentic cache mix (AA-measured task cost not published). ² Provider-dependent (FlashX up to ~200 tok/s; AA run slower). ³ Non-reasoning TTFT; reasoning TTFT is 109–178s at max effort.

**Corrections this cycle:** Hy3 **34 → 25**, LongCat-2.0 **no score → 19**, Muse Spark 1.2 **45–46 → 40**. The old Hy3/LongCat "cheap volume" value was overstated.

**What this means:** the **best Go model (K3.1 Pro, 55.1)** is now only ~3 AA points behind Claude Opus 5.5 (58), and **2.1 points above Argon (53)**. The cheap tier is led by **MiniMax M3.1 Flash (43)** — five points above DeepSeek V4.1 Flash's conservative 39 baseline, at a lower per-request price. The **DeepSeek 1017 checkpoint (45)** shows the same model family can score six points higher than the original checkpoint; Go does not guarantee which checkpoint is served.

---

## 2. Agentic coding consensus (the table that matters most)

Triangulated across Vals AI, AA, LMArena, Terminal-Bench/vendor harnesses, SWE-bench runs, and the OpenHands Index. Harnesses differ; deltas within ~3 points are noise.

| Rank | Model | Best independent evidence | Notable vendor numbers |
|---|---|---|---|
| 🥇 | **Gemini 4 Argon** | **Vals Index v2.2 69.24% (#3 of 41)**, AA 53, AutomationBench #1 51.3%, lowest hallucination (AA-Omniscience: 15% wrong guesses vs 29% next best) | DeepSWE 77.9 SOTA claim (Oct 13) |
| 🥈 | **Kimi K3.1 Pro** | **AA 55.1 (highest on Go)**, Vals v2.2 62.52% (#4) | Kimi K3.1 Pro tech blog; agentic claims not independently replicated yet |
| 🥉 | **Kimi K3** | **Terminal-Bench 2.1 88.3** (verified), DeepSWE 67.5 (verified), SWE-bench 93.4, SWE-Marathon 42, OSWorld 84.8 | FrontierSWE 81.2, BrowseComp 91.2, MCP-Atlas 84.2 |
| 4 | **GLM-5.3 (max)** | TB2.1 88.2, **standardized TB4.0 41.9 (best Go)**, DeepSWE 66.9 | CyberGym 84.5, Z.ai Code Bench 34.5 |
| 5 | **Grok 4.7** | AA 46; Vals 58.56%; consults/reasoning (xhigh) | CursorBench 4.0 46.3, DeepSWE 71.0, TB4.0 37.6 |
| 6 | **DeepSeek V4.1 Flash** | Vendor DeepSWE 74.2 / TB2.1 90.6; **AA TB4.0 only 26.8**; 1017 checkpoint AA 45 | AutomationBench 54.8, CyberGym 88.1 |
| 7 | **GPT 5.6 Luna** | Vals SWE-bench 93.0, TB2.1 84.7, AA Coding Agent Index 71.5, DeepSWE 67.2 | cheap; weak on TB4.0 |
| 8 | **MiniMax M3.1 Flash** | **AA 43 at $0.22/task**, Vals 53.78%, 112.8 tok/s, 1.35s TTFT | new cheap-agent leader; long-horizon data still thin |
| 9 | **MiMo-V2.6-Pro** | Table stakes all vendor: TB2.1 89.9, DeepSWE 71.9, AutomationBench 53.1 | AA AutomationBench high; tool-call repetition bug (fixed Sep 25) |
| 10 | **GLM-5.3-Flash** | AA AutomationBench 60.4% (highest Go), AA 42 | TB2.1 84.3 vendor vs 62.9 Vals — harsh harness gap |
| 11 | **Qwen3.8 Max** | SWE-bench Pro **67.7** (best Go, verified), OSWorld 86.1 (#1 overall) | Terminal-Bench 2.1 86.6 |
| 12 | **Step 5 Preview** | Vendor DeepSWE 67.7 (= Kimi K3), TB2.1 85.0; TB4.0 33.3 | StepCodeBench 49.0, ProgramBench 80.5 — open weights |
| 13 | **Claude Haiku 5.5** | **AA 43 (Max)**; Vals 54.31%, Vibe Code Bench 90.44%, TB4.0 35.35% | Matched Sonnet 5 on many coding tasks (Copilot testing) |
| 14 | **Hy4 preview** | Vals 53.21%; vendor SWE-bench Pro **65.7**, Toolathlon 74.1 | no AA score yet |
| 15 | **LongCat-2.0** | Vendor SWE-bench Pro 59.5, SWE Multilingual 77.3; **AA only 19** | absent from Western independent boards |
| — | **Grok 4.6** (removed) | Vals 71.8, SWE-bench Verified 95.6%, TB2.1 78.3 Vals / 88.4 AA | best *verified* Grok generation; Zen only |
| — | **Beam** (free) | AA 30 — #2 US open-weights model; token-efficient | SWE-bench Verified 80.9 vendor |
| — | **Kimi K2.7 Code** | **All six headline benchmarks are first-party**; KernelBench regression vs K2.6 | treat with suspicion until third-party runs |

**The one-line summary:** for *verified* agentic coding, **Argon, Kimi K3.1 Pro, Kimi K3 and GLM-5.3** are the Go frontier. **Argon is now privacy-clean on Go (ZDR)**, which removes the biggest caveat from the previous cycle. **MiniMax M3.1 Flash** is the new value agent; **DeepSeek V4.1 Flash** remains the best price/performance at volume. Muse Spark Contributor is now the **only** training-on-data route on Go.

---

## 3. Per-model dossier

### 3.1 DeepSeek

**V4.1 Flash** (Sep 10, 2026) — 552B backbone + 196B Engram, 8B active prefill / 16B decode, Causal Encoder-Decoder, CSA2 attention, 890 bytes KV/token, 1M ctx, 384K max output, reasoning effort 1–100, native vision, MIT. Trained 45T tokens. [HF card](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash)

| Benchmark | Score | Verdict |
|---|---|---|
| Terminal-Bench 2.1 | **90.6** (DeepSeek card; verified by evals.report) | Best-in-class on TB2.1 |
| Terminal-Bench 3.0 / 4.0 | 30.0 / 31.2 vendor; **26.8 AA** | Hard-harness reality check |
| DeepSWE v1.1 | **74.2** vendor (beats Opus 5's 74.0 in the same table); 65.5 on OpenCode scaffold | Scaffold-sensitive |
| CyberGym | 88.1 | Security/exploit capable |
| HLE | 36.8 no-tools / **63.9 with tools** | Strong tool-augmented reasoning |
| AA Index | **39** baseline; **45 for the 1017 checkpoint** (169.1 tok/s, 1.18s, $0.26/task, 210M) | Present 39 conservatively; 1017 is upside if served |

**V4 Pro 0813** (legacy — retired upstream Sep 14) — 1.6T/49B MoE, 1M ctx, MIT, no vision. AA **36**, 96 tok/s, $0.67/task. DeepSeek retired it from its own API and routed traffic to V4.1 Flash; Go still lists it separately, but verify what is served.

**Community:** launch thread very positive, but users note reasoning-token burn. Enclave.ai's security team adopted it. OpenCode telemetry shows it as the #1 model by tokens across the entire user base (119T/week) — the crowd's workhorse.

---

### 3.2 Xiaomi MiMo

**MiMo-V2.6-Pro** (Sep 21) — 1.02T/42B sparse MoE, 70 layers, 1M ctx, **native text+image+video+speech**, MIT. AA **46 — #1 of all open-weight models in its class**; $0.13/AA task (cheapest frontier-class), 41.7 tok/s (slow), 4.2s TTFT.

Vendor table: DeepSWE 71.9, **TB2.1 89.9**, TB4.0 34.9, ProgramBench 26.5, AutomationBench 53.1, OSWorld 82.0, GDPval-AA 2.1 1673, CyberGym 94.0.

⚠️ **Known issue:** Xiaomi's Sept 27 post documents **tool-call repetition** (OpenCode: Flash 1.02%, Pro 0.54% of turns; up to 41.7% of replayed MiMo-Code samples). Fixed via MOPD distillation, API updated Sept 25. Also poor p95 TTFT (9.1s). [Post](https://mimo.xiaomi.com/blog/mimo-v2-6-tool-call-repetition)

**MiMo-V2.6-Flash** — smaller RL sibling; 67.9 DeepSWE, 87.6 TB2.1 (vendor). **AA 38** at **$0.06/AA-task** — still the cheapest smart volume on Go ($60 cap, 33k req/mo at your profile).

**MiMo-V2.5 / Pro** (legacy — retired upstream Oct 21) — far behind (AA 25/26). Only useful as volume filler; prefer V2.6.

---

### 3.3 Z.ai GLM

**GLM-5.3** (Aug 18; weights Aug 28) — 753B/40B MoE, 1M ctx, **text-only**, always-on reasoning, commercial-restricted license. AA **45**, 67.8 tok/s, $2.01/task.

| Benchmark | 5.3 | 5.2 |
|---|---|---|
| Terminal-Bench 3.0 (vendor) | **28.3** | 4.6 |
| TB 3.0 on AA-equivalent scale | 41.9 standardized (best Go) | — |
| DeepSWE v1.1 | 66.9 | 46.2 |
| SWE-bench Pro | — | 62.1 |
| CyberGym | 84.5 | 77.2 |
| Agents' Last Exam | 28.5 | 23.8 |
| Z.ai Code Bench | 34.5 @75K tok | 23.4 @96K |
| LMArena text | 1479 (#26) | 1475 (#32) |

⚠️ NIST/CAISI named GLM-5.3 "the most cyber-capable open-weight model released to date," ~4 months behind the US frontier. Strengths: terminal/agentic + cyber. Weaknesses: no vision, always-reasoning (expensive), verbose, 7%+ hallucination per HN users.

**GLM-5.3-Flash** (Aug 26) — 320B/18B MoE, **MIT**, native multimodal, sparse+linear attention. AA **42** at ~$0.25/task, **AA AutomationBench 60.4%** (highest Go), vendor TB2.1 84.3 but Vals only 62.9 — provider quantization/harness variance is the caveat. Fast (up to 200 tok/s on FlashX). Best cheap generalist on the roster, though **M3.1 Flash now beats it on AA and $/task**.

**GLM-5.2** (legacy — superseded by 5.3) — AA 34. Documented TB/SWE-Pro numbers only.

---

### 3.4 xAI Grok

**Grok 4.7** (Sep 21) — proprietary, 500K ctx, vision, reasoning low→xhigh. AA **46**; 44s TTFT, 81K output tokens/index task (240M total — "very verbose"), $3.74/task. Vendor: CursorBench 4.0 46.3, DeepSWE 71.0, TB4.0 37.6 (xAI) / 33 (AA), EEBench 64.0, Harvey Legal 19.6, HealthBench Prof 56.7. **LMArena ranks it BELOW Grok 4.6** (1442 vs 1453); Design Arena 1224. A reasoning/knowledge specialist that over-spends tokens.

**Grok 4.6** (removed from Go — Zen only) — AA 44, Vals 71.8, SWE-bench Verified 95.6, TB2.1 78.3 Vals / 88.4 AA, GPQA 95.0, ARC-AGI-2 67.1. Still the best verified Grok generation; use via Zen if you need it.

---

### 3.5 Moonshot Kimi

**Kimi K3.1 Pro** ✨ (Oct 2026; on Go Oct 25) — Moonshot's refreshed flagship; **AA 55.1** (highest on Go), 57.5 tok/s, 3.07s TTFT, **$2.11/AA task**, 150M verbosity, 1M ctx, vision. Go price **$2/$10/$0.20, cache write $2, $15 cap** → ~269 req/mo at your profile. Vals Index v2.2 **62.52%** (#4). It is the new Go ceiling: 2.1 AA above Argon, 11 above Kimi K3, at 2.4× Argon's per-request cost but with roughly a third of Argon's capacity. OmO 5.1.47 added K3.1 Pro-specific Sisyphus/Atlas prompts. Independent long-horizon/agentic numbers are still thin — treat the AA score as solid and the vendor agentic claims as 🟡.

**Kimi K3** (Jul 16) — **2.8T total / 104B active**, 93 layers (KDA + Gated MLA), MoonViT-V2 vision, 1M ctx, MXFP4 QAT, always-thinking, open weights under the Kimi K3 license. [HF card](https://huggingface.co/moonshotai/Kimi-K3)

Highlights (max): GPQA 93.5, HLE 43.5/56.0 tools, DeepSWE 67.5, TB2.1 88.3, **SWE-Marathon 42.0**, FrontierSWE 81.2, BrowseComp 91.2, OSWorld 84.8, MMMU-Pro 81.6, MCP-Atlas 84.2, Toolathlon 76.5, **#1 Front-end Code Arena (1679)**, ARC-AGI-2 60.4. AA **44**, slow (34.4 tok/s), $2.00/task, verbose (160M). Weaknesses: sensitivity to thinking history, "excessive proactiveness," explicit UX gap vs Fable 5.

**Kimi K2.7 Code** (Jun 12) — 1T/32B, 256K ctx, thinking-only. Vendor deltas: Kimi Code Bench v2 62.0, Program Bench 53.6, MCP Atlas 76.0. **No independent runs**, and KernelBench-Hard showed *regression* vs K2.6. "More honest but not more capable."

**Kimi K2.6** (legacy) — superseded.

---

### 3.6 Alibaba Qwen

**Qwen3.8 Max** (Aug 3; 0902 snapshot) — 2.4T/95B, 1M ctx, text+image(+video), reasoning xhigh/medium/low. Prices $2/$6. AA **45** but **39 tok/s and $5.41/task — the most expensive Go model per unit of work**. Verified: **SWE-bench Pro 67.7 (best Go)**, TB2.1 86.6, **OSWorld 86.1 (#1 overall)**, MMMU-Pro 82.3, IFBench 82.8, LMArena WebDev **1688 (#2)**, LMArena Vision **#9** (not #2 — correction), ScreenSpot-Pro 84.5.

**Qwen3.8 Flash** (Aug 26) — 125B + 51B N-gram embeddings, **6B active**, 262K native → 1M, multimodal. **AA 40**. Vendor: AndroidWorld 84.5, RealWorldQA 88.5, MathVision 90.6, CharXiv 84.6, CoWorkBench 73.9. Thin independent cover beyond AA.

**Qwen3.7 Plus** (May 31) — 1M ctx, multimodal, AA 25. Volume model.

---

### 3.7 OpenAI GPT Luna

**GPT 6 Luna** (Sep 22) — 1.05M ctx, 128K out, effort none→max, vision, computer-use, hosted shell. $0.10/$0.50. AA **37–38**, **$0.07/AA task (cheapest frontier-lab model)**, 125–145 tok/s. Vendor: DeepSWE 66.6, AutomationBench 20.7, OSWorld 52.7, factual error 7.6%. Vals: index 51.2, **TB4.0 13.6, ProgramBench 0.5** — agentically weak.

**GPT 5.6 Luna** (Jul 9) — AA ~35–37, Vals SWE-bench **93.0**, TB2.1 84.7, AA Coding Agent Index 71.5, DeepSWE 67.2. Good cheap second opinion, not a marathon agent.

**Context (not on Go):** GPT-6 Astra (AA 53, ARC-AGI-2 95, WebDev 1792), GPT-6 Sol (47–48), GPT-6.1 Sol (52). Pay-for-the-jump targets via Zen.

---

### 3.8 Meta Muse Spark

**Muse Spark 1.3 Contributor** (Sep 2) — 1M ctx, multimodal, max reasoning. AA **48** (medium confidence). Design Arena **Website #1**, LMArena WebDev 1623, MRCR v2 8-needle 512K–1M = 98.1 (self-reported), JobBench 64.9, GDPval-AA 1754. ⚠️ **Contributor tier trains on your prompts/completions** — the only training-on-data paid route left on Go. Not for client/PHI.

**Muse Spark 1.2** (Aug 5) — **AA 40 (corrected from 45–46)**, Design Arena 1318. Contributor terms apply.

---

### 3.9 Tencent Hunyuan

**Hy4 preview** (Aug 28) — 770B/49B + 10B MTP, 1M ctx, **Apache 2.0**, thinking defaults high. Official blind eval: 2.99 avg vs GLM-5.3 2.92 and Kimi K3 2.94 (203 tasks, 163 Tencent experts). Vendor: **SWE-bench Pro 65.7**, MCP-Atlas 83.7, Toolathlon 74.1, GPQA 92.3 (unverified). **No AA score.** Over-reasons and over-verifies. At $0.834/$2.501 it is the most expensive cheap-tier model on Go.

**Hy3** (Apr 22) — 295B/21B, 256K, community license. GPQA 87.2, SWE-bench Verified 74.4, TB2.0 54.4, HLE 30. **AA 25 (corrected from ~34)**. Old and weak; volume filler only.

---

### 3.10 Meituan LongCat

**LongCat-2.0** (Jun 30) — 1.6T/~48B + 135B N-gram embedding params, LongCat Sparse Attention, native 1M ctx, **MIT**. Vendor: TB2.1 70.8, SWE-bench Pro 59.5, SWE Multilingual 77.3, FORTE 73.2, BrowseComp 79.9, GPQA-D 88.9. **AA 19** — the independent score is far below the vendor story. Cheap ($0.30/$1.20, $0.006 cache), but not a quality pick.

**LongCat 2.5 Preview** — **removed from Go/Zen**; free window ended. No public model card.

---

### 3.11 MiniMax

**MiniMax M3.1 Flash** ✨ (Oct 2026; on Go Oct 25) — MiniMax's refreshed agentic Flash model: **AA 43**, **112.8 tok/s**, **1.35s TTFT**, **$0.22/AA task**, 180M verbosity, 1M ctx, vision. Vals Index v2.2 **53.78%**. Go price **$0.15/$0.60/$0.015, $20 cap** → ~4,975 req/mo at your profile, **10,697 AA pts/$**. It beats GLM-5.3-Flash on AA (43 vs 42) and on $/task ($0.22 vs ~$0.25), with half the capacity but far better speed. Telemetry: #2 by tokens (+92% in a week). Community reports it is the early "Space Bunny" model. This is the new default cheap workhorse.

**MiniMax M3** (Jun 1) — 428B/23B, 1M ctx, open weights, multimodal. Vendor: SWE-bench Pro 59.0, TB2.1 66.0, OSWorld 70.06. **AA only 29** — vendor claims far outrun independent measurement.

**MiniMax M2.7** (removed) — AA 23, 205K, data/ML specialist only.

---

### 3.12 StepFun Step 5 Preview (paid, promo ended)

**Step 5 Preview** (API Sep 20; Go free Oct 8–15; now **$1.00/$2.70/$0.10 with a $15/mo cap**) — 600B total / **27B active** sparse MoE, 1M ctx, native vision, built for long-horizon reasoning and autonomous execution. **AA 44 independently confirmed**; Vals TB4.0 31.8% matches vendor 33.3%. **Open weights released Oct 15** (BF16 + FP8, HuggingFace + ModelScope) — self-hostable. [StepFun announcement](https://www.stepfun.com/step-5-preview) · [Vals page](https://www.vals.ai/models/stepfun_step-5-preview)

| Benchmark | Step 5 (High) | Kimi K3 (Max) | GLM-5.3 (Max) |
|---|---|---|---|
| AA Intelligence Index | **44** | 44 | 45 |
| DeepSWE v1.1 | **67.7** | 67.5 | 66.9 |
| Terminal-Bench 2.1 | 85.0 | 85.0 | 83.9 |
| Terminal-Bench 4.0 | **33.3** | 12.6 | 41.9 |
| StepCodeBench | **49.0** | 43.9 | 40.2 |
| ProgramBench | **80.5** | 77.8 | 72.0 |
| AA-LCR v1.1 | **88.3** | 88.7 | 79.7 |

**Verdict:** Kimi-class across the board, 2.6× Kimi K3 on TB4.0. The promo ended: at a $15 cap it buys **~591 req/mo** at your profile (not ~2,400). Still the best AA 44+ capacity per dollar after Argon/M3.1 Flash, and self-hostable.

---

### 3.13 NEW — Kimi K3.1 Pro (on Go Oct 25)

**Kimi K3.1 Pro** — Moonshot's mid-October flagship refresh, listed on Go on Oct 25 at **$2.00/$10.00/$0.20 (cache write $2.00), $15/mo**. **AA 55.1** — the highest Intelligence Index ever on Go, 2.1 above Gemini 4 Argon and 11.1 above Kimi K3. AA-measured: **57.5 tok/s, 3.07s TTFT, $2.11/AA task, 150M verbosity**, 1M ctx, vision. Vals Index v2.2: **62.52%** (#4 of 41, behind Sonnet 5.5, Opus 5.5 and Argon). At your token profile it costs **$0.0558/request** → **~269 req/mo** (5h: 54, week: 134). That is **1.5× Kimi K3's capacity at 1.25× AA** — strictly better than the old K3 ration. OmO 5.1.47 added K3.1 Pro-specific Sisyphus/Atlas prompts.

**Verdict:** the new Go ceiling for hard, non-convergent work, at a $15-ration price. It is not a volume model. Argon remains the better *agentic* score on Vals (69.24 vs 62.52) and gives 2.7× the capacity for 26% less per request — but K3.1 Pro is the smarter model on AA. Use K3.1 Pro for the hardest plan/debug/review calls, Argon for longer hard-task runs.

---

### 3.14 NEW — MiniMax M3.1 Flash (on Go Oct 25)

**MiniMax M3.1 Flash** — MiniMax's refreshed Flash model, listed on Go Oct 25 at **$0.15/$0.60/$0.015, $20/mo**. **AA 43** (one point above GLM-5.3-Flash, four above DeepSeek V4.1's baseline), **112.8 tok/s**, **1.35s TTFT**, **$0.22/AA task**, 180M verbosity, 1M ctx, vision. Vals v2.2 53.78%. At your profile: **$0.00402/request** → **~4,975 req/mo**, **10,697 AA pts/$**, 214k monthly cognitive throughput. Telemetry: **37T tokens/week, #2 overall, +92%** — the fastest adoption of any new Go model this cycle.

**Verdict:** the new default cheap workhorse. It is smarter, faster and cheaper per AA task than GLM-5.3-Flash; the trade is capacity (4,975 vs 9,836 req/mo) and independent long-horizon coverage. For high-volume 8-hour days, use M3.1 Flash as the quality lane and GLM-5.3-Flash/DeepSeek as the volume lanes.

---

### 3.15 Gemini 4 Argon — privacy correction (on Go since Oct 13)

**Gemini 4 Argon** (GA Sep 30; Go SKU renamed from "Contributor" and cut to **50% off through Nov 30**) — Google's frontier model. **AA 53** (equal to GPT-6 Astra and Claude Fable 5.1), **Vals Index v2.2 69.24% (#3 of 41)**, **AutomationBench #1 (51.3%)**, **lowest hallucination on AA-Omniscience** (15% wrong guesses vs 29% next best). Vendor claim: DeepSWE 77.9 SOTA (Oct 13).

| Go facts | Value |
|---|---|
| Go price | **$2.00 / $10.00 / $0.10** (50% off; list returns after Nov 30) |
| Go monthly cap | **$30** — Plus **$120** |
| Your cost/request | ≈ **$0.0412** → **~728 req/mo** |
| Privacy | ✅ **Not used for training; 0-day retention** per Go docs — **corrected Oct 25** |
| Capacity | 5h ~146 req; week ~364 req |

**Verdict:** the best hard-task *capacity* on Go, now without the Contributor-training caveat. At 728 req/mo it is 2.7× K3.1 Pro's capacity at 26% lower cost per request, and only 2 AA points behind. It is the default hard-task model for client work too, subject to normal provider-contract verification. The old "trains on your data" warning in this repo was **wrong** and is withdrawn.

---

### 3.16 Removed / stealth models

**Space Bunny** — **removed from Go/Zen**. Revealed Oct 19 as an early **MiniMax M3.1 Flash**; the paid SKU and free stealth are both gone. Use `minimax-m3.1-flash`.

**LongCat 2.5 Preview Free** — **removed**; free window ended. LongCat-2.0 remains.

**Beam Free** (Reflection AI, free since Oct 12) — 501B/23B MoE, **AA 30**, Apache-2.0 weights, 30-day retention, no training, limited regions. Good free mid-tier agent, not a frontier alternative.

**Flint 40B Free** (Zen, Oct 2026) — new free 40B-class model; **30-day retention, may train**. Non-sensitive exploration only.

**Big Pickle** (Zen) — stealth; data used for training. Unknown identity. Do not trust with sensitive code.

---

## 4. Benchmark-source health (as of Oct 25, 2026)

| Source | Status | Notes |
|---|---|---|
| Artificial Analysis | 🟢 healthy | v4.3.2 current; added K3.1 Pro (55.1), M3.1 Flash (43), DeepSeek 1017 (45) |
| Vals AI | 🟢 healthy | Index v2.2: Sonnet 5.5 70.85%, Opus 5.5 70.18%, Argon 69.24%, K3.1 Pro 62.52% |
| LMArena | 🟡 unverifiable | JS-only leaderboard; this cycle's numbers come from mirrors/snippets. Qwen3.8 Max is **Vision #9**, not #2. |
| SWE-bench official | 🟡 partial | JS board only renders headers for many rows; numbers circulate via mirrors |
| Terminal-Bench official | 🟡 partial | TB2.1 renders; **TB4.0 table empty** |
| Aider Polyglot | 🔴 frozen | No new entries since Aug 2025 — useless for current models |
| LiveCodeBench official | 🔴 broken | "Loading leaderboard data…" indefinitely; mirrors used |
| METR time-horizon | 🟡 stale | Last update May 8, 2026; **no Go model measured** |
| Epoch AI | 🟡 partial | Only GLM-5.3 among Go models has a public run |
| OpenHands Index | 🔴 stale | Latest is GLM-5.1/MiniMax M3/Kimi K2.6 era |
| Design Arena / WebDev Arena | 🟢 healthy | Go models rank well here |
| ARC Prize | 🟢 healthy | Covers Grok/Kimi/GPT-Luna; missing GLM/Qwen/DeepSeek/Argon |
| HuggingFace Open LLM Leaderboard | 🔴 archived | Use HF model cards/downloads instead |

---

## 5. Final consensus rankings

**Overall intelligence (Go only):**
1. **Kimi K3.1 Pro (55.1)** · 2. **Gemini 4 Argon (53)** · 3. Muse Spark 1.3 (48) ⚠️ trains · 4. MiMo-V2.6-Pro / Grok 4.7 (46) · 6. GLM-5.3 / Qwen3.8 Max (45) · 8. DeepSeek V4.1 Flash 1017 (45, checkpoint-dependent) · 9. Kimi K3 / Step 5 (44) · 11. Claude Haiku 5.5 (43 Max; 34 med) / **MiniMax M3.1 Flash (43)** · 13. GLM-5.3-Flash (42) · 14. Qwen3.8 Flash / Muse Spark 1.2 (40) · 16. DeepSeek V4.1 Flash baseline (39) · 17. MiMo-V2.6-Flash / GPT 6 Luna (38) · 19. GPT 5.6 Luna (35–37) · 20. Beam (30) · 21. MiniMax M3 (29) · 22. Kimi K2.7 / MiMo-V2.5-Pro (26) · 24. Hy3 / MiMo-V2.5 / Qwen3.7 Plus (25) · 27. MiniMax M2.7 (23) · 28. LongCat-2.0 (19).

**Agentic coding (Go only, independent-evidence weighted):**
1. **Gemini 4 Argon** (Vals 69.24, ZDR) · 2. **Kimi K3.1 Pro** (AA 55.1, Vals 62.52) · 3. Kimi K3 · 4. GLM-5.3 · 5. Grok 4.7 · 6. DeepSeek V4.1 Flash (value king) · 7. GPT 5.6 Luna · 8. **MiniMax M3.1 Flash** (new value agent) · 9. MiMo-V2.6-Pro · 10. GLM-5.3-Flash · 11. Qwen3.8 Max · 12. Step 5 · 13. Claude Haiku 5.5 (best subagent) · 14. Hy4 · 15. LongCat-2.0. Free tier: GLM-5.3-Flash Free > DeepSeek V4.1 Flash Free > Beam Free.

**Design/frontend:** Muse Spark 1.3 > Kimi K3.1 Pro / K3 > GLM-5.3 > MiMo-Pro > Qwen3.8 Max. **Value:** M3.1 Flash / GLM-5.3-Flash.

**Vision/visual QA:** Qwen3.8 Max (OSWorld #1) > Kimi K3 > Muse Spark 1.3 > MiMo-Pro > Qwen3.8 Flash. For OCR: Qwen3.8 Max/Flash, DeepSeek V4.1 Flash (DocVQA 95.6).

---

**Next:** [03 — Task Playbook](./03-task-playbook.md) · [04 — Limits & Burn Rate](./04-limits-and-burn-rate.md)
