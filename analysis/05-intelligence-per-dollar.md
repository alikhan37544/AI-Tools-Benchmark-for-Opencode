# 05 — Intelligence per Dollar: Value, Tiers & “Pay More for a Jump”

> **Snapshot: October 1, 2026; refreshed October 13, 16 and 25, 2026.** Intelligence = Artificial Analysis Intelligence Index **v4.3.2**. Costs are **your calibrated per-request cost** from [04](./04-limits-and-burn-rate.md) (7.8k input / 1.1k output+reasoning / 146k cache read), not list prices per token.
>
> 🆕 **Oct 25 — the new stuff:** **Kimi K3.1 Pro (AA 55.1)** is the new intelligence ceiling on Go — but at **988 pts/$** and **269 req/mo**, it is a ration, not a driver. **Gemini 4 Argon (AA 53, 1,286 pts/$, 728 req/mo)** is the better *top-end workhorse* and is now **ZDR/not trained**. **MiniMax M3.1 Flash (AA 43, 10,697 pts/$, 4,975 req/mo)** is the new paid value anchor. **DeepSeek V4.1 Flash’s 1017 checkpoint scores AA 45** at the same price (baseline 39) — upside, not yet the baseline. **Space Bunny and LongCat 2.5 Free are gone**; **Flint 40B Free** is new (may train).

---

## 1. Why flat-plan math is different

On a $10 flat plan, the “price” of using a model isn’t tokens — it’s **how much of that model’s monthly allowance each request consumes**. Your real currency is *requests at a given intelligence level*.

Three metrics matter:

1. **AA points per $ of limit spend** — `AA ÷ $/request`. How efficiently limit-dollars buy intelligence.
2. **Monthly request capacity** — `allowance ÷ $/request`. How much work you can do.
3. **Monthly cognitive throughput** — `AA × monthly capacity`. Intelligence-weighted volume: how much “smart work” the model’s allowance can fund per month.

A model can win on one and lose badly on another (K3.1 Pro has the highest AA but only 269 req/mo; MiMo-Flash has huge capacity but AA 38).

---

## 2. The master value table

| Model | AA | $/req | Req/month | AA points per $ | Monthly cognitive throughput | Grade |
|---|---|---|---|---|---|---|
| **Muse Spark 1.3 Contrib** | 48 | $0.0013 | 46,440 | **37,152** | **2.23M** | A+ (privacy caveat) |
| **MiMo-V2.6-Flash** | 38 | $0.0018 | 33,171 | **21,111** | **1.26M** | **A (cheapest smart volume)** |
| **Claude Haiku 5.5** | 43 (Max) | $0.0028 | 5,375 | 15,357 | 231k | **A− (Max; Med 34)** |
| **DeepSeek V4.1 Flash** | 39 | $0.0031 | 25,484 | 12,426 | 994k | **A+ sustainable** |
| **DeepSeek V4.1 Flash 1017** | **45** | $0.0031 | 25,484 | **14,516** | **1.15M** | **A+ upside (same ID/price)** |
| **MiniMax M3.1 Flash** | 43 | $0.0040 | 4,975 | **10,697** | 214k | **A (new paid value anchor)** |
| **Qwen3.8 Flash** | 40 | $0.0040 | 7,457 | 10,000 | 298k | B+ (AA 40, thin cover) |
| **MiMo-V2.6-Pro** | 46 | $0.0049 | 3,074 | 9,428 | 141k | **A (best premium)** |
| **GLM-5.3-Flash** | 42 | $0.0061 | 9,836 | 6,885 | 413k | A (best cheap automation) |
| **GPT 5.6 Luna** | 35–37 | $0.0058 | 2,586 | 6,379 | 96k | B |
| **Hy3** | **25** | $0.0068 | 8,772 | **3,676** | **219k** | C (corrected 34→25) |
| **MiniMax M3** | 29 | $0.0124 | 4,831 | 2,335 | 140k | C |
| **Qwen3.7 Plus** | 25 | $0.0107 | 5,597 | 2,332 | 140k | C |
| **Step 5 Preview** | 44 | $0.0254 | 591 | 1,733 | 26.0k | **A− (AA 44 capacity)** |
| **Gemini 4 Argon** | 53 | $0.0412 | **728** | **1,286** | 38.6k | **A for the top end (now ZDR)** |
| **Kimi K3.1 Pro** | **55.1** | $0.0558 | **269** | 988 | 14.8k | **B+ (AA ceiling ration)** |
| **GLM-5.3** | 45 | $0.0537 | 279 | 838 | 12.6k | **B+ ration** |
| **Qwen3.8 Max** | 45 | $0.0587 | 256 | 767 | 11.5k | **B+ ration** |
| **Kimi K2.7 Code** | 26 | $0.0395 | 1,517 | 657 | 39k | D (vendor-only) |
| **Kimi K3** | 44 | $0.0837 | 179 | 526 | 7.9k | B+ ration |
| **Grok 4.7** | 46 | $0.0952 | 158 | 483 | 7.3k | B ration |

