# 02 — Model Benchmark Dossier (Go Roster)

> **Snapshot: October 1, 2026; refreshed October 13, 16, 25 and November 17, 2026 — full AA v5.0.1 re-baseline.** Nov 17 rebuilt §1 (v5.0.1 master table + a preserved "v4.3.2 retired scale" table for history), §2 (the ceiling reversal), §3 (new AA numbers; Hy4 GA measured; **Qwen4 Max** added) and §5 (consensus rebuilt on v5.0.1).
> **Confidence legend:** 🟢 independent multi-source · 🟡 vendor + partial independent · 🔴 vendor-only / unverified. **Legacy** = retired upstream or removed from Go docs — still billed on Zen, but avoid for new work.
>
> 🆕 **Nov 17 — the new stuff:** **Gemini 4 Argon (AA 50)** is now the highest-intelligence model on Go; **Kimi K3.1 Pro (AA 46)** drops to #2 and **Qwen4 Max (AA 43, rel Nov 16)** lands at #3. **Claude Haiku 5.5 (36)** is the best cheap lab model, and the cheap tier (27–29) is compressed into noise. *(Oct 25, history: K3.1 Pro and M3.1 Flash launched; Argon's privacy corrected to 0-day retention / not trained.)*

**The single most important caveat:** benchmark scores are only comparable **within the same index version and harness** — and **AA v5.0.1 is not comparable with v4.3.2**. AA shipped **v5.0 on Oct 27, 2026** (added HLE-Diamond, Terminal-Bench-Science, FrontierCode-AA 2.0 and CritPt v2 Hard Subset; dropped GDPval-AA, SciCode, AA-LCR, HLE; four equal 25% categories; 9 evaluations) and the **v5.0.1 regrade went live Nov 3** (CritPt v2 grading-robustness fixes from the CritPt authors; all models regraded; nothing else changed vs v5.0). Same-model moves are large and non-uniform (K3.1 Pro 55.1→46, Argon 53→50), and the frontier moved ≈58→65 partly because of the **Nov 9 Fable 5.2 release** — a newer model, not a pure rescale. For cross-vintage comparison AA itself points to its separate **Progress Index v1** ("one capability scale"). Terminal-Bench 2.1 ≠ 3.0 ≠ 4.0, and every TB4.0 score swings by 10+ points depending on scaffold. v5 tasks are also heavier (median output 35k→59k tokens).

---

## 1. Master table — Intelligence Index v5.0.1 (Artificial Analysis)

All Go-roster models with a v5.0.1 AA run are listed; unmeasured ones get explicit rows. Speed/TTFT are AA Performance Benchmarking v3.0.0 (Nov 3): output speed is end-to-end including first-token wait, 5-day workload averages. **TTFT (TFAAT)**: for OpenAI/Anthropic/Google/Meta/xAI first-party endpoints time-to-first-token equals time-to-first-*answer*-token (shown `(=)`); for DeepSeek/Kimi/Xiaomi/Alibaba/Tencent/MiniMax/StepFun TTFT ≪ TFAAT (thinking time included in TFAAT). AA publishes no "median TTFT" — these are workload averages. **AA $/task** = weighted-average USD to complete one index task from AA's actual measured token usage across the 9-eval workload — not AA "Price (Blended)". Effort variants are separate AA rows; **the effort OpenCode Go actually serves per model is undocumented — open question**.

| Model | AA Index v5.0.1 | Speed (tok/s) | TTFT (TFAAT) | AA $/task | Context | Vision | Notes |
|---|---|---|---|---|---|---|---|
| **Gemini 4 Argon** ✨ | **50** (high; 50.41) 🟢 | 66.3 | 43.9s (=) | $4.97 | 1M | ✅ | No max effort on AA (High/Medium only); 50% off through Nov 30 |
| **Kimi K3.1 Pro** | **46** (max; 46.45) 🟢 | 31.0 | 3.92s (151.0s) | $3.68 | 1M | ✅ | Single variant @max |
| **Qwen4 Max** ✨ | **43** (42.89) 🟢 | 54.4 | 5.28s (147.6s) | $3.27 | 984K | — | Rel Nov 16; AA changelog Nov 15 "43" |
| **Muse Spark 1.3 Contributor** | **37** (max; 36.62) 🟡 | 109.3 | 31.6s (=) | $2.39 | 1M | ✅ | ⚠ trains on data; AA prices **Meta's endpoint ($1.25/$4.25), NOT the Go Contributor SKU** |
| **Claude Haiku 5.5** | **36** (max; 36.48) 🟢 | 257.0 | 182.3s (=) | $0.41 | 1M | ✅ | Effort spread 36/35/30/25/19 (max→low) |
| **Hy4 (GA)** | **35** (34.56) 🟢 | 95.6 | 2.89s (112.8s) | $1.03 | 1M | — | AA "Tencent Hy4"; rel Nov 3, results Nov 4; **AA has no separate Hy4-preview entry** |
| **Grok 4.7** (xhigh) | **35** (35.49) 🟢 | 70.7 | 49.2s (=) | $7.77 | 500K | ✅ | high 35.21 / low 31.13; AA creator listed "SpaceXAI" |
| **Qwen3.8 Max (0902 snapshot)** | **34** (33.65) 🟢 | 60.6 | 3.69s (102.7s) | $10.02 | 1M | ✅ | ⚠ Go SKU rel = **0803 snapshot = unscored on v5.0.1** |
| **DeepSeek V4.1 Flash 1017** | **33** (max; 32.59) 🟢 | 177.3 | 1.26s (40.0s) | $0.60 | 1M | ✅ | The catalog SKU is literally "DeepSeek V4.1 Flash 1017" — the 1017 checkpoint **is** the served product (AA 33 = what you get); base (Sep-10) checkpoint unscored |
| **GLM-5.3** (max) | **32** (31.65) 🟢 | 89.4 | 2.53s (59.5s) | $5.01 | 1M | ❌ | (Low) variant = 23 |
| **MiMo-V2.6-Pro** | **30** (29.89) 🟢 | 54.4 | 4.06s (25.8s) | $0.26 | 1M | ✅ omni | |
| **Step 5 Preview** | **29** (28.53) 🟢 | 133.2 | 0.87s (22.1s) | $2.35 | 1M | ✅ | |
| **MiniMax M3.1 Flash** | **29** (29.06) 🟢 | 141.3 | 1.25s (46.3s) | $0.49 | 1M | ✅ | |
| **Qwen3.8 Flash** | **29** (28.58) 🟢 | 84.0 | 2.43s (59.9s) | $0.57 | 1M | ✅ | AA name "Qwen3.8-Flash-Next" — mapping inferred (same release date + price) |
| **GLM-5.3-Flash** | **28** (27.8) 🟢 | 57.1 | 3.09s (78.6s) | $0.58 | 1M | ✅ (in) | |
| **GPT 6 Luna** (max) | **28** (27.86) 🟢 | 102.6 | 68.3s (=) | $0.15 | 1.05M | ✅ | Spread 28/23/21/18/10/9 (max→low→non-reas) |
| **MiMo-V2.6-Flash** | **27** (26.73) 🟢 | 42.9 | 5.20s (26.0s) | $0.13 | 1M | ✅ omni | |
| **GPT 5.6 Luna** (max) | **24** (23.79) 🟢 | 105.0 | 49.5s (=) | $0.33 | 1.05M | ✅ | Other efforts unscored |
| **DeepSeek V4 Pro 0813** (legacy, max) | **23** (23.06) 🟢 | 94.9 | 2.69s (49.8s) | $1.77 | 1M | ❌ | (high)=21, (non-reas)=13 |
| **MiniMax M3** | **19** (18.88) 🟢 | 112.5 | 1.48s (65.2s) | $1.29 | 1M | ✅ | |
| **Beam Free** | **18** (17.73) 🟢 | 281.2 | 0.74s (7.7s) | $0.28 | 1M | ❌ text-only | AA "Beam 1.0"; AA prices the public API ($0.40/$1.20) — Go SKU is free |
| **Kimi K3** | **17** (low only; 17.42) 🟢 | 46.6 (max) | 5.22s (54.8s) | $2.37 | 1M | ✅ | ⚠ AA scores ONLY the (Low) variant; (Max) = N/A — **do not over-read** |

