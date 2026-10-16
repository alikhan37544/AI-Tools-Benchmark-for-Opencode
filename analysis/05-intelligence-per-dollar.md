# 05 — Intelligence per Dollar: Value, Tiers & "Pay More for a Jump"

> **Snapshot: October 1, 2026, refreshed October 13 and October 16.** Intelligence = Artificial Analysis Intelligence Index **v4.3.2**. Costs are **your calibrated per-request cost** from `04-limits-and-burn-rate.md` (7.8k input / 1.1k output+reasoning / 146k cache read), not list prices per token. Oct 16: **Gemini 4 Argon Contributor added** (AA 53, ~728 req/mo, trains on data); **Step 5 Preview now paid** but still the best AA 44+ capacity per $; **free twins** (DS V4.1 Flash Free, GLM-5.3-Flash Free) and **Beam Free** added to the math; Grok 4.6 removed.
>
> 🆕 **Oct 16 — the new stuff:** **Argon is the new #1 by raw intelligence-per-dollar at the top end (643 pts/$, 15–25 heavy tasks/mo)**; the **free GLM-5.3-Flash (AA 42)** is the best free intelligence OpenCode has ever offered; tier structure rebuilt around the new free floor.

---

## 1. Why flat-plan math is different

On a $10 flat plan, the "price" of using a model isn't tokens — it's **how much of that model's monthly allowance each request consumes**. Your real currency is *requests at a given intelligence level*.

Three metrics matter:

1. **AA points per $ of limit spend** — `AA ÷ $/request`. How efficiently limit-dollars buy intelligence.
2. **Monthly request capacity** — `allowance ÷ $/request`. How much work you can do.
3. **Monthly cognitive throughput** — `AA × monthly capacity`. Intelligence-weighted volume: how much "smart work" the model's allowance can fund per month.

A model can win on one and lose badly on another (Grok 4.7 has high AA but 158 req/mo; MiMo-V2.5 has huge capacity but AA 25).

---

## 2. The master value table

| Model | AA | $/req | Req/month | AA points per $ | Monthly cognitive throughput | Grade |
|---|---|---|---|---|---|---|
| **Muse Spark 1.3 Contrib** | 48 | $0.0013 | 46,440 | **37,152** | **2.23M** | A+ (privacy caveat) |
| **GLM-5.3-Flash Free** | 42 | $0 (free) | ∞ | **∞** | **∞** | **A+ free (zero-retention)** |
| **DeepSeek V4.1 Flash Free** | 39 | $0 (free) | ∞ | **∞** | **∞** | **A+ free (zero-retention)** |
| **Beam Free** | 30 | $0 (free) | ∞ | **∞** | **∞** | A free (no training; 30-day retention) |
| MiMo-V2.6-Flash (~) | 38 | $0.0018 | 33,171 | ~21,111 | 1.26M | **A (cheapest smart volume)** |
| GPT 6 Luna | 38 | $0.0028 | 5,376 | 13,620 | 204k | A− (weak agentically) |
| Claude Haiku 5.5 | 43 (Max) | $0.0028 | 5,375 | 15,357 | 231k | **A- (Max; Med 34)** |
| **DeepSeek V4.1 Flash** | 39 | $0.0031 | 25,484 | 12,426 | 994k | **A+ sustainable** |
| **MiMo-V2.6-Pro** | 46 | $0.0049 | 3,074 | 9,428 | 141k | **A (best premium)** |
| GLM-5.3-Flash | 42 | $0.0061 | 9,836 | 6,885 | 413k | A (best quality/value) |
| GPT 5.6 Luna | 35–37 | $0.0058 | 2,586 | 6,379 | 96k | B |
| Hy3 | 34 | $0.0068 | 8,772 | 4,971 | 298k | B (old but cheap) |
| LongCat-2.0 | n/a (SWE Pro 59.5 🟡) | $0.0045 | 13,228 | — | — | B |
| Qwen3.8 Flash | 40 | $0.0040 | 7,457 | 10,000 | 298k | B+ (AA 40, thin cover) |
| **Step 5 Preview (paid 4×)** | 44 | $0.0254 | ~2,360 | 1,733 | 104k | **A− (best AA 44+ capacity)** |
| Space Bunny (paid) | — | $0.0062 | 4,831 | — | — | B (fast stealth) |
| MiniMax M3 | 29 | $0.0124 | 4,831 | 2,335 | 140k | C |
| Qwen3.7 Plus | 25 | $0.0107 | 5,597 | 2,332 | 140k | C |
| **Gemini 4 Argon Contrib (2×)** | 53 | $0.0824 | ~728 | **643** | 38.6k | **A for the top end (trains on data)** |
| **GLM-5.3** | 45 | $0.0537 | 279 | 838 | 12.6k | **B+ ration** |
| **Qwen3.8 Max** | 45 | $0.0587 | 256 | 767 | 11.5k | **B+ ration** |
| **Kimi K3** | 44 | $0.0837 | 179 | 526 | 7.9k | **B+ ration** |
| Grok 4.7 | 46 | $0.0952 | 158 | 483 | 7.3k | B ration |
| Kimi K2.7 Code | 26 | $0.0395 | 1,517 | 657 | 39k | D (vendor-only) |

