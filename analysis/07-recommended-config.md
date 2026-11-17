# 07 — Recommended OpenCode Configuration & Workflow

> **Snapshot: October 1, 2026; refreshed October 13, 16, 25 and November 17, 2026.** **Nov 17: AA v5.0.1 re-baseline applied** — all AA scores and capacities below are v5.0.1 / measured profile (heavy mix in parentheses) unless labeled (v4.3.2). **This machine now runs OpenCode v2.3.0** (v1 latest is **1.19.5**, Oct 28). The configs below use the portable fields (`model`, `small_model`, `agent`) that both v1 and v2 accept; on a fresh v2 install put them in `~/.config/opencode/opencode.jsonc`. Verify keys against [opencode.ai/docs/config](https://opencode.ai/docs/config/) and [docs/permissions](https://opencode.ai/docs/permissions/). Model IDs are the provider IDs confirmed by OpenCode docs and this machine’s `/models` (`opencode-go/*`, free models on `opencode/*`).
>
> 🆕 **Nov 17:** **Gemini 4 Argon (AA 50) is now both the AA ceiling and the default planning model** — ZDR/not trained, **961 req/mo** measured (728 heavy), 3× multiplier, 50%-off through Nov 30. **Kimi K3.1 Pro (AA 46, 259 req/mo measured / 269 heavy)** is now the hardest-5% escalation, not the default. **DeepSeek daily driver: 52,632 req/mo measured** (32,258 heavy; AA 33 — the catalog SKU is "DeepSeek V4.1 Flash 1017", so the 1017 checkpoint is the served product; base ckpt unmeasured/not served). **M3.1 Flash (AA 29, 5,760 req/mo measured / 4,975 heavy)** stays the paid value lane — but the cheap tier is compressed (27–29: M3.1 Flash/Step 5/Qwen3.8 Flash 29, GLM-5.3-Flash/GPT 6 Luna 28, MiMo-Flash 27), so capacity/price/speed decide, not AA. **Haiku 5.5 (AA 36)** = best cheap lab model (subagent pick). Frontier anchor: **Opus 5.5 = AA 59** (was 58).
> 🆕 **Oct 25 (kept as history — v4.3.2-era numbers):** `gemini-4-argon-contributor` → **`gemini-4-argon`** (Go now documents it **ZDR/not trained**, $30 50%-off cap). Add **`kimi-k3.1-pro`** (AA 55.1, v4.3.2; 269 req/mo heavy) and **`minimax-m3.1-flash`** (AA 43, v4.3.2; 4,975 req/mo heavy). `grok-4.6` is gone; `grok-4.7` is the Grok. Step 5 is paid ($15). **India:** pay Go with **UPI**; set **DeepSeek → Regions = Global**; enable Muse’s training opt-in only on non-client work.

---

## 1. Global config (personal machine, non-client)

`~/.config/opencode/opencode.jsonc` (v2) or `opencode.json` (v1) — the goal: cheap volume on the main agent, premium models only for planning/exploration where they pay off, and free twins as the floor.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",

  // Daily driver: proven at your volume (~52,632 req/mo measured / 32,258 heavy, $100 cap docs basis), native vision, 96% cache hit
  "model": "opencode-go/deepseek-v4.1-flash",

  // Cheap utility model for titles/summaries and tiny tasks
  "small_model": "opencode-go/mimo-v2.6-flash",

  "agent": {
    // Planning: Argon is now BOTH the AA ceiling (AA 50) and the independent agentic leader (Vals #1 Go),
    // ZDR, 961 req/mo measured. Swap to kimi-k3.1-pro (AA 46, 259 req/mo measured) only for 1M-ctx / Max-effort needs.
    "plan": { "model": "opencode-go/gemini-4-argon" },

    // Exploration/repo Q&A — fastest Claude; free alt: opencode/glm-5.3-flash-free
    "explore": { "model": "opencode-go/claude-haiku-5-5" },

    // Build loops — quality step-up when you want it, still ~52,632 req/mo measured (32,258 heavy)
    "build": { "model": "opencode-go/deepseek-v4.1-flash" },

    // Cheap paid quality lane: AA 29 at 5,760 req/mo measured (4,975 heavy) — cheap tier compressed (27–29), capacity/price decide
    "value": { "model": "opencode-go/minimax-m3.1-flash" }
  }
}
```

**Free-lane tip:** `opencode/deepseek-v4.1-flash-free` and `opencode/glm-5.3-flash-free` are zero-retention and cost nothing — pin them on a bulk agent or use them when a Go cap binds. `opencode/beam-free` is the no-training/30-day alternative; **Flint 40B Free may train — do not use it for client work.**

**Why not a premium driver?** At your calibration, the $15 rations give ~2–5 tasks/month (K3.1 Pro, 259 req/mo measured) or ~6–19 (Argon, 961 req/mo measured); DeepSeek V4.1 Flash gives ~52,632 requests/month (measured profile), and the free twins give unlimited non-critical capacity. Planning is where premium intelligence changes the *whole* trajectory of a task for a handful of requests — and **Argon (AA 50, 961 req/mo measured, ZDR)** now fills that slot as both the AA ceiling and the best top-end value, without the old training caveat. Keep **K3.1 Pro (AA 46)** as the escalation for the hardest 5%, not the default.

**India-specific settings:**
- **Billing:** Go/Plus checkout supports **UPI**, card, Link, Alipay and WeChat Pay. Top-ups add 4.6% + $0.31.
- **DeepSeek:** in the Go model settings, set **Regions = Global** — the default allowed regions are Europe & United States, so DeepSeek can look “blocked” until you change it.
- **Muse Spark:** enable **“Allow paid endpoints that train on request data”** only on non-client projects. Leave it off everywhere else.

---

## 2. Client / PHI-safe config (per project)

Put this in the client repo’s `opencode.json` (project config overrides global). Key points: no Contributor/free/training routes, no OpenAI models for the contract that bans them, and tighter permissions.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "model": "opencode-go/glm-5.3-flash",
  "small_model": "opencode-go/glm-5.3-flash",
  "agent": {
    "plan":  { "model": "opencode-go/mimo-v2.6-pro" },
    "build": { "model": "opencode-go/glm-5.3-flash" }
  },
  "permission": {
    "edit": "allow",
    "bash": {
      "*": "ask",
      "git status*": "allow",
      "git diff*": "allow",
      "git log*": "allow",
      "ls *": "allow",
      "cat *": "allow",
      "pytest*": "allow",
      "python -m pytest*": "allow",
      "npm test*": "allow",
      "az account show*": "allow",
      "docker ps*": "allow"
    }
  }
}
```

