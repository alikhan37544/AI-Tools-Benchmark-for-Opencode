# Research Guide — How This Was Built & How to Update It

> Methodology for the October 1, 2026 refresh. Use this to re-run the analysis in ~5 minutes of agent time (plus web access).

---

## 1. Research architecture

This analysis used **8 parallel research agents** plus direct document fetches and a local data-calibration pass:

| Agent | Scope |
|---|---|
| 1. Go ground truth | Plans, roster, limit mechanics, free/stealth models, changelog Aug→Oct, opencode.ai/data |
| 2. OpenAI GPT Luna | GPT 6 / 5.6 Luna: AA, vendor, Vals, LMArena, ARC, community, weaknesses |
| 3. Grok / GLM / MiniMax | Per-model specs, benchmarks, community sentiment |
| 4. DeepSeek / Qwen | V4.1/V4 Pro/V4 Flash + Qwen3.8 Max/Flash |
| 5. Kimi / MiMo / LongCat / Hyuan / Muse / stealth | Including HuggingFace download/like metrics |
| 6. Task-specific best models | 18 task categories with benchmark evidence |
| 7. Value & community | AA cost-to-intelligence, OpenRouter rankings, burn-rate anecdotes, tokenomics |
| 8. Independent evaluators | LMArena, AA, SWE-bench, Terminal-Bench, Aider, LiveCodeBench, METR, Epoch, OpenHands, ARC, Vals, HuggingFace |

Each agent was instructed to: search multiple queries, fetch authoritative URLs directly, never invent numbers, attach a source URL to every figure, distinguish vendor vs independent measurements, and list uncertainties/gaps.

### Why multiple agents

- Different search backends surface different leaderboards and regional sources.
- Cross-agent contradictions expose unreliable numbers (e.g. DeepSeek V4 Pro ranged 36–44 on "AA" across agents; direct fetch confirmed **36** on v4.3.2).
- Per-vendor agents can go deep on model cards and vendor benchmark tables, while the evaluator agent covers cross-vendor boards.

### Local calibration (the secret sauce)

For limits and value math, aggregate token/cost statistics were computed from the local OpenCode session database:

```bash
sqlite3 -readonly ~/.local/share/opencode/opencode.db \
  "SELECT json_extract(model,'\$.id'), COUNT(*), SUM(tokens_input), SUM(tokens_output),
          SUM(tokens_reasoning), SUM(tokens_cache_read), SUM(cost)
   FROM session GROUP BY 1 ORDER BY COUNT(*) DESC;"
```

Then message-level `tokens`/`cost` fields were aggregated to compute the user's true per-request profile (7.8k input / 1.1k output+reasoning / 146k cache read), peak burst rates (630 req/h), and rolling 5h/7d/30d spend. Only aggregates are used; no session content, titles, or client data.

---

## 2. Source hierarchy

1. **Vendor docs & model cards** (opencode.ai, HF cards, provider docs) — facts about pricing, context, modalities.
2. **Artificial Analysis v4.3.2** — the cross-vendor intelligence scale; always cite the version.
3. **Independent harnesses** — Vals AI, LMArena, Terminal-Bench, SWE-bench mirrors, OpenHands Index, ARC Prize, METR, Epoch AI.
4. **Vendor benchmark tables** — useful but self-selected; label 🟡/🔴.
5. **Community** — Reddit r/opencode + r/opencodeCLI, Hacker News, X, blogs. Good for burn rates and reliability, bad for precise scores.
6. **Aggregators** — OpenRouter rankings (revealed preference), opencode.ai/data (whole-user telemetry), theopenweights.com.

---

## 3. Key URLs used

