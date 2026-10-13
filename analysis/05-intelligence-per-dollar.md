# 05 — Intelligence per Dollar: Value, Tiers & "Pay More for a Jump"

> **Snapshot: October 1, 2026, refreshed October 13.** Intelligence = Artificial Analysis Intelligence Index **v4.3.2**. Costs are **your calibrated per-request cost** from `04-limits-and-burn-rate.md` (7.8k input / 1.1k output+reasoning / 146k cache read), not list prices per token. Oct 13: DeepSeek cap $80 (capacity ↑), Space Bunny now paid, +Step 5 Preview (free, AA 44) and +Claude Haiku 5.5; legacy retired/superseded models moved to a separate table.
>
> 🆕 **Oct 13 — the new stuff:** **Step 5 Preview Free** is winner #2 (AA 44 at $0 — infinite pts/$); jump table has new Step 5 + Haiku rows with the DeepSeek baseline at 25.5k; T0/T1 tiers rebuilt around the new free floor.

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
| **Step 5 Preview Free** | 44 | $0 (free) | ∞ | **∞** | **∞** | **A+ free (until it ends)** |
| **DeepSeek V4.1 Flash** | 39 | $0.0031 | 25,484 | 12,426 | 994k | **A+ sustainable** |
| MiMo-V2.6-Flash | ~37–42? | $0.0018 | 33,171 | ~21,000? | ~1.3M? | A (unmeasured) |
| GPT 6 Luna | 38 | $0.0028 | 5,376 | 13,620 | 204k | A− (weak agentically) |
| Claude Haiku 5.5 | — (too new) | $0.0028 | 5,375 | — | — | B+ (subagent star, unmeasured) |
| **MiMo-V2.6-Pro** | 46 | $0.0049 | 3,074 | 9,428 | 141k | **A (best premium)** |
| GLM-5.3-Flash | 42 | $0.0061 | 9,836 | 6,885 | 413k | A (best quality/value) |
| GPT 5.6 Luna | 35–37 | $0.0058 | 2,586 | 6,379 | 96k | B |
| Hy3 | 34 | $0.0068 | 8,772 | 4,971 | 298k | B (old but cheap) |
| LongCat-2.0 | n/a (SWE Pro 59.5 🟡) | $0.0045 | 13,228 | — | — | B |
| Qwen3.8 Flash | n/a (~40?) | $0.0040 | 7,457 | — | — | B+ (unproven) |
| Space Bunny (paid) | — | $0.0062 | 4,831 | — | — | B (fast stealth) |
| MiniMax M3 | 29 | $0.0124 | 4,831 | 2,335 | 140k | C |
| Qwen3.7 Plus | 25 | $0.0107 | 5,597 | 2,332 | 140k | C |
| MiniMax M2.7 | 23 | $0.0124 | 4,831 | 1,852 | 111k | C− (MLE niche) |
| **GLM-5.3** | 45 | $0.0537 | 279 | 838 | 12.6k | **B+ ration** |
| **Qwen3.8 Max** | 45 | $0.0587 | 256 | 767 | 11.5k | **B+ ration** |
| **Kimi K3** | 44 | $0.0837 | 179 | 526 | 7.9k | **B+ ration** |
| Grok 4.7 | 46 | $0.0952 | 158 | 483 | 7.3k | B ration |
| Grok 4.6 | 44 | $0.0952 | 158 | 462 | 7.0k | B ration |
| Kimi K2.7 Code | 26 | $0.0395 | 1,517 | 657 | 39k | D (vendor-only) |

**Legacy — retired upstream or superseded (still billed; avoid for new work):** DeepSeek V4 Flash (AA ~34, 9,448 req/mo) · DeepSeek V4 Pro (AA 36, 1,017) · GLM-5.2 (AA 34, 1,117) · MiMo-V2.5 (AA 25, 33,171) · MiMo-V2.5-Pro (AA 26, 3,074) · Kimi K2.6 (—, 1,706). Full per-model numbers in the legacy table in `04-limits-and-burn-rate.md`.

*(Other unmeasured: LongCat 2.5, Hy4, Claude Haiku 5.5 (no AA yet) — see tier table.)*

### The four winners

1. **Most intelligence per limit-dollar — Muse Spark 1.3 Contributor** (37,152 points/$; 2.23M monthly throughput). It is *both* the highest-AA model on Go and one of the cheapest per call. The catch is the contributor data policy: **your prompts train Meta models**.
2. **Best free intelligence — Step 5 Preview.** AA 44 (tied Kimi K3) at $0/request while the preview lasts. Infinite points/$. The single best arbitrage on Go right now — run bulk agentic work here first.
3. **Best sustainable intelligence per dollar — DeepSeek V4.1 Flash.** 25.5k requests/month (after the Oct 8 cap raise to $80), 12.4k points/$, 209–232 tok/s, native vision. This is why it's the crowd's #2 model by tokens and your daily driver. Its cap now comfortably covers your actual pace — which is the practical definition of "the right model."
4. **Best premium intelligence per dollar — MiMo-V2.6-Pro.** AA 46 (highest verified on Go), $0.13/AA-task (vs $2.00 for Kimi K3), MIT, omnimodal, 1M ctx. Only 3,074 req/month at your profile, but **at $0.0049/request you can run it ~10× more than Kimi K3 per month**.