**Free (∞ pts/$):** **GLM-5.3-Flash Free (AA 42, zero-retention)**, **DeepSeek V4.1 Flash Free (AA 39, zero-retention)**, **Beam Free (AA 30, no training, 30-day)**. **Flint 40B Free** is new but **may train**; MiMo Free/NVIDIA free also train or log.

**Legacy / removed from Go (Zen or deprecated; avoid for new work):** Grok 4.6 (AA 44, 158 req/mo — Zen $2/$6), DeepSeek V4 Flash (AA ~34, 9,448), DeepSeek V4 Pro (AA 36, 1,017), GLM-5.2 (AA 34, 1,117), MiMo-V2.5 (AA 25, 33,171), MiMo-V2.5-Pro (AA 26, 3,074), Kimi K2.6 (—, 1,706), MiniMax M2.7 (AA 23), Space Bunny (removed), LongCat 2.5 Free (removed).

*(Other unmeasured: Hy4 — see tier table. LongCat-2.0 is AA 19. Haiku score is Max-effort; default medium is AA 34.)*

> **Haiku 100K-tier footnote:** the 5,375 req/mo and 15,357 pts/$ figures assume a prompt of **≤100K tokens**. The frozen profile (146k cache read + 7.8k input) is above that boundary, so Haiku is billed at the **>100K tier** ($0.50/$2.50/$0.05 per 1M): the same heavy request costs **~$0.014** and the $15 cap buys **~1,075 req/mo** — about **3,000 pts/$**. Keep Haiku on explore/subagent contexts under 100K; above that, DeepSeek V4.1 Flash or MiMo-V2.6-Flash is cheaper and stronger.

### The four winners (updated)

1. **Most intelligence per limit-dollar — Muse Spark 1.3 Contributor** (37,152 pts/$; 2.23M monthly throughput) — still the mathematical winner, with the Contributor data-policy caveat (trains on your prompts).
2. **Best free intelligence — GLM-5.3-Flash Free** (AA 42, zero-retention, $0/req) with **DeepSeek V4.1 Flash Free** (AA 39, zero-retention) as the high-capacity twin. **Beam Free** (AA 30) covers the no-training case.
3. **Best sustainable intelligence per dollar — DeepSeek V4.1 Flash.** 25.5k requests/month, 12,426 pts/$ (14,516 if 1017 is served), 209–232 tok/s, native vision — and the free twin makes the marginal cost $0.
4. **Highest raw intelligence — Kimi K3.1 Pro (AA 55.1)**: 269 req/mo at 988 pts/$. **Gemini 4 Argon (AA 53)** is the better *top-end capacity* buy: 728 req/mo at 1,286 pts/$, **Vals #1 among Go models (69.24%)**, and **ZDR/not trained** — the old training caveat is withdrawn.

### AA “cost to run the entire Intelligence Index” (list-price basis, AA data)

| Model | Cost to run full index |
|---|---|
| GLM-5.3-Flash | **$280** |
| DeepSeek V4.1 Flash | ~$300 |
| MiMo-V2.6-Pro | ~$350 (at $0.13/task × ~2,700 tasks) |
| **Gemini 4 Argon** (at 50% off) | ~$700–900 |
| DeepSeek V4 Pro (legacy) | $1,122 |
| GLM-5.3 | $2,503 |
| Kimi K3 | **$3,658** |

The premium models cost **9–13× more per unit of measured work** than the cheap tier — Argon at 50% off is the cheapest AA 53-class run ever measured. **K3.1 Pro** is **$2.11 per AA task** (AA); its full-index figure is not yet in the same table, but at AA 55.1 it is the most expensive per unit of work on Go.

---

## 3. Tier structure

### Tier 0 — Free (limited-time windows)
**GLM-5.3-Flash Free (AA 42, zero-retention) · DeepSeek V4.1 Flash Free (AA 39, zero-retention) · Beam Free (AA 30, no-training) · Flint 40B Free (may train) · MiMo-V2.6-Flash Free (may train) · Nemotron 3.5 Super VL / 3 Ultra / 3.5 Lightning Free (logged) · Big Pickle (may train) · Jev 1.13 (structured decisions).**
Unlimited, zero-allowance. The two zero-retention twins can carry real (non-critical) work — the best free floor this repo has seen. **Flint/MiMo/NVIDIA/Big Pickle train or log on data — never for client work.**

