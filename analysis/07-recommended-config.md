# 07 — Recommended OpenCode Configuration & Workflow

> **Snapshot: October 1, 2026.** Verify config keys against [opencode.ai/docs/config](https://opencode.ai/docs/config/) and [docs/permissions](https://opencode.ai/docs/permissions/) — OpenCode v2 shipped recently and keys can change. Model IDs below are the Go provider IDs confirmed by OpenCode docs and your own session DB (`providerID: opencode-go`).

---

## 1. Global config (personal machine, non-client)

`~/.config/opencode/opencode.json` — the goal: cheap volume on the main agent, premium models only for planning/exploration where they pay off.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",

  // Daily driver: proven at your volume (19k req/mo), native vision, 96% cache hit
  "model": "opencode-go/deepseek-v4.1-flash",

  // Cheap utility model for titles/summaries and tiny tasks
  "small_model": "opencode-go/mimo-v2.6-flash",

  "agent": {
    // Planning only — best independent reasoning on Go (GPQA 95.0, ARC-AGI-2 67.1)
    "plan": { "model": "opencode-go/grok-4.6" },

    // Exploration/repo Q&A — 33k req/mo of capacity at your token profile
    "explore": { "model": "opencode-go/mimo-v2.6-flash" },

    // Build loops — quality step-up when you want it, still 9.8k req/mo
    "build": { "model": "opencode-go/deepseek-v4.1-flash" }
  }
}
```

**Why not a premium driver?** At your calibration, Kimi K3/Grok 4.6 give ~3 tâches/week; DeepSeek V4.1 Flash gives ~380 sessions/month. Planning is where premium intelligence changes the *whole* trajectory of a task for a handful of requests.

---

## 2. Client / PHI-safe config (per project)

Put this in the client repo's `opencode.json` (project config overrides global). Key points: no contributor/free/training routes, no OpenAI models for the contract that bans them, and tighter permissions.

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

> ⚠️ Per your own project rule: **never start servers autonomously**. Keep `npm run dev`, `uvicorn`, `docker compose up`, etc. behind `ask`. Your GEMINI.md says "always run builds and fix build errors autonomously" — keep build/test allowed, but gated from long-running processes.

---

## 3. Role-based model matrix (copy/paste reference)

| Role | Model | Effort/variant | Rationale |
|---|---|---|---|
| Daily build | `deepseek-v4.1-flash` | medium/high for routine, **max** for hard | best capacity + 209 tok/s + vision |
| Explore subagent | `mimo-v2.6-flash` | default | 33k req/mo, $0.0018/req |
| Bulk edits/tests | `glm-5.3-flash` | default | AA AutomationBench 60.4, 9.8k req/mo |
| Plan/architecture | `grok-4.6` **or** `mimo-v2.6-pro` | high | GPQA 95 / AA 46 |
| Hard debug | `kimi-k3` | max | honesty battery 0/12, SWE-Marathon 42 |
| Frontend review | `muse-spark-1.3-contributor` (non-client) or `kimi-k3` | default | Design Arena #1 / #3 |
| Visual QA verification | `qwen3.8-max` | default | OSWorld 86.1 (#1 overall) |
| OCR/docs | `deepseek-v4-flash-vision-exp` / `qwen3.8-flash` | default | cheap native vision |
| Data/ML scripts | `deepseek-v4.1-flash` or `kimi-k3` | max | Python + tests |
| Security review | `glm-5.3` | max | CyberGym 84.5 |
| Marathon refactor | `kimi-k3` → Copilot `claude-opus-5.5` | max | only when it must succeed |
| General research | `muse-spark-1.3-contributor` or `grok-4.7` | default | AA 48 / 46 |
| Frontier escalation | Copilot `claude-opus-5.5` / Zen `claude-opus-5-5` | max | AA 58 |

---

## 4. Workflow patterns that save limits

1. **Plan once with a premium model, execute with a cheap one.**
   `Plan` agent on Grok 4.6 → save the plan → `Build` on DeepSeek V4.1 Flash. A 5-request plan can save 50 wasted cheap requests.
2. **Use effort levels deliberately.** Max effort costs 3.6–6.5× more output tokens than low/medium. Reserve `max` for planning, security, and hard debugging.
3. **Delegate exploration to a subagent on MiMo-V2.6-Flash.** Repo scans are token-heavy and low-intelligence — perfect for the 33k/mo model. Your history already shows heavy `explore` usage (192 sessions).
4. **Batch independent work off-peak (DeepSeek).** Long autonomous runs after ~15:30 IST and on weekends are half price, which literally doubles your cap.
5. **Install Playwright-MCP or use browser tools for visual QA**, run the loop on Qwen3.8 Flash, and do the final pass on Qwen3.8 Max / Kimi K3.
6. **Keep `Use balance` ON** in the Go console so you degrade to Zen credits instead of getting blocked; free models remain the final floor.
7. **One premium review per difficult PR** (Kimi K3 or Grok 4.6) catches the class of errors cheap models ship.
8. **Do not let agents run `git push`, deploys, or infra mutations without approval** — keep them in the `ask` permission list. Use separate `plan` and `build` passes for anything touching production.

---

## 5. Monthly operating plan (suggested)

| Budget | Plan |
|---|---|
| $10/mo | Go + project routing above + off-peak shift. Expect: ~380 DeepSeek sessions + ~200 GLM-Flash/MiMo sessions + ~4 Kimi K3 tasks + ~5 Qwen3.8 Max verification runs. |
| $40/mo | Go Plus **only if** you concentrate on GLM-5.3 (8×) or the $15 rations; otherwise Go + $30 Zen overflow is more flexible. |
| Flex | Add Zen balance (auto-reload $20) for overflow; use Copilot for Opus 5.5/Astra on the rare must-not-fail task. |

**Expected outcome:** you should almost never hit the 5-hour wall on the workhorse tier, hit the weekly wall only in exceptional crunch weeks, and always have a ration model available for the hard 5%.

---

**Back to:** [README](../README.md) · [01 Roster](./01-go-roster-and-limits.md) · [02 Benchmarks](./02-benchmarks.md) · [03 Playbook](./03-task-playbook.md) · [04 Limits](./04-limits-and-burn-rate.md) · [05 Value](./05-intelligence-per-dollar.md) · [06 Privacy](./06-free-models-and-privacy.md)