**Legacy / removed from Go (Zen or deprecated; avoid for new work):** Grok 4.6 (AA 44, 158 req/mo — Zen $2/$6), DeepSeek V4 Flash (AA ~34, 9,448), DeepSeek V4 Pro (AA 36, 1,017), GLM-5.2 (AA 34, 1,117), MiMo-V2.5 (AA 25, 33,171), MiMo-V2.5-Pro (AA 26, 3,074), Kimi K2.6 (—, 1,706), MiniMax M2.7 (AA 23). Full numbers in the legacy table in `04-limits-and-burn-rate.md`.

*(Other unmeasured: LongCat 2.5, Hy4 — see tier table. Haiku score is Max-effort; default medium is AA 34.)*

### The four winners (updated)

1. **Most intelligence per limit-dollar — Muse Spark 1.3 Contributor** (37,152 points/$; 2.23M monthly throughput) — still the mathematical winner, with the Contributor data policy caveat.
2. **Best free intelligence — GLM-5.3-Flash Free** (AA 42, zero-retention, $0/req) with **DeepSeek V4.1 Flash Free** (AA 39, zero-retention) as the high-capacity twin. These are the strongest free models OpenCode has offered; Beam Free (AA 30) covers the no-training case.
3. **Best sustainable intelligence per dollar — DeepSeek V4.1 Flash.** 25.5k requests/month, 12.4k points/$, 209–232 tok/s, native vision — and if you accept the free twin's window, the cost is literally $0.
4. **Highest raw intelligence — Gemini 4 Argon Contributor (AA 53)**: ~728 req/mo at the $60 2× promo, 643 pts/$ — more hard-task capacity than any other AA 50+ model on any flat plan, for the price of training data on Google's side. Non-client only.

### AA "cost to run the entire Intelligence Index" (list-price basis, AA data)

| Model | Cost to run full index |
|---|---|
| GLM-5.3-Flash | **$280** |
| DeepSeek V4.1 Flash | ~$300 |
| MiMo-V2.6-Pro | ~$350 (at $0.13/task × ~2,700 tasks) |
| **Gemini 4 Argon** (Standard, at 50% off) | ~$700–900 |
| DeepSeek V4 Pro | $1,122 |
| GLM-5.3 | $2,503 |
| Kimi K3 | **$3,658** |

The premium models cost **9–13× more per unit of measured work** than the cheap tier — Argon at 50% off is the cheapest AA 53-class run ever measured.

---

## 3. Tier structure

### Tier 0 — Free (limited-time windows)
**GLM-5.3-Flash Free (AA 42, zero-retention) · DeepSeek V4.1 Flash Free (AA 39, zero-retention) · Beam Free (AA 30, no-training) · LongCat 2.5 Preview Free · Space Bunny Free (stealth) · LL Alpha Free (stealth, 30-day retention, may train).**
Unlimited, zero-allowance. The two zero-retention twins can carry real (non-critical) work — the best free floor this repo has seen. Stealths vary: **Big Pickle / LL Alpha / NVIDIA free train or log on data — never for client work.**