### Tier 1 — Workhorses (effectively unlimited at your pace)
**DeepSeek V4.1 Flash · MiMo-V2.6-Flash · MiniMax M3.1 Flash · GLM-5.3-Flash · Muse Spark 1.3 Contributor · LongCat-2.0 · Hy3 · Qwen3.8 Flash · Claude Haiku 5.5 · Step 5 Preview ($15).**
$15–80 allowances, 2.5k–46k requests/month at your profile. This is where 90% of your work lives. Best quartet: **DeepSeek V4.1 Flash (general) + its free twin (bulk) + MiniMax M3.1 Flash (paid quality/value) + GLM-5.3-Flash (cheap automation / free twin)** — plus **Haiku 5.5 for subagents** and **Step 5 for AA 44 capacity**.

### Tier 2 — Premium rations ($15–30, high quality-per-call)
**MiMo-V2.6-Pro (AA 46) · Gemini 4 Argon (AA 53, $30, ZDR) · GPT 6 Luna (AA 38) · GPT 5.6 Luna · Hy4 preview.**
1k–5k requests/month (Argon ~728 at your profile but the best per-task quality on independent agentic boards). Use for planning, hard debugging, design review, OCR verification. **Argon is now the privacy-safe top-end default**; MiMo-V2.6-Pro for cheaper reasoning.

### Tier 3 — Frontier rations ($15, ~150–280 requests/month)
**Kimi K3.1 Pro (AA 55.1) · Kimi K3 (AA 44) · GLM-5.3 (AA 45) · Qwen3.8 Max (AA 45) · Grok 4.7 (AA 46).**
~1–5 substantial tasks per week each (K3.1 Pro is the smallest at ~2–5/month). Reserve for what cheap models fail at: multi-hour refactors, hard architecture, marathon debugging, visual QA on OSWorld-class tasks.

### Tier 4 — Beyond Go (the real frontier)
**Claude Opus 5.5 (AA 58) · GPT-6 Astra / Fable 5.1 (AA 53) · Muse Wonder Full (AA 56) / Muse Wonder (52) · GPT-6.1 Sol (AA 52).**
Not on Go. Available via **GitHub Copilot** or Zen pay-as-you-go. Watch **Muse Wonder** (Meta, Oct 12 — AA 52/56) for the next escalation-slot change.

---

## 4. “Pay a little more, maybe run out of limits, but get a huge jump”

Each row is a switch from **DeepSeek V4.1 Flash** (your baseline, AA 39):

