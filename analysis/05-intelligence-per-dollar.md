# 05 — Intelligence per Dollar: Value, Tiers & “Pay More for a Jump”

> **Snapshot: October 1, 2026; refreshed October 13, 16, 25 and November 17, 2026 — full AA v5.0.1 re-baseline.** Intelligence = Artificial Analysis Intelligence Index **v5.0.1** (Nov 3, 2026 regrade). Every old score is **(v4.3.2, retired scale)** — history only, never mixed into a table or comparison. Costs are **measured per-request costs** on the **MEASURED profile** (30-day provider-side logs, both Go accounts, all machines — see [04](./04-limits-and-burn-rate.md) §0): **3,477 input / 768 output+reasoning / 166k cache-read** per request (+~5k cache-write where a model bills it) — the realistic fleet average, subagent traffic included. The old frozen **heavy mix** (7.8k in / 1.1k out / 146k cache) is kept as the conservative secondary column labeled "heavy".
>
> 🆕 **Nov 17 — the new stuff:** the value podium is **Muse Spark 1.3 (44,404 pts/$, ⚠ trains on data) · MiMo-V2.6-Flash (23,145) · DeepSeek V4.1 Flash (17,368 — 52,632 req/mo measured, 10× multiplier)**. **Argon (AA 50, 1,601 pts/$, 961 req/mo measured)** is now **both the intelligence ceiling and the best top-end value** — **K3.1 Pro (AA 46)** is the ration. The cheap tier (27–29) is compressed into noise, and **Haiku 5.5 (36) is the best cheap lab model**. *(Earlier delta notes in this file are v4.3.2-era history.)*

---

## 1. Why flat-plan math is different