**Not measured (v5.0.1)** — AA shows N/A; old scores live only in the retired table below:

| Model | AA Index v5.0.1 | Notes |
|---|---|---|
| GLM-5.2 (legacy) | not measured (v5.0.1) | (v4.3.2, retired scale: 34) |
| Kimi K2.7 Code | not measured (v5.0.1) | all headline numbers first-party |
| LongCat-2.0 | not measured (v5.0.1) | (v4.3.2, retired scale: 19) |
| Hy3 | not measured (v5.0.1) | (v4.3.2, retired scale: 25) |
| Qwen3.7 Plus | not measured (v5.0.1) | (v4.3.2, retired scale: 25) |
| Muse Spark 1.2 Contributor | not measured (v5.0.1) | ⚠ trains on data; (v4.3.2, retired scale: 40) |
| MiMo-V2.5 / MiMo-V2.5-Pro (removed from Go Nov 17) | not measured (v5.0.1) | (v4.3.2, retired scale: 25 / 26) |
| DeepSeek V4.1 Flash (base ckpt) | not measured (v5.0.1) | not the served SKU — the catalog SKU is "DeepSeek V4.1 Flash 1017" (1017 = what you get) |
| Qwen3.8 Max (0803 = the Go SKU) | not measured (v5.0.1) | ⚠ the 34 above belongs to the 0902 snapshot |
| Kimi K3 (max) | not measured (v5.0.1) | only the (Low) variant is scored |
| Hy4 preview (Go-only SKU) | not measured (v5.0.1) | AA has no Hy4-preview entry at all |
| MiniMax M2.7 (removed) | not measured (v5.0.1) | (v4.3.2, retired scale: 23) |

**Not on AA at all (Go-only SKUs):** Iceman Contributor Free (⚠ trains on data) · LongCat 2.5 Free (China-hosted — needs Regions=Global) · Hy4 Flash Free.