| Switch to | ΔAA | Cost/req | Capacity change | When the jump is worth it |
|---|---|---|---|---|
| **DeepSeek V4.1 Flash Free / GLM-5.3-Flash Free** | **+0 / +3** | **×0 (free!)** | 25.5k → **∞** | Always, for non-critical work — zero-retention twins of the workhorse tier. |
| **Muse Spark 1.3 Contrib** | **+9** | **×0.42 (cheaper!)** | 25.5k → 46.4k (**+82%**) | Always — if the data policy is acceptable (it trains). |
| **MiniMax M3.1 Flash** | **+4** | **×1.3** | 25.5k → 4,975 (−80%) | The best paid quality step-up: AA 43 at 4,975 req/mo. |
| **MiMo-V2.6-Pro** | **+7** | ×1.6 | 25.5k → 3.1k (−88%) | Any task where first-try success matters; still only $0.005/req. |
| GLM-5.3-Flash | +3 | ×2.0 | 25.5k → 9.8k (−61%) | Frontend/docs/automation quality step-up; free twin if data is open. |
| Claude Haiku 5.5 | +4 (Max) | ×0.9 | 25.5k → 5.4k (−79%) | Subagents, quick edits, compactions — Sonnet-class coding in Copilot tests. |
| **Step 5 Preview** | **+5** | ×8.2 | 25.5k → **591** (−98%) | AA 44 capacity; open weights = self-host option. |
| **Gemini 4 Argon** | **+14** | ×13.3 | 25.5k → **728** (−97%) | The ceiling for hard/non-convergent tasks — **now ZDR**, 728 req/mo, Vals #1 Go. |
| **Kimi K3.1 Pro** | **+16.1** | ×18.0 | 25.5k → **269** (−99%) | The absolute AA ceiling: hardest architecture/marathon work, 1M ctx. |
| **GLM-5.3** | **+6** | ×17.3 | 25.5k → **279** (−98.9%) | Hard terminal/standardized-harness tasks, security work, deep refactors. |
| **Qwen3.8 Max** | **+6** | ×18.9 | 25.5k → **256** (−99.0%) | Visual QA (OSWorld #1), screenshot/vision verification. |
| **Kimi K3** | **+5** | ×27 | 25.5k → **179** (−99.3%) | Multi-hour marathons, 1M-context legacy code; superseded by K3.1 Pro. |
| **Grok 4.7** | **+7** | ×30.7 | 25.5k → **158** (−99.4%) | Deep reasoning specialist; privacy-safe Grok since 4.6 left Go. |
| **Claude Opus 5.5** (not Go) | **+19** | ~×100–300 | ~50–150 req/mo via Copilot | Genuinely impossible tasks; must-not-fail deliverables. |

### How to think about “huge jump” economics

- **Retry math:** if DeepSeek V4.1 Flash needs 3 attempts where Opus 5.5 needs 1, DeepSeek still costs **~100–300× less**. So for *convergent* tasks (bugs you can reproduce, code you can test), cheap-model retries beat premium every time.
- **Premium is worth it when:** failure is expensive (production deploy, security, data migration), the task is **non-convergent** (one-shot long-horizon planning, ambiguous architecture), or cheap models demonstrably loop. **Argon at AA 53 is the new “non-convergent” workhorse** — 728 req/mo, ZDR, Vals #1 Go. **K3.1 Pro** is the escalation when AA 55.1 matters more than volume.
- **The rational portfolio (Oct 25):** ~50% DeepSeek V4.1 Flash (+free twin for bulk) + ~15% MiniMax M3.1 Flash (paid value) + ~10% free GLM-5.3-Flash + ~8% MiMo-Flash/Haiku 5.5 (explore) + ~8% Argon (planning/agentic, ZDR) + ~5% K3.1 Pro (hardest) + ~2% Step 5/MiMo-Pro + ~1% Qwen3.8 Max (visual) + <1% Opus-class. This uses every model’s independent allowance and rarely hits any single cap.

---

## 5. Value vs the outside world (Go vs BYOK)

- **The multiplier is the core Go deal:** $10 buys up to $80 of usage at list rates (DeepSeek), $60 (MiMo-Flash/GLM-Flash/Hy3/LongCat/M3/K2.7/Muse), $30 (Argon/Qwen Flash/Hy4), or $15 (most premium rations). Per-model detail in [12](./12-opencode-vs-direct.md).
- **Go vs direct API:** a light user (100M tokens/month at agentic cache mix) might spend $25–30 on DeepSeek’s API, making Go’s $10 superior; very light users (<$10 equivalent) are better off pure BYOK. **Kimi Code/Z.ai/Xiaomi/StepFun** can beat Go for single-model focus — see [13](./13-best-value-coding-plans.md).
- **Revealed preference (telemetry, week to Oct 25):** DeepSeek V4.1 Flash **119T** tokens (#1, +39%), **MiniMax M3.1 Flash 37T (#2, +92%)**, GLM-5.3-Flash 8.9T, Muse Spark 7.6T (−76%), MiMo-Flash 7.2T, Beam 5.3T. The market has already voted: **cheap near-frontier models win the bulk of agent traffic**, and M3.1 Flash is the fastest-rising paid model.
- **Zen overflow** is the flexible pressure valve: keep **Extra Usage** enabled so Go gracefully degrades instead of blocking. Zen now also carries free DS/GLM twins and the paid Argon (50% off through Nov 30).
- **Go Plus verdict:** worth it if your usage concentrates on GLM-5.3 (8×), Argon (4× → $120), M3.1 Flash (4× → $80), or the $15-tier rations (4×); poor for DeepSeek V4.1 Flash/MiMo/Muse (2×). For DeepSeek-heavy users, **Go + Zen balance > Go Plus**.

---

## 6. The single most important value conclusion

> **The ceiling and the floor both moved in October — in opposite directions.**
>
> The raw intelligence ceiling is now **Kimi K3.1 Pro (AA 55.1)**, but at **269 heavy requests/month** it is a scalpel, not a driver. The better *top-end workhorse* is **Gemini 4 Argon (AA 53, 728 req/mo)** — and its **ZDR correction removes the data-rights tax** that made the Oct 16 recommendation conditional. The paid value anchor is **MiniMax M3.1 Flash (AA 43, 4,975 req/mo, $0.0020/req plan-effective)**, which dominates GLM-5.3-Flash on both axes. The volume king is still **DeepSeek V4.1 Flash (AA 39, 25.5k req/mo, 8× face value)**, with the **1017 checkpoint’s AA 45** as free upside.
>
> The winning strategy is **portfolio routing v4**: bulk on **DeepSeek V4.1 Flash + its free twin**, paid quality on **M3.1 Flash**, free quality on **GLM-5.3-Flash Free**, explore on MiMo-Flash/Haiku 5.5, planning/agentic ceiling on **Argon (ZDR, 728 req/mo)**, the absolute hard 5% on **K3.1 Pro (269 req/mo)**, visual QA on **Qwen3.8 Max**, and keep the $15 rations for the few tasks where their specific strengths matter. Escalate outside Go only for must-not-fail work.

---

**Next:** [06 — Free Models & Privacy](./06-free-models-and-privacy.md) · [07 — Recommended Config](./07-recommended-config.md)