> ⚠️ Per your own project rule: **never start servers autonomously**. Keep `npm run dev`, `uvicorn`, `docker compose up`, etc. behind `ask`. Your GEMINI.md says “always run builds and fix build errors autonomously” — keep build/test allowed, but gated from long-running processes.

**If you want Argon in the client config:** `gemini-4-argon` is now documented **ZDR/not trained**, so it is no longer disqualified on data-policy grounds. Still confirm with the client and keep it out of `small_model`; the safest default remains GLM/MiMo paid.

---

## 3. Role-based model matrix (copy/paste reference)

| Role | Model | Effort/variant | Rationale |
|---|---|---|---|
| Daily build | `deepseek-v4.1-flash` | medium/high for routine, **max** for hard | best capacity + 177.3 tok/s + vision; AA 33 on v5.0.1 — catalog SKU "DeepSeek V4.1 Flash 1017" = the served product |
| Free workhorse loop | `deepseek-v4.1-flash-free` / `glm-5.3-flash-free` | high | zero-retention, $0; keeps working after Go caps |
| Explore subagent | `claude-haiku-5-5` (alt: `mimo-v2.6-flash`) | medium/default | fastest Claude (AA 36 — best cheap lab model), Sonnet-class coding, 1M ctx |
| Bulk edits/tests | `minimax-m3.1-flash` / `glm-5.3-flash` | default | M3.1 Flash AA 29, 5,760 req/mo measured (4,975 heavy); GLM-Flash 10,196 req/mo measured |
| Plan/architecture | `gemini-4-argon` (ZDR) **or** `kimi-k3.1-pro` | high | Argon AA 50 / Vals #1 Go / 961 req/mo measured; K3.1 Pro AA 46 / 259 req/mo measured (escalation) |
| Hard debug | `kimi-k3.1-pro` | max | honesty lineage, 1M ctx, AA 46 |
| Frontend review | `muse-spark-1.3-contributor` (non-client) or `kimi-k3.1-pro` | default | Design Arena #1 / K3 #3; K3.1 Pro likely K3-class |
| Visual QA verification | `qwen3.8-max` | default | OSWorld 86.1 (#1 overall); 229 req/mo measured (256 heavy) |
| OCR/docs | `deepseek-v4.1-flash` / `qwen3.8-flash` | default | cheap native vision |
| Data/ML scripts | `deepseek-v4.1-flash` or `minimax-m3.1-flash` | max | Python + tests |
| Security review | `glm-5.3` | max | CyberGym 84.5 |
| Paid quality capacity | `step-5-preview` | high | AA 29 with 677 req/mo measured (591 heavy) at the $15 cap |
| Marathon refactor | `kimi-k3.1-pro` → Copilot `claude-opus-5.5` | max | only when it must succeed |
| General research | `gemini-4-argon` / `kimi-k3.1-pro` / `muse-spark-1.3-contributor` / `grok-4.7` | default | AA 50 / 46 / 37 / 35 |
| Frontier escalation | Copilot `claude-opus-5.5` / Zen `claude-opus-5-5` | max | AA 59 |

---

## 4. Workflow patterns that save limits

1. **Plan once with a premium model, execute with a cheap one.**
   `Plan` agent on Argon (ZDR, 961 req/mo measured) or K3.1 Pro → save the plan → `Build` on DeepSeek V4.1 Flash. A 5-request plan can save 50 wasted cheap requests.
2. **Use effort levels deliberately.** Max effort costs 3.6–6.5× more output tokens than low/medium. Reserve `max` for planning, security, and hard debugging.
3. **Delegate exploration to a subagent on Haiku 5.5 / MiMo-V2.6-Flash.** Repo scans are token-heavy and low-intelligence — perfect for cheap models.
4. **Use the free twins for anything non-critical.** `opencode/deepseek-v4.1-flash-free` / `glm-5.3-flash-free` are zero-retention and $0 — the default bulk lane.
5. **Use M3.1 Flash as the paid value lane.** AA 29 at 5,760 req/mo measured (4,975 heavy) and $0.00347/req — the cheapest “good” model on Go. The cheap tier is compressed (27–29), so capacity/price/speed — not AA — decide between it, Step 5, Qwen3.8 Flash, GLM-5.3-Flash, GPT 6 Luna and MiMo-Flash.
6. **Batch independent work off-peak (DeepSeek).** Long autonomous runs after ~15:30 IST and on weekends are half price, which literally doubles your cap.
7. **Install Playwright-MCP or use browser tools for visual QA**, run the loop on Qwen3.8 Flash, and do the final pass on Qwen3.8 Max / K3.1 Pro.
8. **Keep Extra Usage ON** in the Go console so you degrade to Zen credits instead of getting blocked; free models remain the final floor.
9. **One premium review per difficult PR** (K3.1 Pro or Argon) catches the class of errors cheap models ship.
10. **Do not let agents run `git push`, deploys, or infra mutations without approval** — keep them in the `ask` permission list. Use separate `plan` and `build` passes for anything touching production.

---

## 5. Monthly operating plan (suggested)

| Budget | Plan |
|---|---|
| $10/mo | Go + project routing above + off-peak shift. Expect (measured profile): ~52,632 DeepSeek requests + unlimited free-twin bulk + ~5,760 M3.1 Flash + ~961 Argon + ~259 K3.1 Pro + ~229 Qwen3.8 Max requests/month — hundreds of DeepSeek sessions, daily Argon plans/reviews, and ~5 hard-ration K3.1 Pro tasks. |
| $28–30/mo | Go + **Z.ai Lite $18** if GLM is >50% of your work, **or** Go + **Kimi Code Plus $19** if K3.1 Pro is. Keep Go for the other 28 models. |
| $40/mo | Go Plus **only if** you concentrate on GLM-5.3 (8×), Argon (4× → $120), M3.1 Flash (4× → $80), or the $15 rations; otherwise Go + $30 Zen overflow is more flexible. |
| Flex | Add Zen balance (auto-reload $20) for overflow; Zen Gemini 4 Argon is 50% off through Nov 30; use Copilot for Opus 5.5/Astra on the rare must-not-fail task. |

**Expected outcome:** you should almost never hit the 5-hour wall on the workhorse tier, hit the weekly wall only in exceptional crunch weeks, and always have a ration model available for the hard 5% — with the free twins absorbing anything that would otherwise bind.

---

**Back to:** [README](../README.md) · [01 Roster](./01-go-roster-and-limits.md) · [02 Benchmarks](./02-benchmarks.md) · [03 Playbook](./03-task-playbook.md) · [04 Limits](./04-limits-and-burn-rate.md) · [05 Value](./05-intelligence-per-dollar.md) · [06 Privacy](./06-free-models-and-privacy.md) · [12 Go vs Direct](./12-opencode-vs-direct.md) · [13 Best-Value Plans](./13-best-value-coding-plans.md) · [14 India](./14-india-availability.md)