**Frontier anchors (not on Go — scale context, v5.0.1):** Claude Fable 5.2 (max) **65** (64.56; Vals 71.31% #1 — new Vals leader; effort spread 65/62/62/56/54; $26.54/task) — board leader · **GPT-6.2 Astra (max/xhigh) 62 (new #2; high 60, med 57, low 46; Vals 67.66% #7)** · Gemini 4 Carbon (high) 60 (60.03; Vals 70.45%) · Claude Opus 5.5 (max) 59 (59.11) · GPT-6 Astra (max) 57 (56.85 — earlier anchor, superseded by 6.2) · GPT-6.2 Sol (max) 57 (Vals 66.06% #9) · Claude Sonnet 5.5 (max) 55 (54.54) · GPT-6.1 Sol (max) 55 · Gemini 4 Hydrogen (xhigh) 54 · GPT-6.1 Terra (max) 51 · Muse Wonder Full (max) 50 (Vals 66.79%) · **Claude Fable 5.1 (xhigh) 50** (49 max / 47 high / 43 med / 39 low — deprecated but benchmarked every 18h; $12.99/task at max) · GPT-6 Sol (max) 44 (44.16). ⚠ Bare **"Claude Fable 5"** (Jun 2026) is an **unscored stub** — but **Fable 5.1 is scored** (50 xhigh / 49 max — same tier as Argon 50.4) and Fable 5.2 leads at 65. "Gemini 4 Argon Pro" does not exist on AA.

**What this means (v5.0.1):** **Argon (50)** is the highest-AA model on Go and (per [05](./05-intelligence-per-dollar.md)) the best top-end value on raw pts/$ — **but 55-day retention (corrected Nov 18)**, so the old "privacy-clean (ZDR)" claim is withdrawn: default it for non-client planning, contract-check for client/PHI, escalate privacy-safe to K3.1 Pro. **K3.1 Pro (46)** is #2 and the 1M-ctx/Max-effort specialist. **Qwen4 Max (43)** is the new #3 and the first fresh model to land already scored on v5.0.1 (Vals 63.20% #11, top Chinese). **Haiku 5.5 (36)** is the strongest cheap-lab model. The cheap tier is compressed: Step 5 / M3.1 Flash / Qwen3.8 Flash = 29, GLM-5.3-Flash / GPT 6 Luna = 28, MiMo-V2.6-Flash = 27 — within ±3 points that is measurement noise, so pick on capacity/price/speed/privacy. And the DeepSeek checkpoint question is resolved: the console catalog names the SKU **"DeepSeek V4.1 Flash 1017"** — Go serves the 1017 checkpoint as the product (AA 33 = what you get), so the earlier checkpoint ambiguity is over (light hedge: router behavior can still change).

---

### v4.3.2 (retired scale — history only)

Everything in this table is **(v4.3.2, retired scale)** and must never be mixed with the v5.0.1 table above. Preserved verbatim from the Oct 25 cycle.

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

**Corrections of that cycle (history):** Hy3 **34 → 25**, LongCat-2.0 **no score → 19**, Muse Spark 1.2 **45–46 → 40**. The old Hy3/LongCat "cheap volume" value was overstated.

**v4.3.2 → v5.0.1 same-model deltas** (large and non-uniform — this is exactly why cross-scale comparison is forbidden): Kimi K3.1 Pro 55.1→46 · Gemini 4 Argon 53→50 · Muse Spark 1.3 48→37 · MiMo-V2.6-Pro 46→30 · Grok 4.7 46→35 · GLM-5.3 45→32 · Qwen3.8 Max 45→34 (0902) · DeepSeek 1017 45→33 · Kimi K3 44→17 (low only) · Step 5 44→29 · MiniMax M3.1 Flash 43→29 · Haiku 5.5 43→36 · GLM-5.3-Flash 42→28 · Qwen3.8 Flash 40→29 · GPT 6 Luna 37→28 · DeepSeek V4 Pro 36→23 · GPT 5.6 Luna ~36→24 · Beam 30→18 · MiniMax M3 29→19. Frontier ≈58 (Opus 5.5, v4.3.x) → 65 (Fable 5.2, Nov release — also a newer model, not a pure rescale).

---

## 2. Agentic coding consensus (the table that matters most)

Triangulated across Vals AI, AA, LMArena, Terminal-Bench/vendor harnesses, SWE-bench runs, and the OpenHands Index. Harnesses differ; deltas within ~3 points are noise. **Ranks below the top 3 are weighted on independent agentic evidence (Vals/TB/SWE), not AA** — the two disagree sharply for some models (Kimi K3: TB2.1 88.3 verified vs AA 17 @low-only; Haiku: AA 36 vs Vals 54.31%).

| Rank | Model | AA v5.0.1 | Best independent evidence | Notable vendor numbers / flags |
|---|---|---|---|---|
| 🥇 | **Gemini 4 Argon** | **50** (high) | **Vals Index v2.2 launch 69.24% (#3 of 41 at launch)**, AutomationBench #1 51.3%, lowest hallucination (AA-Omniscience: 15% wrong guesses vs 29% next best) | DeepSWE 77.9 SOTA claim (Oct 13); no max effort on AA; **55-day retention (corrected Nov 18 — worst on roster)** |
| 🥈 | **Kimi K3.1 Pro** | **46** (max) | **Vals v2.2 62.52% (#4 of 41, confirmed)** | single AA variant @max; agentic claims not independently replicated yet |
| 🥉 | **Qwen4 Max** | **43** | **Vals 63.20% (#11, top Chinese)**; AA 43 (rel Nov 16, scored on v5.0.1 immediately) | 984K ctx; other agentic evidence **not measured yet** |
| 4 | **Kimi K3** | 17 (low ⚠) | **Terminal-Bench 2.1 88.3** (verified), DeepSWE 67.5 (verified), SWE-bench 93.4, SWE-Marathon 42, OSWorld 84.8 | FrontierSWE 81.2, BrowseComp 91.2, MCP-Atlas 84.2; ⚠ AA's 17 is @Low only — do not over-read |
| 5 | **GLM-5.3 (max)** | 32 | Vals 59.85%; TB2.1 88.2, **standardized TB4.0 41.9 (best Go)**, DeepSWE 66.9 | CyberGym 84.5, Z.ai Code Bench 34.5 |
| 6 | **Grok 4.7** | 35 (xhigh) | Vals 58.62%; consults/reasoning (xhigh) | CursorBench 4.0 46.3, DeepSWE 71.0, TB4.0 37.6 |
| 7 | **DeepSeek V4.1 Flash** | 33 (1017 — the served SKU) | Vals 61.26%; vendor DeepSWE 74.2 / TB2.1 90.6; **AA TB4.0 only 26.8** | AutomationBench 54.8, CyberGym 88.1; catalog SKU = "DeepSeek V4.1 Flash 1017" (base ckpt unscored, not served) |
| 8 | **GPT 5.6 Luna** | 24 (max) | Vals SWE-bench 93.0, TB2.1 84.7, AA Coding Agent Index 71.5, DeepSWE 67.2 | cheap; weak on TB4.0 |
| 9 | **MiniMax M3.1 Flash** | 29 | **$0.49/AA task**, Vals 53.78%, 141.3 tok/s, 1.25s TTFT | cheap-agent value lane; long-horizon data still thin |
| 10 | **MiMo-V2.6-Pro** | 30 | Vals 57.81%; table stakes all vendor: TB2.1 89.9, DeepSWE 71.9, AutomationBench 53.1 | AA AutomationBench high; tool-call repetition bug (fixed Sep 25) |
| 11 | **GLM-5.3-Flash** | 28 | AA AutomationBench 60.4% (highest Go) | TB2.1 84.3 vendor vs 62.9 Vals — harsh harness gap |
| 12 | **Qwen3.8 Max** | 34 (0902 ⚠) | SWE-bench Pro **67.7** (best Go, verified), OSWorld 86.1 (#1 overall) | Terminal-Bench 2.1 86.6; ⚠ Go serves the unscored 0803 snapshot |
| 13 | **Step 5 Preview** | 29 | Vals 54.76%; vendor DeepSWE 67.7 (= Kimi K3), TB2.1 85.0; TB4.0 33.3 | StepCodeBench 49.0, ProgramBench 80.5 — open weights |
| 14 | **Claude Haiku 5.5** | 36 (max) | Vals 54.31% (#16, $2.99/test), Vibe Code Bench 90.44%, TB4.0 35.35% | best cheap lab model / best subagent; matched Sonnet 5 on many coding tasks (Copilot testing) |
| 15 | **Hy4 (GA)** | 35 | Vals 59.35%; vendor SWE-bench Pro **65.7**, Toolathlon 74.1 | AA "Tencent Hy4" (GA); ⚠ preview is a separate Go SKU and is unscored |
| 16 | **LongCat-2.0** | not measured | Vendor SWE-bench Pro 59.5, SWE Multilingual 77.3 | absent from Western independent boards |
| — | **Grok 4.6** (removed) | (v4.3.2, retired scale: 44) | Vals 71.8, SWE-bench Verified 95.6%, TB2.1 78.3 Vals / 88.4 AA | best *verified* Grok generation; Zen only |
| — | **Beam Free** | 18 | Vals 43.42% | AA "Beam 1.0"; SWE-bench Verified 80.9 vendor; token-efficient |
| — | **Kimi K2.7 Code** | not measured | **All six headline benchmarks are first-party**; KernelBench regression vs K2.6 | treat with suspicion until third-party runs |

**Flags & caveats on the AA numbers (all open, not resolved):**
- **Qwen3.8 Max's 34 is the 0902 snapshot** — Go serves the **0803** snapshot, which is **unscored** on v5.0.1 (HN/Reddit controversy about the 0902 re-baseline is context only).
- **DeepSeek's 33 is the Oct-17 checkpoint — and that is now confirmed as the product:** the catalog SKU is literally **"DeepSeek V4.1 Flash 1017"**, so the 1017 checkpoint is what Go serves (AA 33 = what you get) and the earlier checkpoint ambiguity is resolved (light hedge: router behavior can change). The base (Sep-10) checkpoint stays **not measured**.
- **Kimi K3's 17 exists only @Low effort** ((Max) unscored) — **do not over-read**; measurement-artifact risk.
- **Qwen3.8 Flash ↔ AA "Qwen3.8-Flash-Next" mapping is inferred** (same release date Aug 26 + same price), not confirmed.
- **Muse Spark's AA score prices Meta's endpoint ($1.25/$4.25)**, not the Go Contributor SKU.
- The effort setting Go actually serves per model is **undocumented — open question**. AA name quirks: Grok 4.7's creator is "SpaceXAI"; Beam = "Beam 1.0".

**The one-line summary:** the consensus reversal is real — **Argon (AA 50, Vals launch 69.24%) still leads the Go pair on both boards**, and AA and Vals agree **Argon ≥ K3.1 Pro (46, Vals 62.52%)**, with **Qwen4 Max (43, Vals 63.20%)** the fresh #3. **Argon is now the worst retention on Go (55-day, corrected Nov 18)** — the old privacy-clean claim is withdrawn; K3.1 Pro is the privacy-safe escalation. **Haiku 5.5 (36)** is the best cheap lab model and the best subagent pick; the cheap tier (27–29) is compressed into noise. **DeepSeek V4.1 Flash** remains the volume/value driver (47,619 req/mo measured — see [05](./05-intelligence-per-dollar.md)). Muse Spark Contributor remains the only *paid* training-on-data route on Go (Iceman Free also trains).

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
| AA Index (v5.0.1) | **33 (max)** for the 1017 checkpoint (177.3 tok/s, 1.26s TTFT / 40.0s TFAAT, $0.60/task) — the catalog SKU is "DeepSeek V4.1 Flash 1017", so this is the served product (AA 33 = what you get) | base (Sep-10) checkpoint **not measured (v5.0.1)**, not served; (v4.3.2, retired scale: 45 / 39) |

**V4 Pro 0813** (legacy — retired upstream Sep 14) — 1.6T/49B MoE, 1M ctx, MIT, no vision. AA **23 (max)** on v5.0.1 ((high)=21, (non-reas)=13; (v4.3.2, retired scale: 36)), 94.9 tok/s, $1.77/task. DeepSeek retired it from its own API and routed traffic to V4.1 Flash; Go still lists it separately, but verify what is served.

**Community:** launch thread very positive, but users note reasoning-token burn. Enclave.ai's security team adopted it. OpenCode telemetry shows it as the #1 model by tokens across the entire user base (119T/week) — the crowd's workhorse.

---

### 3.2 Xiaomi MiMo

**MiMo-V2.6-Pro** (Sep 21) — 1.02T/42B sparse MoE, 70 layers, 1M ctx, **native text+image+video+speech**, MIT. AA **30 (29.89)** on v5.0.1 ((v4.3.2, retired scale: 46 — then #1 of all open-weight models in its class)); $0.26/AA task, 54.4 tok/s, 4.06s TTFT (25.8s TFAAT).

Vendor table: DeepSWE 71.9, **TB2.1 89.9**, TB4.0 34.9, ProgramBench 26.5, AutomationBench 53.1, OSWorld 82.0, GDPval-AA 2.1 1673, CyberGym 94.0. Vals Index **57.81%**.

⚠️ **Known issue:** Xiaomi's Sept 27 post documents **tool-call repetition** (OpenCode: Flash 1.02%, Pro 0.54% of turns; up to 41.7% of replayed MiMo-Code samples). Fixed via MOPD distillation, API updated Sept 25. Also poor p95 TTFT (9.1s). [Post](https://mimo.xiaomi.com/blog/mimo-v2-6-tool-call-repetition)

**MiMo-V2.6-Flash** — smaller RL sibling; 67.9 DeepSWE, 87.6 TB2.1 (vendor). **AA 27 (26.73)** on v5.0.1 at **$0.13/AA-task** ((v4.3.2, retired scale: 38)) — still the cheapest smart volume on Go: **47,455 req/mo measured (33,171 heavy), 21,355 AA pts/$** — #2 on the value podium.

**MiMo-V2.5 / Pro** (legacy — retired upstream Oct 21, dropped from the Go catalog Nov 17) — **not measured (v5.0.1)** ((v4.3.2, retired scale: 25/26)). Only useful as volume filler where still reachable; prefer V2.6.

---

### 3.3 Z.ai GLM

**GLM-5.3** (Aug 18; weights Aug 28) — 753B/40B MoE, 1M ctx, **text-only**, always-on reasoning, commercial-restricted license. AA **32 (max; 31.65)** on v5.0.1 ((Low) variant = 23; (v4.3.2, retired scale: 45)), 89.4 tok/s, $5.01/task.

| Benchmark | 5.3 | 5.2 |
|---|---|---|
| Terminal-Bench 3.0 (vendor) | **28.3** | 4.6 |
| TB 3.0 on AA-equivalent scale | 41.9 standardized (best Go) | — |
| DeepSWE v1.1 | 66.9 | 46.2 |
| SWE-bench Pro | — | 62.1 |
| CyberGym | 84.5 | 77.2 |
| Agents' Last Exam | 28.5 | 23.8 |
| Vals Index | 59.85% (5.3) | — |
| Z.ai Code Bench | 34.5 @75K tok | 23.4 @96K |
| LMArena text | 1479 (#26) | 1475 (#32) |

⚠️ NIST/CAISI named GLM-5.3 "the most cyber-capable open-weight model released to date," ~4 months behind the US frontier. Strengths: terminal/agentic + cyber. Weaknesses: no vision, always-reasoning (expensive), verbose, 7%+ hallucination per HN users.

**GLM-5.3-Flash** (Aug 26) — 320B/18B MoE, **MIT**, native multimodal, sparse+linear attention. AA **28 (27.8)** on v5.0.1 at $0.58/task ((v4.3.2, retired scale: 42 at ~$0.25/task)), **AA AutomationBench 60.4%** (highest Go), vendor TB2.1 84.3 but Vals only 62.9 — provider quantization/harness variance is the caveat. Fast (up to 200 tok/s on FlashX; AA measures 57.1). Best cheap automation generalist on the roster; on v5.0.1 **M3.1 Flash is one AA point ahead (29 vs 28 — noise)** and wins on pts/$ (7,286 vs 4,068).

**GLM-5.2** (legacy — superseded by 5.3) — **not measured (v5.0.1)** ((v4.3.2, retired scale: 34)). Documented TB/SWE-Pro numbers only.

---

### 3.4 xAI Grok

**Grok 4.7** (Sep 21) — proprietary, 500K ctx, vision, reasoning low→xhigh. AA **35 (xhigh; 35.49)** on v5.0.1 (high 35.21 / low 31.13; (v4.3.2, retired scale: 46)); 70.7 tok/s, 49.2s TTFT, $7.77/task. AA creator is listed "SpaceXAI". Vendor: CursorBench 4.0 46.3, DeepSWE 71.0, TB4.0 37.6 (xAI) / 33 (AA), EEBench 64.0, Harvey Legal 19.6, HealthBench Prof 56.7. **LMArena ranks it BELOW Grok 4.6** (1442 vs 1453); Design Arena 1224. A reasoning/knowledge specialist that over-spends tokens.

**Grok 4.6** (removed from Go — Zen only) — (v4.3.2, retired scale: AA 44), Vals 71.8, SWE-bench Verified 95.6, TB2.1 78.3 Vals / 88.4 AA, GPQA 95.0, ARC-AGI-2 67.1. Still the best verified Grok generation; use via Zen if you need it.

---

### 3.5 Moonshot Kimi

**Kimi K3.1 Pro** ✨ (Oct 2026; on Go Oct 25) — Moonshot's refreshed flagship; **AA 46 (max; 46.45)** on v5.0.1 — **#2 on Go, behind Argon (50)** ((v4.3.2, retired scale: 55.1, then the Go ceiling)). AA-measured: 31.0 tok/s, 3.92s TTFT (151.0s TFAAT), **$3.68/AA task**, 1M ctx, vision. Go price **$2/$10/$0.20, cache write $2, $15 cap** → **191 req/mo measured (269 heavy)**. Vals Index v2.2 **62.52%** (#4). On v5.0.1 it is no longer the ceiling: Argon is 4 AA points ahead, gives ~4.5× the capacity (862 vs 191) and costs less per Go request ($0.035 vs $0.079 measured). K3.1 Pro keeps its niches: 1M ctx, Max effort, and OmO 5.1.47's K3.1 Pro-specific Sisyphus/Atlas prompts. Independent long-horizon/agentic numbers are still thin — treat the AA score as solid and the vendor agentic claims as 🟡.

**Kimi K3** (Jul 16) — **2.8T total / 104B active**, 93 layers (KDA + Gated MLA), MoonViT-V2 vision, 1M ctx, MXFP4 QAT, always-thinking, open weights under the Kimi K3 license. [HF card](https://huggingface.co/moonshotai/Kimi-K3)

Highlights (max): GPQA 93.5, HLE 43.5/56.0 tools, DeepSWE 67.5, TB2.1 88.3, **SWE-Marathon 42.0**, FrontierSWE 81.2, BrowseComp 91.2, OSWorld 84.8, MMMU-Pro 81.6, MCP-Atlas 84.2, Toolathlon 76.5, **#1 Front-end Code Arena (1679)**, ARC-AGI-2 60.4. AA **17 on v5.0.1 — @Low effort only ((Max) = N/A; do not over-read)**; 46.6 tok/s (max), $2.37/task ((v4.3.2, retired scale: 44)). Weaknesses: sensitivity to thinking history, "excessive proactiveness," explicit UX gap vs Fable 5.

**Kimi K2.7 Code** (Jun 12) — 1T/32B, 256K ctx, thinking-only. Vendor deltas: Kimi Code Bench v2 62.0, Program Bench 53.6, MCP Atlas 76.0. **No independent runs** (**not measured (v5.0.1)**; (v4.3.2, retired scale: 26)), and KernelBench-Hard showed *regression* vs K2.6. "More honest but not more capable."

**Kimi K2.6** (legacy) — superseded.

---

### 3.6 Alibaba Qwen

**Qwen4 Max** ✨ (Nov 16, 2026) — Alibaba's fresh flagship; **984K ctx**. **AA 43 (42.89) on v5.0.1** — the first fresh model to land already scored on the new scale (AA changelog Nov 15 "43"). Vals **63.20% (#11, top Chinese)**. AA-measured: 54.4 tok/s, 5.28s TTFT (147.6s TFAAT), **$3.27/task**. Go price **$1.50/$4.50/$0.075 (cache write $1.875), $15 cap** → **454 req/mo measured (543 heavy)**. New #3 on Go behind Argon and K3.1 Pro. Independent agentic runs are **not measured yet** — AA is the anchor for now.

**Qwen3.8 Max** (Aug 3; 0902 snapshot) — 2.4T/95B, 1M ctx, text+image(+video), reasoning xhigh/medium/low. Prices $2/$6. AA **34 (0902 snapshot)** on v5.0.1 — ⚠ **Go serves the 0803 snapshot, which is unscored** ((v4.3.2, retired scale: 45)); 60.6 tok/s and $10.02/task — still **the most expensive Go model per unit of work**. Verified: **SWE-bench Pro 67.7 (best Go)**, TB2.1 86.6, **OSWorld 86.1 (#1 overall)**, MMMU-Pro 82.3, IFBench 82.8, LMArena WebDev **1688 (#2)**, LMArena Vision **#9** (not #2 — correction), ScreenSpot-Pro 84.5.

**Qwen3.8 Flash** (Aug 26) — 125B + 51B N-gram embeddings, **6B active**, 262K native → 1M, multimodal. **AA 29 (28.58)** on v5.0.1 ((v4.3.2, retired scale: 40)) — ⚠ AA lists it as **"Qwen3.8-Flash-Next"**; mapping inferred (same release date Aug 26 + same price), not confirmed. Vendor: AndroidWorld 84.5, RealWorldQA 88.5, MathVision 90.6, CharXiv 84.6, CoWorkBench 73.9. Thin independent cover beyond AA.

**Qwen3.7 Plus** (May 31) — 1M ctx, multimodal. **Not measured (v5.0.1)** ((v4.3.2, retired scale: 25)). Volume model; ⚠ tiered pricing above 256K.

---

### 3.7 OpenAI GPT Luna

**GPT 6 Luna** (Sep 22) — 1.05M ctx, 128K out, effort none→max, vision, computer-use, hosted shell. $0.10/$0.50. AA **28 (max; 27.86)** on v5.0.1 (spread 28/23/21/18/10/9; (v4.3.2, retired scale: 37–38)), **$0.15/AA task (cheapest frontier-lab model per AA task on v5.0.1)**, 102.6 tok/s, 68.3s TTFT (=TFAAT). Vendor: DeepSWE 66.6, AutomationBench 20.7, OSWorld 52.7, factual error 7.6%. Vals: index 51.2, **TB4.0 13.6, ProgramBench 0.5** — agentically weak.

**GPT 5.6 Luna** (Jul 9) — AA **24 (max; 23.79)** on v5.0.1 (other efforts unscored; (v4.3.2, retired scale: ~36)), Vals SWE-bench **93.0**, TB2.1 84.7, AA Coding Agent Index 71.5, DeepSWE 67.2. Good cheap second opinion, not a marathon agent.

**Context (not on Go):** v5.0.1 anchors — GPT-6.2 Astra (62, new #2), GPT-6.2 Sol (57) / GPT-6 Astra (57, earlier anchor), GPT-6.1 Sol (55), GPT-6.1 Terra (51), GPT-6 Sol (44); see the frontier anchors in §1. ((v4.3.2, retired scale: Astra 53, Sol 47–48, GPT-6.1 Sol 52.)) Pay-for-the-jump targets via Zen.

---

### 3.8 Meta Muse Spark

**Muse Spark 1.3 Contributor** (Sep 2) — 1M ctx, multimodal, max reasoning. AA **37 (max; 36.62)** on v5.0.1 (medium confidence; (v4.3.2, retired scale: 48)) — ⚠ AA prices **Meta's endpoint ($1.25/$4.25), not the Go Contributor SKU**. Design Arena **Website #1**, LMArena WebDev 1623, MRCR v2 8-needle 512K–1M = 98.1 (self-reported), JobBench 64.9, GDPval-AA 1754. ⚠️ **Contributor tier trains on your prompts/completions** — the only training-on-data paid route left on Go. Not for client/PHI.

**Muse Spark 1.2** (Aug 5) — **not measured (v5.0.1)** ((v4.3.2, retired scale: 40, corrected from 45–46)), Design Arena 1318. Contributor terms apply.

---

### 3.9 Tencent Hunyuan

**Hy4 (GA)** (rel Nov 3, 2026; results Nov 4) — the GA of the Hy4 family. **AA 35 (34.56)** on v5.0.1 ("Tencent Hy4"; AA has **no separate Hy4-preview entry**), 95.6 tok/s, 2.89s TTFT (112.8s TFAAT), **$1.03/task**. ⚠ Go lists **two separate SKUs at identical token prices ($0.834/$2.501/$0.042)**: **Hy4 (GA) ($60 cap) ≠ Hy4 preview ($30 cap)** — a new finding this cycle. At those token prices it is the most expensive cheap-tier model on Go.

**Hy4 preview** (Aug 28) — 770B/49B + 10B MTP, 1M ctx, **Apache 2.0**, thinking defaults high. Official blind eval: 2.99 avg vs GLM-5.3 2.92 and Kimi K3 2.94 (203 tasks, 163 Tencent experts). Vendor: **SWE-bench Pro 65.7**, MCP-Atlas 83.7, Toolathlon 74.1, GPQA 92.3 (unverified). **Not measured (v5.0.1)** (the GA is — see above). Over-reasons and over-verifies.

**Hy3** (Apr 22) — 295B/21B, 256K, community license. GPQA 87.2, SWE-bench Verified 74.4, TB2.0 54.4, HLE 30. **Not measured (v5.0.1)** ((v4.3.2, retired scale: 25, corrected from ~34)). Old and weak; volume filler only.

---

### 3.10 Meituan LongCat

**LongCat-2.0** (Jun 30) — 1.6T/~48B + 135B N-gram embedding params, LongCat Sparse Attention, native 1M ctx, **MIT**. Vendor: TB2.1 70.8, SWE-bench Pro 59.5, SWE Multilingual 77.3, FORTE 73.2, BrowseComp 79.9, GPQA-D 88.9. **Not measured (v5.0.1)** ((v4.3.2, retired scale: 19) — the independent score was far below the vendor story). Cheap ($0.30/$1.20, $0.006 cache; 20,266 req/mo measured), but not a quality pick.

**LongCat 2.5 Free** — listed on Go again per the Nov 17 live docs: free/unlimited (limited time), **China-hosted — needs Regions=Global opt-in**. Not on AA. No public model card.

---

### 3.11 MiniMax

**MiniMax M3.1 Flash** ✨ (Oct 2026; on Go Oct 25) — MiniMax's refreshed agentic Flash model: **AA 29 (29.06)** on v5.0.1 ((v4.3.2, retired scale: 43)), **141.3 tok/s**, **1.25s TTFT (46.3s TFAAT)**, **$0.49/AA task**, 1M ctx, vision. Vals Index v2.2 **53.78%**. Go price **$0.15/$0.60/$0.015, $20 cap** → **5,025 req/mo measured (4,975 heavy), 7,286 AA pts/$**. On v5.0.1 it sits in the compressed cheap tier (29 vs GLM-5.3-Flash's 28 — noise), but still wins the value comparison on pts/$ (7,286 vs 4,068) and speed (141.3 vs 57.1 tok/s). Telemetry: #2 by tokens (+92% in a week). Community reports it is the early "Space Bunny" model. This is still the paid quality/value workhorse.

**MiniMax M3** (Jun 1) — 428B/23B, 1M ctx, open weights, multimodal. Vendor: SWE-bench Pro 59.0, TB2.1 66.0, OSWorld 70.06. **AA 19 (18.88)** on v5.0.1 ((v4.3.2, retired scale: 29)) — vendor claims far outrun independent measurement. ⚠ Tiered pricing: **>512K prompts double** ($0.60/$2.40/$0.12).

**MiniMax M2.7** (removed) — (v4.3.2, retired scale: 23), 205K, data/ML specialist only.

---

### 3.12 StepFun Step 5 Preview (paid, promo ended)

**Step 5 Preview** (API Sep 20; Go free Oct 8–15; now **$1.00/$2.70/$0.10 with a $15/mo cap**) — 600B total / **27B active** sparse MoE, 1M ctx, native vision, built for long-horizon reasoning and autonomous execution. **AA 29 (28.53) on v5.0.1** ((v4.3.2, retired scale: 44, independently confirmed)); Vals Index **54.76%**; Vals TB4.0 31.8% matches vendor 33.3%. **Open weights released Oct 15** (BF16 + FP8, HuggingFace + ModelScope) — self-hostable. [StepFun announcement](https://www.stepfun.com/step-5-preview) · [Vals page](https://www.vals.ai/models/stepfun_step-5-preview)

| Benchmark | Step 5 (High) | Kimi K3 (Max) | GLM-5.3 (Max) |
|---|---|---|---|
| AA Intelligence Index (v5.0.1) | **29** | 17 (low only; max N/A) | 32 |
| DeepSWE v1.1 | **67.7** | 67.5 | 66.9 |
| Terminal-Bench 2.1 | 85.0 | 85.0 | 83.9 |
| Terminal-Bench 4.0 | **33.3** | 12.6 | 41.9 |
| StepCodeBench | **49.0** | 43.9 | 40.2 |
| ProgramBench | **80.5** | 77.8 | 72.0 |
| AA-LCR v1.1 (v4.3.2-era eval, retired) | **88.3** | 88.7 | 79.7 |

**Verdict:** the non-AA evidence still says Kimi-class across the board, 2.6× Kimi K3 on TB4.0 — but on AA v5.0.1 it is **29** (old (v4.3.2, retired scale: 44) must not be compared). At the $15 cap it buys **677 req/mo measured (591 heavy)**, and it is self-hostable.

---

### 3.13 NEW — Kimi K3.1 Pro (on Go Oct 25)

**Kimi K3.1 Pro** — Moonshot's mid-October flagship refresh, listed on Go on Oct 25 at **$2.00/$10.00/$0.20 (cache write $2.00), $15/mo**. **AA 46 (max; 46.45) on v5.0.1** — **#2 on Go** behind Argon (50); on the retired scale it scored (v4.3.2, retired scale: 55.1, then the Go ceiling). AA-measured: **31.0 tok/s, 3.92s TTFT (151.0s TFAAT), $3.68/AA task**, 1M ctx, vision. Vals Index v2.2: **62.52%** (#4 of 41, behind Sonnet 5.5, Opus 5.5 and Argon). At the measured fleet profile it costs **$0.07867/request** → **191 req/mo measured** (269 heavy; 5h ~38, week ~96).

**Verdict:** no longer the Go ceiling — a specialist ration. Argon beats it on AA (50 vs 46), on Vals (69.24 vs 62.52), on cost per Go request ($0.035 vs $0.079) and on capacity (862 vs 191 req/mo). Keep K3.1 Pro for what its specific strengths buy you: **1M context, Max effort, and its OmO prompt tooling** — hardest plan/debug/review calls where those matter.

---

### 3.14 NEW — MiniMax M3.1 Flash (on Go Oct 25)

**MiniMax M3.1 Flash** — MiniMax's refreshed Flash model, listed on Go Oct 25 at **$0.15/$0.60/$0.015, $20/mo**. **AA 29 (29.06) on v5.0.1** ((v4.3.2, retired scale: 43)), **141.3 tok/s**, **1.25s TTFT (46.3s TFAAT)**, **$0.49/AA task**, 1M ctx, vision. Vals v2.2 53.78%. At the measured fleet profile: **$0.00398/request** → **5,025 req/mo measured (4,975 heavy)**, **7,286 AA pts/$**. Telemetry: **37T tokens/week, #2 overall, +92%** — the fastest adoption of any new Go model this cycle.

**Verdict:** still the paid quality/value workhorse, but on v5.0.1 it is inside the compressed cheap tier (29 vs GLM-5.3-Flash 28, Qwen3.8 Flash 29 — noise). It keeps the edge on pts/$ (7,286 vs 4,068 for GLM-5.3-Flash) and speed. For high-volume days: DeepSeek V4.1 Flash / MiMo-V2.6-Flash are the volume lanes, M3.1 Flash the quality lane.

---

### 3.15 Gemini 4 Argon — privacy correction & new AA ceiling (on Go since Oct 13)

**Gemini 4 Argon** (GA Sep 30; Go SKU renamed from "Contributor" and cut to **50% off through Nov 30**) — Google's frontier model. **AA 50 (high; 50.41) on v5.0.1 — now the highest-AA model on Go** ((v4.3.2, retired scale: 53, then behind K3.1 Pro)). AA has no max-effort variant (High/Medium only). **Vals Index v2.2 69.24% (#3 of 41)**, **AutomationBench #1 (51.3%)**, **lowest hallucination on AA-Omniscience** (15% wrong guesses vs 29% next best). Vendor claim: DeepSWE 77.9 SOTA (Oct 13).

| Go facts | Value |
|---|---|
| Go price | **$2.00 / $10.00 / $0.10** (50% off; list returns after Nov 30) |
| Go monthly cap | **$30** — Plus **$120** — Teams **$35** |
| Your cost/request | ≈ **$0.0348** (measured mix) → **862 req/mo measured** (728 heavy) |
| Privacy | ⚠️ **Not trained BUT 55-day retention** — corrected Nov 18 (the "0-day / ZDR" claim is withdrawn); worst retention on the Go roster. Footnote: "Requests are retained for up to 55 days for abuse monitoring in accordance with Google's Gemini API Terms" |
| Capacity | 5h ~192 req; week ~480 (measured mix; heavy: 146 / 364) |

**Verdict:** the Go **ceiling (AA 50) and the best hard-task capacity** in one SKU: 862 req/mo measured — 4.5× K3.1 Pro's capacity at ~56% lower cost per request, and 4 AA points *ahead*. But it is **no longer the privacy-safe default**: 55-day retention rules it out for client/PHI work without a contract check — **K3.1 Pro (0-day, not trained, AA 46) is the privacy-safe escalation**. The old "ZDR / trains-on-your-data withdrawn" framing in this repo was **half-right and is now corrected**: training was never the issue; retention is. Still confirm with the client and re-verify the table before PHI work.

---

### 3.16 Removed / stealth models

**Space Bunny** — **removed from Go/Zen**. Revealed Oct 19 as an early **MiniMax M3.1 Flash**; the paid SKU and free stealth are both gone. Use `minimax-m3.1-flash`.

**LongCat 2.5 Preview Free** — the old free window ended; a **LongCat 2.5 Free** SKU is listed again per the Nov 17 live docs (free/unlimited, limited time, **China-hosted — needs Regions=Global**; not on AA).

**Beam Free** (Reflection AI, free since Oct 12) — 501B/23B MoE, **AA 18 (17.73) on v5.0.1** ((v4.3.2, retired scale: 30)), Apache-2.0 weights, 30-day retention, no training, limited regions. AA name "Beam 1.0"; AA prices the public API ($0.40/$1.20) — the Go SKU is free. Good free mid-tier agent, not a frontier alternative.

**Iceman Contributor Free** (Go) — free/unlimited (limited time); **⚠ trains on your data**; not on AA. Never for client work.

**Hy4 Flash Free** (Go) — free/unlimited (limited time); 0-day retention, not trained; not on AA.

**Flint 40B Free** (Zen, Oct 2026) — new free 40B-class model; **30-day retention, may train**. Non-sensitive exploration only.

**Big Pickle** (Zen) — stealth; data used for training. Unknown identity. Do not trust with sensitive code.

---

## 4. Benchmark-source health (as of Nov 17, 2026)

| Source | Status | Notes |
|---|---|---|
| Artificial Analysis | 🟢 healthy | **v5.0.1 current** (v5.0 Oct 27 → v5.0.1 Nov 3 regrade; whole Go roster re-scored); Qwen4 Max added at 43; Performance Benchmarking v3.0.0 (TTFT/TFAAT); retired v4.3.2 scores kept in §1 for history only |
| Vals AI | 🟢 healthy | Index v2.2 — launch values Sonnet 5.5 70.85%, Opus 5.5 70.18%, Argon 69.24% (live board now shows per-lab best only). Verifiable Nov 18: Fable 5.2 **71.31% #1** (new leader) · Carbon 70.45% · GPT-6.2 Astra 67.66% #7 · Wonder Full 66.79% · GPT-6.2 Sol 66.06% #9 · Qwen4 Max 63.20% #11 (top Chinese) · K3.1 Pro 62.52% (confirmed) · DS 1017 61.26% · GLM-5.3 59.85% · Hy4 59.35% · Grok 58.62% · MiMo-Pro 57.81% · Step 5 54.76% · Haiku 54.31% #16 ($2.99/test; #3 Vibe Code Bench 90.44%) · M3.1 Flash 53.78% · Beam 43.42% |
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

**Overall intelligence (Go only, AA v5.0.1):**
1. **Gemini 4 Argon (50, high)** · 2. **Kimi K3.1 Pro (46, max)** · 3. **Qwen4 Max (43)** · 4. Muse Spark 1.3 (37, max) ⚠️ trains · 5. Claude Haiku 5.5 (36, max; spread 35/30/25/19) · 6. Hy4 GA / Grok 4.7 (35) · 8. Qwen3.8 Max (34, 0902 snapshot ⚠️) · 9. DeepSeek V4.1 Flash 1017 (33, max — the served SKU) · 10. GLM-5.3 (32, max; low 23) · 11. MiMo-V2.6-Pro (30) · 12. Step 5 Preview / MiniMax M3.1 Flash / Qwen3.8 Flash (29) · 15. GLM-5.3-Flash / GPT 6 Luna (28) · 17. MiMo-V2.6-Flash (27) · 18. GPT 5.6 Luna (24) · 19. DeepSeek V4 Pro (23, legacy) · 20. MiniMax M3 (19) · 21. Beam Free (18) · 22. Kimi K3 (17, low only ⚠️). **Not measured (v5.0.1):** GLM-5.2 · Kimi K2.7 Code · LongCat-2.0 · Hy3 · Qwen3.7 Plus · Muse Spark 1.2 · DeepSeek base checkpoint (not the served SKU) · Qwen3.8 Max 0803 (the Go SKU) · Kimi K3 (max) · Hy4 preview. *(MiMo-V2.5/-Pro dropped from Go Nov 17 — roster 29→34→32.)* **Not on AA:** Iceman Contributor Free · LongCat 2.5 Free · Hy4 Flash Free.

**Agentic coding (Go only, independent-evidence weighted):**
1. **Gemini 4 Argon** (AA 50, Vals launch 69.24, 55-day retained) · 2. **Kimi K3.1 Pro** (AA 46, Vals 62.52, privacy-safe) · 3. **Qwen4 Max** (AA 43; Vals 63.20%; agentic evidence thin) · 4. Kimi K3 (TB2.1 88.3 / DeepSWE 67.5 verified; AA 17 @low — do not over-read) · 5. GLM-5.3 (Vals 59.85%) · 6. Grok 4.7 (Vals 58.62%) · 7. DeepSeek V4.1 Flash (value king; Vals 61.26%) · 8. GPT 5.6 Luna · 9. **MiniMax M3.1 Flash** (value lane; Vals 53.78%) · 10. MiMo-V2.6-Pro (Vals 57.81%) · 11. GLM-5.3-Flash · 12. Qwen3.8 Max · 13. Step 5 (Vals 54.76%) · 14. Claude Haiku 5.5 (best cheap lab / best subagent; Vals 54.31%) · 15. Hy4 GA (Vals 59.35%) · 16. LongCat-2.0. Free tier: DeepSeek V4.1 Flash Free / GLM-5.3-Flash Free (zero-retention) > Beam Free (18, no training; Vals 43.42%) > LongCat 2.5 Free / Hy4 Flash Free (unmeasured).

**Design/frontend:** Muse Spark 1.3 > Kimi K3.1 Pro / K3 > GLM-5.3 > MiMo-Pro > Qwen3.8 Max. **Value:** MiMo-V2.6-Flash / DeepSeek V4.1 Flash / M3.1 Flash.

**Vision/visual QA:** Qwen3.8 Max (OSWorld #1) > Kimi K3 > Muse Spark 1.3 > MiMo-Pro > Qwen3.8 Flash. For OCR: Qwen3.8 Max/Flash, DeepSeek V4.1 Flash (DocVQA 95.6).

**The one-line summary:** the ceiling and the value story both changed — **Argon is the ceiling (AA 50, 862 req/mo measured, 50%-off through Nov 30) but 55-day retained** — pick it for non-client planning, escalate privacy-safe to K3.1 Pro; the **cheap tier (27–29) is compressed into noise** — pick it on capacity/price/speed/privacy; **Haiku 5.5 (36) is the best cheap lab model**. **K3.1 Pro (46)** is the specialist ration (1M ctx, Max effort), **Qwen4 Max (43)** the fresh #3, and **DeepSeek V4.1 Flash** stays the volume king (47,619 req/mo measured, 10× multiplier).

---

**Next:** [03 — Task Playbook](./03-task-playbook.md) · [04 — Limits & Burn Rate](./04-limits-and-burn-rate.md)