### Tier 1 — Workhorses (effectively unlimited at your pace)
**DeepSeek V4.1 Flash · MiMo-V2.6-Flash · GLM-5.3-Flash · Muse Spark 1.3 Contributor · LongCat-2.0 · Hy3 · Qwen3.8 Flash · Claude Haiku 5.5 · Space Bunny ($30) · Step 5 Preview ($60 4×).**
$30–80 allowances ($15 for Haiku 5.5), 2.4k–46k requests/month at your profile. This is where 90% of your work lives. Best quartet: **DeepSeek V4.1 Flash (general) + its free twin (bulk) + MiMo-V2.6-Flash (explore) + GLM-5.3-Flash (quality step-up / free twin)** — plus **Haiku 5.5 for subagents** and **Step 5 for paid AA 44 capacity**.

### Tier 2 — Premium rations ($15–60, high quality-per-call)
**MiMo-V2.6-Pro (AA 46) · Gemini 4 Argon Contributor (AA 53, trains) · GPT 6 Luna (AA 38) · GPT 5.6 Luna · Hy4 preview.**
1k–5k requests/month (Argon ~730 at your profile but the best per-task quality). Use for planning, hard debugging, design review, OCR verification. Argon is the standout for hard work; MiMo-V2.6-Pro for privacy-safe reasoning.

### Tier 3 — Frontier rations ($15, ~150–280 requests/month)
**Grok 4.7 (AA 46) · Kimi K3 (AA 44) · GLM-5.3 (AA 45) · Qwen3.8 Max (AA 45).** (Grok 4.6 removed from Go — Zen only.)
~1–3 substantial tasks per week each. Reserve for what cheap models fail at: multi-hour refactors, hard architecture, marathon debugging, visual QA on OSWorld-class tasks.