### AA "cost to run the entire Intelligence Index" (list-price basis, AA data)

| Model | Cost to run full index |
|---|---|
| GLM-5.3-Flash | **$280** |
| DeepSeek V4.1 Flash | ~$300 |
| MiMo-V2.6-Pro | ~$350 (at $0.13/task × ~2,700 tasks) |
| DeepSeek V4 Pro | $1,122 |
| GLM-5.3 | $2,503 |
| Kimi K3 | **$3,658** |

The premium models cost **9–13× more per unit of measured work** than the cheap tier.

---

## 3. Tier structure

### Tier 0 — Free (until it ends)
**Step 5 Preview Free, LongCat 2.5 Preview Free, Zen free models.**
Unlimited, zero-allowance. Step 5 Preview is the best free coder on Go (AA 44, Kimi-class). LongCat 2.5's window already extended past its initial ~Oct 10 estimate. (Space Bunny converted to paid in early Oct — see Tier 1.) Identities of stealth models are unconfirmed and policies vary. **Use for non-sensitive, non-critical exploration.** Big Pickle/NVIDIA/MiMo free train on data — never for client work.

### Tier 1 — Workhorses (effectively unlimited at your pace)
**Muse Spark 1.3 Contributor · DeepSeek V4.1 Flash · MiMo-V2.6-Flash · LongCat-2.0 · GLM-5.3-Flash · Hy3 · Qwen3.8 Flash · Claude Haiku 5.5 · Space Bunny (now paid, $30).**
$60–80 allowances ($30 for Qwen3.8 Flash/Space Bunny, $15 for Haiku 5.5), 3k–46k requests/month at your profile. This is where 90% of your work should live. Best quartet: **DeepSeek V4.1 Flash (general) + MiMo-V2.6-Flash (explore/bulk) + GLM-5.3-Flash (quality step-up) + Muse Spark (if data policy allows)** — plus **Haiku 5.5 for subagents/quick tasks** and **Step 5 Free for bulk coding**.

### Tier 2 — Premium rations ($15–30, but high quality-per-call)
**MiMo-V2.6-Pro (AA 46) · GPT 6 Luna (AA 38) · GPT 5.6 Luna · Hy4 preview · Space Bunny ($30).**
1k–5k requests/month. Use for planning, hard debugging, design review, OCR verification. MiMo-V2.6-Pro is the standout. (Legacy rations removed: DeepSeek V4 Pro, DS V4 Flash Vision, MiMo-V2.5-Pro — retired/superseded.)

### Tier 3 — Frontier rations ($15, ~150–280 requests/month)
**Grok 4.6/4.7 (AA 44/46) · Kimi K3 (AA 44) · GLM-5.3 (AA 45) · Qwen3.8 Max (AA 45).**
~1–3 substantial tasks per week each. Reserve for what cheap models fail at: multi-hour refactors, hard architecture, marathon debugging, visual QA on OSWorld-class tasks, one-shot must-work code.

### Tier 4 — Beyond Go (the real frontier)
**Claude Opus 5.5 (AA 58) · GPT-6 Astra / Fable 5.1 / Gemini 4 Argon (AA 53) · GPT-6.1 Sol (AA 52).**
Not on Go. Available via your **GitHub Copilot** subscription (you already used Opus 5.5 and GPT-6 Astra) or Zen pay-as-you-go ($4–10 in / $20–50 out). 10–19 AA points above the best Go model — the difference between "usually works" and "works on the first try" for brutal tasks.

---

## 4. "Pay a little more, maybe run out of limits, but get a huge jump"

Each row is a switch from **DeepSeek V4.1 Flash** (your baseline) to another model:

| Switch to | ΔAA | Cost/req | Capacity change | When the jump is worth it |
|---|---|---|---|---|
| **Step 5 Preview Free** | **+5** | **×0 (free!)** | 25.5k → **∞** | Always, while the preview lasts — Kimi-class coding for zero limit spend. The best arbitrage on Go right now. |
| **Muse Spark 1.3 Contrib** | **+9** | **×0.42 (cheaper!)** | 25.5k → 46.4k (**+82%**) | Always — if the data policy is acceptable. |
| **MiMo-V2.6-Pro** | **+7** | ×1.6 | 25.5k → 3.1k (−88%) | Any task where first-try success matters; still only $0.005/req. |
| GLM-5.3-Flash | +3 | ×2.0 | 25.5k → 9.8k (−62%) | Frontend/docs/automation quality step-up while keeping thousands of requests. |
| GPT 6 Luna | −1 | ×0.9 | 25.5k → 5.4k | Only for quick non-agentic Q&A/cheap bulk; agentically weaker. |
| Claude Haiku 5.5 | unmeasured | ×0.9 | 25.5k → 5.4k | Subagents, quick edits, compactions — Sonnet-class coding in Copilot tests. |
| **GLM-5.3** | **+6** | ×17 | 25.5k → **279** (−98.9%) | Hard terminal/standardized-harness tasks, security work, deep refactors. |
| **Qwen3.8 Max** | **+6** | ×19 | 25.5k → **256** (−99.0%) | Visual QA (OSWorld #1), screenshot/vision verification, best WebDev Arena Go model. |
| **Kimi K3** | **+5** | ×27 | 25.5k → **179** (−99.3%) | Multi-hour marathons, 1M-context legacy code, frontend, honest debugging. |
| **Grok 4.6** | **+5** | ×31 | 25.5k → **158** (−99.4%) | Best verified agentic accuracy (SWE-bench 95.6), planning/architecture. |
| **Grok 4.7** | **+7** | ×31 | 25.5k → **158** | Deep reasoning specialist; skip unless you specifically need GPQA-class reasoning. |
| **Claude Opus 5.5** (not Go) | **+19** | ~×100–300 | ~50–150 req/mo via Copilot | Genuinely impossible tasks; must-not-fail deliverables. |

### How to think about "huge jump" economics

- **Retry math:** if DeepSeek V4.1 Flash needs 3 attempts where Opus 5.5 needs 1, DeepSeek still costs **~100–300× less**. So for *convergent* tasks (bugs you can reproduce, code you can test), cheap-model retries beat premium every time.
- **Premium is worth it when:** failure is expensive (production deploy, security, data migration), the task is **non-convergent** (one-shot long-horizon planning, ambiguous architecture), or cheap models demonstrably loop (Kimi K3/Grok are for exactly these cases).
- **The rational portfolio:** ~70% DeepSeek V4.1 Flash + ~15% Step 5 Preview Free (while it lasts) + ~10% GLM-5.3-Flash/MiMo-V2.6-Flash/Haiku 5.5 + ~2% rations (Kimi K3/Grok 4.6/Qwen3.8 Max) + ~1% Opus-class. This uses every model's independent allowance and rarely hits any single cap.

---

## 5. Value vs the outside world (Go vs BYOK)

- **The 8× multiplier is the core Go deal:** $10 buys up to $80 of usage at list rates (some models $15–30). At Go's rates, DeepSeek V4.1 Flash off-peak equals DeepSeek's own off-peak price.
- **Go vs direct API:** a light user (100M tokens/month at agentic cache mix) might spend $25–30 on DeepSeek's API, making Go's $10 superior; very light users (<$10 equivalent) are better off pure BYOK.
- **OpenRouter revealed preference (30 days to Sep 27):** #1 DeepSeek V4.1 Flash 19.6T tokens, #2 GLM 5.3 Flash 16.3T, #3 Space Bunny Alpha 13.9T, #4 Hy4 preview 9.64T, #5 GPT-5.6 Luna 8.53T. Coding category: GLM-5.3-Flash 17.7%, DeepSeek V4.1 Flash 14.4%. The market has already voted: **cheap near-frontier models win the bulk of agent traffic.**
- **Zen overflow** is the flexible pressure valve: keep `Use balance` enabled so Go gracefully degrades instead of blocking.
- **Go Plus verdict:** worth it only if your usage concentrates on GLM-5.3 (8×) or $15-tier rations including Haiku 5.5 (4×); poor for DeepSeek V4.1 Flash/MiMo/Muse (2×). For DeepSeek-heavy users, **Go + Zen balance > Go Plus**.

---

## 6. The single most important value conclusion

> **There is no one "most intelligent model" worth running for everything on Go.** The intelligence gap between the $80-allowance tier and the $15-allowance tier is ~5–7 AA points (39 vs 44–46), but the capacity gap is **90–160×** (25,500 vs 158–279 requests/month at your profile).
>
> The winning strategy is **portfolio routing**: sustain volume on DeepSeek V4.1 Flash + Step 5 Preview Free + MiMo-V2.6-Flash, buy quality-per-call with MiMo-V2.6-Pro, deploy Haiku 5.5 on subagents, and spend the ration models (Kimi K3, Grok 4.6, Qwen3.8 Max, GLM-5.3) on the handful of tasks per week where +5 AA actually changes the outcome. Escalate outside Go only for must-not-fail work.

---

**Next:** [06 — Free Models & Privacy](./06-free-models-and-privacy.md) · [07 — Recommended Config](./07-recommended-config.md)