On a $10 flat plan, the “price” of using a model isn’t tokens — it’s **how much of the shared monthly allowance each request consumes** (normalized by that model's limit). Your real currency is *requests at a given intelligence level*.

Four metrics matter:

1. **AA points per $ of limit spend** — `AA ÷ $/request`. How efficiently limit-dollars buy intelligence.
2. **Monthly request capacity** — `allowance ÷ $/request`, on the **measured profile** (primary) and the **heavy mix** (conservative).
3. **Break-even vs $10** — requests/month at which the plan's $10 equals paying Go list prices per-token; also reads as "requests bought per $10 of list spend".
4. **Go multiplier** — face value of the monthly allowance: `cap ÷ $10` (DeepSeek's **10×** is the biggest on the platform).

A model can win on one and lose badly on another (K3.1 Pro has AA 46 but only 259 req/mo measured; MiMo-V2.6-Flash has 51,433 req/mo but AA 27).

---

## 2. The master value table (MEASURED profile — primary)

Sorted by AA pts/$. AA = v5.0.1. Heavy = the frozen conservative mix. All numbers are the computed basis (measured profile).

| Model | AA | $/req | Req/mo (measured) | Req/mo (heavy) | AA pts/$ | Break-even vs $10 | Go mult | Role |
|---|---|---|---|---|---|---|---|---|
| **Muse Spark 1.3 Contrib** | 37 (max) | $0.00083 | **72,007** | 46,440 | **44,404** | 12,001 | 6.0× | 🥇 value — **⚠ trains on data** |
| **MiMo-V2.6-Flash** | 27 | $0.00117 | **51,433** | 33,171 | **23,145** | 8,572 | 6.0× | 🥈 value — cheapest smart volume |
| **DeepSeek V4.1 Flash** | 33 (1017) | $0.00190 | **52,632** | 32,258 | **17,368** | 5,263 | **10.0×** | 🥉 value — volume king |
| **Claude Haiku 5.5 (≤100K)** | 36 (max) | $0.00302 | 4,973 | 5,376 | **11,934** | 3,315 | 1.5× | best cheap lab / subagent |
| **MiMo-V2.6-Pro** | 30 | $0.00278 | 5,391 | 3,074 | **10,782** | 3,594 | 1.5× | premium value |
| **GPT 6 Luna** | 28 (max) | $0.00302 | 4,973 | 5,376 | 9,282 | 3,315 | 1.5× | cheap lab |
| **MiniMax M3.1 Flash** | 29 | $0.00347 | 5,760 | 4,975 | 8,352 | 2,880 | 2.0× | paid quality/value |
| **Qwen3.8 Flash** | 29 | $0.00454 | 6,611 | 7,457 | 6,390 | 2,204 | 3.0× | thin independent cover |
| **GLM-5.3-Flash** | 28 | $0.00588 | 10,196 | 9,836 | 4,758 | 1,699 | 6.0× | cheap automation |
| **GPT 5.6 Luna** | 24 (max) | $0.00619 | 2,425 | 2,586 | 3,879 | 1,616 | 1.5× | second opinion |
| **DeepSeek V4 Pro (legacy)** | 23 (max) | $0.00747 (off-peak basis; peak = 2×) | 2,009 | 1,423 | 3,080 | 1,339 | 1.5× | legacy — avoid |
| **Hy4 (GA)** | 35 | $0.01179 | 5,088 | 3,899 | 2,968 | 848 | 6.0× | best mid-tier AA |
| **Claude Haiku 5.5 (>100K)** | 36 (max) | $0.01508 | 995 | 1,075 | 2,387 | 663 | 1.5× | what the fleet mix bills |
| **Gemini 4 Argon** | 50 (high) | $0.03123 | **961** | 728 | **1,601** | 320 | 3.0× | **ceiling + best top-end value** (ZDR; 50%-off to Nov 30) |
| **MiniMax M3** | 19 | $0.01192 | 5,032 | 4,831 | 1,593 | 839 | 6.0× | capacity, low AA |
| **Qwen4 Max** | 43 | $0.03049 | 492 | 543 | 1,410 | 328 | 1.5× | fresh #3 (rel Nov 16) |
| **Step 5 Preview** | 29 | $0.02215 | 677 | 591 | 1,309 | 451 | 1.5× | open weights |
| **Kimi K3.1 Pro** | 46 (max) | $0.05783 | 259 | 269 | 795 | 173 | 1.5× | the ration — 1M ctx / Max effort |
| **GLM-5.3** | 32 (max) | $0.05140 | 292 | 279 | 623 | 195 | 1.5× | terminal/cyber ration |
| **Qwen3.8 Max** | 34 (0902 ⚠) | $0.06556 | 229 | 256 | 519 | 153 | 1.5× | visual-QA ration (OSWorld #1) |
| **Grok 4.7** | 35 (xhigh) | $0.09455 | 159 | 158 | 370 | 106 | 1.5× | reasoning ration |
| **Kimi K3** | 17 (low ⚠) | $0.08674 | 173 | 179 | 196 | 115 | 1.5× | ⚠ low-only score — do not over-read |
| **Beam Free** | 18 | $0 | ∞ | ∞ | ∞ | — | free | free mid-tier |

> **DeepSeek V4 Pro basis note:** the row's $0.00747/req is **off-peak basis; peak = 2×** (the 28% peak blend was applied only to V4.1 Flash's measured $0.00190). Blended at 28% peak it would be ≈$0.00956/req → 1,569 req/mo · 2,406 pts/$ · break-even 1,046.

**Free (∞ pts/$):** **GLM-5.3-Flash Free (AA 28, zero-retention)** · **DeepSeek V4.1 Flash Free (AA 33 for the 1017 checkpoint; base checkpoint not measured — zero-retention)** · **Beam Free (AA 18 on v5.0.1 — (v4.3.2, retired scale: 30); no training, 30-day retention)** · **LongCat 2.5 Free (not on AA — China-hosted, needs Regions=Global)** · **Hy4 Flash Free (not on AA, zero-retention)**. ⚠ **Iceman Contributor Free, Flint 40B Free and the MiMo free tier train on data** — never for client work.

**AA-unmeasured (v5.0.1) — capacity only:** LongCat-2.0 ($0.00296/req → 20,266 req/mo, 6.0×) · Hy3 ($0.00674 → 8,900) · Qwen3.7 Plus ($0.01176 → 5,103) · Kimi K2.7 Code ($0.03791 → 1,583) · GLM-5.2 legacy ($0.05140 → 1,167) · Muse Spark 1.2 (same price as 1.3 → 72,007 ⚠ trains) · MiMo-V2.5 & -Pro (same as the V2.6 rows — dropped from the Go catalog Nov 17).

**Legacy / removed from Go (Zen or deprecated; avoid for new work):** Grok 4.6 (Zen only), DeepSeek V4 Flash (retired), Kimi K2.6, MiniMax M2.7, Space Bunny (revealed as an early M3.1 Flash). Their headline scores are all (v4.3.2, retired scale).

> **Haiku two-tier pricing:** the measured mix (170k prompt) **always bills the >100K tier** ($0.50/$2.50/$0.05 per 1M): **$0.01508/req → 995 req/mo, 2,387 pts/$**. The **≤100K row** ($0.10/$0.50/$0.01 → **$0.00302/req, 4,973 req/mo, 11,934 pts/$**) is the **subagent-context option** — keep explore/subagent contexts under 100K. Above that boundary, DeepSeek V4.1 Flash or MiMo-V2.6-Flash is cheaper and stronger.

### The winners on v5.0.1

1. **Most intelligence per limit-dollar — Muse Spark 1.3 Contributor** (44,404 pts/$; 72,007 req/mo measured) — the mathematical winner, with the data-policy caveat: **it trains on your prompts**.
2. **Best free intelligence — the free twins.** DeepSeek V4.1 Flash Free and GLM-5.3-Flash Free (both zero-retention) can carry real non-critical work; **Beam Free** covers the no-training case (AA 18); LongCat 2.5 Free / Hy4 Flash Free round out the floor (unmeasured on AA).
3. **Best sustainable intelligence per dollar — DeepSeek V4.1 Flash.** **52,632 requests/month measured** (32,258 heavy), **17,368 pts/$**, **10× multiplier** — and the free twin makes the marginal cost $0.
4. **Highest raw intelligence AND best top-end value — Gemini 4 Argon (AA 50).** 1,601 pts/$ at 961 req/mo measured, **ZDR/not trained**, 50%-off through Nov 30. **K3.1 Pro (AA 46)** is the ration (259 req/mo, 795 pts/$) — reserve it for 1M-context and Max-effort work. **Haiku 5.5 (AA 36)** is the best cheap lab model and the best subagent pick (11,934 pts/$ at ≤100K).

### AA cost per task (v5.0.1 — AA's measured token usage across the 9-eval workload)

| Model | AA $/task | Model | AA $/task |
|---|---|---|---|
| MiMo-V2.6-Flash | **$0.13** | MiniMax M3 | $1.29 |
| GPT 6 Luna | $0.15 | DeepSeek V4 Pro | $1.77 |
| MiMo-V2.6-Pro | $0.26 | Step 5 Preview | $2.35 |
| Beam Free | $0.28 | Kimi K3 | $2.37 |
| GPT 5.6 Luna | $0.33 | Muse Spark 1.3 | $2.39 |
| Claude Haiku 5.5 | $0.41 | Qwen4 Max | $3.27 |
| MiniMax M3.1 Flash | $0.49 | Kimi K3.1 Pro | $3.68 |
| Qwen3.8 Flash | $0.57 | Gemini 4 Argon | $4.97 |
| GLM-5.3-Flash | $0.58 | GLM-5.3 | $5.01 |
| DeepSeek V4.1 Flash 1017 | $0.60 | Grok 4.7 | $7.77 |
| Hy4 (GA) | $1.03 | Qwen3.8 Max | $10.02 |

AA's **Cost per Task** = weighted-average USD to complete one index task from actual measured token usage (input, cache hit, cache write, reasoning, answer prices) ÷ task count — **not** AA "Price (Blended)". The old v4.3.2-era "cost to run the entire index" totals are **(v4.3.2, retired scale — history only)** and are not carried over to the new scale. Qwen3.8 Max remains the most expensive Go model per unit of work; MiMo-V2.6-Flash the cheapest measured.

---

## 3. Tier structure

### Tier 0 — Free (limited-time windows)
**GLM-5.3-Flash Free (AA 28, zero-retention) · DeepSeek V4.1 Flash Free (AA 33/1017, zero-retention) · Beam Free (AA 18, no training, 30-day) · LongCat 2.5 Free (China-hosted — needs Regions=Global) · Hy4 Flash Free (zero-retention) · Flint 40B Free (may train) · MiMo-V2.6-Flash Free (may train) · Iceman Contributor Free (trains on data).**
Unlimited, zero-allowance. The zero-retention trio can carry real (non-critical) work. **Iceman / Flint / MiMo free train or log on data — never for client work.**

### Tier 1 — Workhorses (effectively unlimited at your pace)
**DeepSeek V4.1 Flash (52,632/mo measured) · Muse Spark 1.3 Contrib (72,007, ⚠ trains) · MiMo-V2.6-Flash (51,433) · LongCat-2.0 (20,266, AA unmeasured) · GLM-5.3-Flash (10,196) · Hy3 (8,900, AA unmeasured) · Qwen3.8 Flash (6,611) · MiniMax M3.1 Flash (5,760) · Hy4 GA (5,088) · MiniMax M3 (5,032) · Claude Haiku 5.5 ≤100K (4,973 — subagent contexts).**
$15–100 allowances, 5k–72k requests/month measured. This is where 90% of your work lives. Best quartet: **DeepSeek V4.1 Flash (general/volume) + its free twin (bulk) + MiniMax M3.1 Flash (paid quality) + GLM-5.3-Flash (cheap automation)** — plus **Haiku 5.5 for subagents** and **MiMo-V2.6-Flash for cheap smart volume**.

### Tier 2 — Quality step-ups (AA 24–35, 0.7k–5.4k req/mo)
**Hy4 GA (35) · MiMo-V2.6-Pro (30) · GPT 6 Luna (28) · Step 5 Preview (29, open weights) · GPT 5.6 Luna (24).**
Smoother than the volume lane, far cheaper than the rations. Use for planning drafts, hard debugging, design review.

### Tier 3 — Top-end (the new shape: ceiling = value)
**Gemini 4 Argon (AA 50 — ceiling AND best top-end value; 961 req/mo measured; ZDR; 50%-off through Nov 30) · Qwen4 Max (AA 43 — fresh #3, 492 req/mo) · Kimi K3.1 Pro (AA 46 — the ration at 259 req/mo; 1M ctx + Max effort where they matter).**

### Tier 4 — Specialist rations ($15, ~160–290 req/mo)
**Grok 4.7 (35 — deep-reasoning) · Qwen3.8 Max (34 ⚠ 0902 snapshot — visual QA, OSWorld #1) · GLM-5.3 (32 — terminal/cyber) · Kimi K3 (17 ⚠ low-only — marathon legacy code).**
~1–6 substantial tasks per week each. Reserve for what cheap models fail at.

### Tier 5 — Beyond Go (the real frontier, AA v5.0.1)
**Claude Fable 5.2 (65) · Gemini 4 Carbon (60) · Claude Opus 5.5 (59) · GPT-6 Astra (57) · Claude Sonnet 5.5 (55) / GPT-6.1 Sol (55) · Gemini 4 Hydrogen (54) · GPT-6.1 Terra (51) · Muse Wonder Full (50) · Claude Fable 5.1 (50 xhigh / 49 max — deprecated but benchmarked every 18h; $12.99/task at max; bare "Claude Fable 5" is an unscored stub) · GPT-6 Sol (44).**
Not on Go. Available via **GitHub Copilot** or Zen pay-as-you-go.

---

## 4. “Pay a little more, maybe run out of limits, but get a huge jump”

Each row is a switch from **DeepSeek V4.1 Flash** (your baseline — **AA 33** for the 1017 checkpoint; the base checkpoint is not measured (v5.0.1)). Capacity = req/mo on the measured profile (52,632 baseline).

| Switch to | ΔAA | $/req (vs DeepSeek) | Capacity | When the jump is worth it |
|---|---|---|---|---|
| **DeepSeek V4.1 Flash Free / GLM-5.3-Flash Free** | **n/a / −5** (DS Free = base ckpt, unmeasured; GLM Free = 28 vs 33) | **$0 (×0 — free!)** | 52.6k → **∞** | Always, for non-critical work — zero-retention twins of the workhorse tier. |
| **Muse Spark 1.3 Contrib** | **+4** | $0.00083 (**×0.44 — cheaper!**) | → 72,007 (+37%) | Always — if the data policy is acceptable (⚠ it trains). |
| **MiMo-V2.6-Flash** | −6 | $0.00117 (×0.6) | → 51,433 (−2%) | Bulk/explore lane: same capacity, 40% cheaper, 6 AA lower. |
| **Claude Haiku 5.5 (≤100K / >100K)** | **+3** | $0.00302 (×1.6) / $0.01508 (×7.9) | → 4,973 / 995 | Subagents, quick edits, compactions — best cheap lab model. |
| **MiMo-V2.6-Pro** | −3 | $0.00278 (×1.5) | → 5,391 | Any task where first-try success matters; still only $0.0028/req. |
| **MiniMax M3.1 Flash** | −4 | $0.00347 (×1.8) | → 5,760 | The paid quality lane: 141 tok/s, 1.25s TTFT, 8,352 pts/$. |
| **Hy4 (GA)** | **+2** | $0.01179 (×6.2) | → 5,088 | Best AA under the top end, at workhorse capacity. |
| **Gemini 4 Argon** | **+17** | $0.03123 (×16.4) | → **961** (−98%) | **The jump**: ceiling + best top-end value, ZDR, 50%-off to Nov 30. |
| **Qwen4 Max** | **+10** | $0.03049 (×16.0) | → **492** (−99%) | Fresh flagship (rel Nov 16), 984K ctx, scored on v5.0.1 out of the box. |
| **Kimi K3.1 Pro** | **+13** | $0.05783 (×30) | → **259** (−99.5%) | 1M ctx + Max effort — the specialist ration. |
| **GLM-5.3** | −1 | $0.05140 (×27) | → 292 (−99.4%) | Hard terminal/standardized-harness tasks, security work, deep refactors. |
| **Qwen3.8 Max** | +1 (0902 ⚠) | $0.06556 (×34.5) | → 229 (−99.6%) | Visual QA (OSWorld #1), screenshot/vision verification. |
| **Kimi K3** | −16 (low ⚠) | $0.08674 (×45.7) | → 173 (−99.7%) | Multi-hour marathons on 1M-context legacy code; superseded by K3.1 Pro. |
| **Grok 4.7** | +2 | $0.09455 (×49.8) | → 159 (−99.7%) | Deep-reasoning specialist. |
| **Claude Opus 5.5** (not Go) | **+26** | ~×100–300 (estimate) | ~50–150 req/mo via Copilot | Genuinely impossible tasks; must-not-fail deliverables. |

### How to think about “huge jump” economics

- **Retry math:** if DeepSeek V4.1 Flash needs 3 attempts where Opus 5.5 (AA 59) needs 1, DeepSeek still costs **orders of magnitude less** (~100–300×, estimate unchanged from the Oct 25 cycle). So for *convergent* tasks (bugs you can reproduce, code you can test), cheap-model retries beat premium every time.
- **Premium is worth it when:** failure is expensive (production deploy, security, data migration), the task is **non-convergent** (one-shot long-horizon planning, ambiguous architecture), or cheap models demonstrably loop. **Argon at AA 50 is the new “non-convergent” workhorse** — 961 req/mo, ZDR, Vals #1 of the Go models. **K3.1 Pro** is the escalation when 1M context or Max effort matters more than volume.
- **The rational portfolio (Nov 17):** ~50% DeepSeek V4.1 Flash (+free twin for bulk) + ~15% MiniMax M3.1 Flash (paid quality) + ~10% free GLM-5.3-Flash + ~8% MiMo-V2.6-Flash/Haiku 5.5 (explore/subagents) + ~8% Argon (planning/agentic, ZDR) + ~5% K3.1 Pro (1M ctx / Max effort) + ~2% Step 5/MiMo-V2.6-Pro + ~1% Qwen4 Max/Qwen3.8 Max (visual) + <1% Opus-class. This concentrates usage on the high solo-coverage lanes — the models are one shared allowance (normalized per model limit), so those lanes consume the least of it per request.

---

## 5. Value vs the outside world (Go vs BYOK)

- **The multiplier is the core Go deal:** $10 buys up to **$100 of usage** at list rates (**DeepSeek V4.1 Flash, 10×**), **$60** (MiMo-V2.6-Flash, GLM-5.3-Flash, Muse Spark, Hy4 GA, LongCat-2.0, MiniMax M3 — 6×), **$30** (Argon, Qwen3.8 Flash — 3×), **$20** (MiniMax M3.1 Flash — 2×), or **$15** (the premium rations — 1.5×). Per-model detail in [12](./12-opencode-vs-direct.md).
- **Go vs direct API:** a light user (100M tokens/month at agentic cache mix) might spend $25–30 on DeepSeek’s API, making Go’s $10 superior; very light users (<$10 equivalent) are better off pure BYOK. **Kimi Code/Z.ai/Xiaomi/StepFun** can beat Go for single-model focus — see [13](./13-best-value-coding-plans.md).
- **Revealed preference (telemetry, week to Oct 25):** DeepSeek V4.1 Flash **119T** tokens (#1, +39%), **MiniMax M3.1 Flash 37T (#2, +92%)**, GLM-5.3-Flash 8.9T, Muse Spark 7.6T (−76%), MiMo-Flash 7.2T, Beam 5.3T. The market has already voted: **cheap near-frontier models win the bulk of agent traffic**.
- **Zen overflow** is the flexible pressure valve: keep **Extra Usage** enabled so Go gracefully degrades instead of blocking. Zen also carries the free DS/GLM twins and the paid Argon (50% off through Nov 30).
- **Go Plus verdict:** worth it if your usage concentrates on GLM-5.3 (8×), Argon (4× → $120), M3.1 Flash (4× → $80), Qwen3.8 Flash (3×), or the $15-tier rations (4×); poor for DeepSeek V4.1 Flash / MiMo / Muse (2×). **Go Teams ($20/member/mo)** gives every member their own limits, adds **+$5/mo on every model cap** (e.g. DeepSeek $100→$105, K3.1 Pro $15→$20), and starts with **Extra Usage ON**. For DeepSeek-heavy users, **Go + Zen balance > Go Plus**.

---

## 6. The single most important value conclusion

> **The ceiling and the value story both changed — and they changed together.**
>
> **Gemini 4 Argon (AA 50)** is now the intelligence ceiling on Go **and** the best top-end value (1,601 pts/$, 961 req/mo measured, ZDR, 50%-off through Nov 30) — **K3.1 Pro (AA 46)** is the ration (259 req/mo) for when 1M context or Max effort is what actually matters. The **cheap tier (27–29) is compressed into noise**: Step 5 / M3.1 Flash / Qwen3.8 Flash = 29, GLM-5.3-Flash / GPT 6 Luna = 28, MiMo-V2.6-Flash = 27 — pick those on capacity/price/speed/privacy, not on a 2-point AA delta. **Haiku 5.5 (AA 36) is the best cheap lab model** and the best subagent pick (11,934 pts/$ at ≤100K). The value podium is **Muse Spark 1.3 (44,404 pts/$ ⚠ trains) · MiMo-V2.6-Flash (23,145) · DeepSeek V4.1 Flash (17,368, 52,632 req/mo, 10×)** — the volume king unchanged in role, upgraded in evidence (measured provider-side, not frozen).
>
> The winning strategy is **portfolio routing v5**: bulk on **DeepSeek V4.1 Flash + its free twin**, paid quality on **M3.1 Flash**, free quality on **GLM-5.3-Flash Free**, explore/subagents on **MiMo-V2.6-Flash / Haiku 5.5**, planning and non-convergent work on **Argon (ZDR)**, the 1M-context/Max-effort 5% on **K3.1 Pro**, visual QA on **Qwen3.8 Max / Qwen4 Max**, and keep the $15 rations for the few tasks where their specific strengths matter. Escalate outside Go only for must-not-fail work.

---

**Next:** [06 — Free Models & Privacy](./06-free-models-and-privacy.md) · [07 — Recommended Config](./07-recommended-config.md)