### Tier 4 — Beyond Go (the real frontier)
**Claude Opus 5.5 (AA 58) · GPT-6 Astra / Fable 5.1 (AA 53) · Muse Wonder Full (AA 56) / Muse Wonder (52) · GPT-6.1 Sol (AA 52).**
Not on Go (Argon's Contributor SKU now brings 53-level intelligence *onto* Go — with training-data strings attached). Available via **GitHub Copilot** or Zen pay-as-you-go. Watch **Muse Wonder** (Meta, Oct 12 — AA 52/56, current Zen/Copilot-territory candidate) for the next escalation-slot change.

---

## 4. "Pay a little more, maybe run out of limits, but get a huge jump"

Each row is a switch from **DeepSeek V4.1 Flash** (your baseline) to another model:

| Switch to | ΔAA | Cost/req | Capacity change | When the jump is worth it |
|---|---|---|---|---|
| **DeepSeek V4.1 Flash Free / GLM-5.3-Flash Free** | **+0 / +3** | **×0 (free!)** | 25.5k → **∞** | Always, for non-critical work — zero-retention twins of the workhorse tier. |
| **Muse Spark 1.3 Contrib** | **+9** | **×0.42 (cheaper!)** | 25.5k → 46.4k (**+82%**) | Always — if the data policy is acceptable. |
| **MiMo-V2.6-Pro** | **+7** | ×1.6 | 25.5k → 3.1k (−88%) | Any task where first-try success matters; still only $0.005/req. |
| GLM-5.3-Flash | +3 | ×2.0 | 25.5k → 9.8k (−62%) | Frontend/docs/automation quality step-up; free twin if data is open. |
| GPT 6 Luna | −1 | ×0.9 | 25.5k → 5.4k | Only for quick non-agentic Q&A/cheap bulk; agentically weaker. |
| Claude Haiku 5.5 | +4 (Max) | ×0.9 | 25.5k → 5.4k | Subagents, quick edits, compactions — Sonnet-class coding in Copilot tests. |
| **Step 5 Preview (paid 4×)** | **+5** | ×8 | 25.5k → **~2,360** (−91%) | Best capacity at AA 44+; open weights = self-host option. |
| **Gemini 4 Argon Contrib** | **+14** | ×27 | 25.5k → **~730** (−97%) | The ceiling for hard/non-convergent tasks — if training-data terms are OK. **Biggest AA jump ever available on Go.** |
| **GLM-5.3** | **+6** | ×17 | 25.5k → **279** (−98.9%) | Hard terminal/standardized-harness tasks, security work, deep refactors. |
| **Qwen3.8 Max** | **+6** | ×19 | 25.5k → **256** (−99.0%) | Visual QA (OSWorld #1), screenshot/vision verification, best WebDev Arena Go model. |
| **Kimi K3** | **+5** | ×27 | 25.5k → **179** (−99.3%) | Multi-hour marathons, 1M-context legacy code, frontend, honest debugging. |
| **Grok 4.7** | **+7** | ×31 | 25.5k → **158** | Deep reasoning specialist; privacy-safe Grok since 4.6 left Go. |
| **Claude Opus 5.5** (not Go) | **+19** | ~×100–300 | ~50–150 req/mo via Copilot | Genuinely impossible tasks; must-not-fail deliverables. |

### How to think about "huge jump" economics

- **Retry math:** if DeepSeek V4.1 Flash needs 3 attempts where Opus 5.5 needs 1, DeepSeek still costs **~100–300× less**. So for *convergent* tasks (bugs you can reproduce, code you can test), cheap-model retries beat premium every time.
- **Premium is worth it when:** failure is expensive (production deploy, security, data migration), the task is **non-convergent** (one-shot long-horizon planning, ambiguous architecture), or cheap models demonstrably loop (Kimi K3/Grok are for exactly these cases). Argon at AA 53 is the new "non-convergent" workhorse — capacity allows ~15–25 heavy tasks/month, far more than the old $15 rations.
- **The rational portfolio (Oct 16):** ~55% DeepSeek V4.1 Flash (+free twin for bulk) + ~20% free GLM-5.3-Flash + ~10% MiMo-Flash/Haiku 5.5 + ~10% Step 5/MiMo-Pro (paid quality) + ~4% Argon (hard, non-client) + ~1% rations (Kimi K3/Grok 4.7/Qwen3.8 Max) + <1% Opus-class. This uses every model's independent allowance and rarely hits any single cap.

---

## 5. Value vs the outside world (Go vs BYOK)

- **The 8× multiplier is the core Go deal:** $10 buys up to $80 of usage at list rates (some models $15–30). At Go's rates, DeepSeek V4.1 Flash off-peak equals DeepSeek's own off-peak price.
- **Go vs direct API:** a light user (100M tokens/month at agentic cache mix) might spend $25–30 on DeepSeek's API, making Go's $10 superior; very light users (<$10 equivalent) are better off pure BYOK.
- **OpenRouter revealed preference (30 days to Sep 27):** #1 DeepSeek V4.1 Flash 19.6T tokens, #2 GLM 5.3 Flash 16.3T, #3 Space Bunny Alpha 13.9T, #4 Hy4 preview 9.64T, #5 GPT-5.6 Luna 8.53T. Coding category: GLM-5.3-Flash 17.7%, DeepSeek V4.1 Flash 14.4%. The market has already voted: **cheap near-frontier models win the bulk of agent traffic.**
- **Zen overflow** is the flexible pressure valve: keep `Use balance` enabled so Go gracefully degrades instead of blocking. Zen now also carries free DS/GLM twins and the paid Standard Argon (50% off through Nov 30).
- **Go Plus verdict:** worth it if your usage concentrates on GLM-5.3 (8×), Argon (4×), or the $15-tier rations (4×); poor for DeepSeek V4.1 Flash/MiMo/Muse (2×). For DeepSeek-heavy users, **Go + Zen balance > Go Plus**.

---

## 6. The single most important value conclusion

> **There is no one "most intelligent model" worth running for everything on Go.** The raw intelligence ceiling moved up a whole tier (Argon, AA 53), the capacity of that ceiling at ~730 req/mo is usable rather than symbolic, and the free floor regenerated stronger than ever (AA 42 zero-retention GLM + AA 39 DeepSeek). Meanwhile the old premium rations (Kimi K3/Grok/Qwen Max at 158–279 req/mo) were passed on both axes by cheaper and freer options.
>
> The winning strategy is **portfolio routing v3**: bulk on **DeepSeek V4.1 Flash + its free twin**, free quality on **GLM-5.3-Flash Free**, explore on MiMo-Flash/Haiku 5.5, paid hard-work capacity on **Step 5 Preview** and **Gemini 4 Argon** (the former for volume at AA 44, the latter for ceiling at AA 53 — both data-policy-gated differently), and keep the $15 rations for the few tasks where their specific strengths (marathon, visual QA, security) matter. Escalate outside Go only for must-not-fail work.

---

**Next:** [06 — Free Models & Privacy](./06-free-models-and-privacy.md) · [07 — Recommended Config](./07-recommended-config.md)