| Purpose | URL |
|---|---|
| Go plans/limits/roster | https://opencode.ai/docs/go/ · https://opencode.ai/v2/docs/console/go |
| Zen pricing/models | https://opencode.ai/docs/zen/ |
| Whole-user telemetry | https://opencode.ai/data |
| Changelog | https://opencode.ai/changelog |
| Model list JSON | https://opencode.ai/zen/v1/models |
| Intelligence index | https://artificialanalysis.ai/leaderboards/models |
| Coding agents | https://artificialanalysis.ai/agents/coding-agents |
| LMArena | https://lmarena.ai/leaderboard |
| Terminal-Bench | https://www.tbench.ai/ · https://terminal-bench.com |
| SWE-bench | https://www.swebench.com/ |
| Aider (frozen) | https://aider.chat/docs/leaderboards/ |
| OpenHands Index | https://openhands.dev/ |
| METR | https://metr.org/time-horizons/ |
| Epoch AI | https://epoch.ai/benchmarks |
| ARC Prize | https://arcprize.org/ |
| Vals AI | https://www.vals.ai/ |
| Design/WebDev Arena | https://www.designarena.ai/ · https://lmarena.ai/leaderboard/code |
| OpenRouter rankings | https://openrouter.ai/rankings |
| DeepSeek pricing/updates | https://api-docs.deepseek.com/quick_start/pricing · /updates |

---

## 4. Update procedure (quarterly, or on any roster change)

1. **Fetch Go docs** and diff the roster/limits against `analysis/01`. Record additions/removals, cap changes, free-model windows.
2. **Re-fetch AA pages** for every Go model; capture Intelligence Index **with version**, speed, TTFT, $/task. Update `analysis/02` master table.
3. **Check independent boards** (LMArena, Vals, Terminal-Bench, OSWorld) for new Go-model entries.
4. **Recalibrate your profile** with the SQL above (or the burn script pattern in `analysis/04`): recompute cost/request, rolling-window peaks, and capacity per model at Go prices.
5. **Re-run the value math** (`AA ÷ $/req`; `AA × req/mo`) and update tiers and jump analysis in `analysis/05`.
6. **Update the HTML** — the file was generated by a script; simplest path is to ask an agent to regenerate `opencode-go-analysis.html` from the updated markdown (data tables at the top of the generator).
7. **Verify privacy policies** — especially DeepSeek ZDR renewals, Muse Spark Contributor terms, and any new stealth/free models.
8. **Commit** with a dated message.

### Fast prompts for a future agent

- *"Fetch https://opencode.ai/docs/go/ and diff the model roster, monthly limits and estimated requests against analysis/01-go-roster-and-limits.md; update the file and list changes."*
- *"For each model in the Go roster, fetch its Artificial Analysis model page and record Intelligence Index vX.Y.Z, output speed, TTFT and $/task; update analysis/02-benchmarks.md."*
- *"Recompute my token profile from ~/.local/share/opencode/opencode.db (read-only) and refresh analysis/04-limits-and-burn-rate.md capacity tables."*
- *"Check the oh-my-openagent releases + opencode.ai/v2/docs/migrate-v1 for OMO-on-v2 support status; update the compatibility matrix in analysis/08 and analysis/09."*
- *"Re-scrape the opencode ecosystem page + awesome-opencode for new plugins/MCPs; update analysis/10."*

## 6. Second-wave topics (Oct 1, 2026) and their refresh triggers

| File | Refresh trigger |
|---|---|
| `08-oh-my-opencode.md` | OMO releases (esp. official v2 support), category renames, fallback-chain changes (`doctor --verbose` is ground truth) |
| `09-opencode-v1-vs-v2.md` | v2 releases (LSP/share restoration, history migrator fixes, plugin API freeze), v1 EOL announcement |
| `10-plugins-and-stacks.md` | New ecosystem entries, MCP deprecations, v2 ports of v1 plugins |
| `11-amazing-additions.md` | Any change in your stack (new Azure services, new RPA targets, new repos) — re-run the 80/20 ranking |

---

## 5. Rules of thumb learned in this cycle

1. **Never quote an AA score without its index version.** v4.1.1 scores are ~15–20 points higher than v4.3.2 for the same models.
2. **Terminal-Bench version + harness matters more than the model.** TB2.1 vendor vs Vals can differ by 20 points.
3. **Vendor benchmarks are marketing** until an independent run exists; mark them.
4. **The docs' estimated requests assume light traffic.** Heavy agentic users divide by 3–7×.
5. **Cache-read pricing dominates real agent costs.** A model with 10× cheaper cache can be cheaper in practice than a model with half the output price.
6. **Reasoning effort is the biggest cost lever** (3.6–6.5× on Kimi K3).
7. **Free/stealth models are the highest-variance choice** — great value, unknown identity/policies; keep them off critical and sensitive work.
8. **Roster churn is weekly.** Any analysis older than a month is stale; this repo should be re-run at least quarterly.
