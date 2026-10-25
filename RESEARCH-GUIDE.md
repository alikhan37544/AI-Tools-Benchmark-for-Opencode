# Research Guide — How This Was Built & How to Update It

> Methodology for the October 1, 2026 refresh; used again for the **Oct 13, 16 and 25 refreshes** (each refresh: fetch docs → diff roster/caps → re-check AA/independents → re-run value math → update HTML → commit). Use this to re-run the analysis in ~5 minutes of agent time (plus web access). The Oct 25 cycle added three questions: **Is Go cheaper than direct? Which coding plan is best value? Does it actually work from India?**

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

**Oct 25 add-on wave (3 parallel agents + direct verification):** (9) India availability — signup country lists, phone rules, payment methods, regional inference blocks; (10) Go vs direct — per-model list-price break-even at the frozen token profile; (11) coding-plan value — Go, Z.ai, Xiaomi, StepFun, Kimi, MiniMax, Alibaba, Meta, normalized to $/heavy-request. Vendor billing/FAQ pages were then fetched directly to confirm the payment and region claims (OpenCode UPI, Z.ai PayPal, Xiaomi Waffo, StepFun Stripe, Alibaba Singapore-only, Meta US-first).

### Why multiple agents

- Different search backends surface different leaderboards and regional sources.
- Cross-agent contradictions expose unreliable numbers (e.g. DeepSeek V4 Pro ranged 36–44 on "AA" across agents; direct fetch confirmed **36** on v4.3.2).
- Per-vendor agents can go deep on model cards and vendor benchmark tables, while the evaluator agent covers cross-vendor boards.

### Local calibration (the secret sauce)

For limits and value math, aggregate token/cost statistics were computed from the local OpenCode session database.

**V1 database (Sep–Oct, schema with `session`):**

```bash
sqlite3 -readonly ~/.local/share/opencode/opencode.db \
  "SELECT json_extract(model,'\$.id'), COUNT(*), SUM(tokens_input), SUM(tokens_output),
          SUM(tokens_reasoning), SUM(tokens_cache_read), SUM(cost)
   FROM session GROUP BY 1 ORDER BY COUNT(*) DESC;"
```

**V2 database (Oct 16+, schema with `session_v2` / `session_message`)** — per-model aggregates per assistant message:

```bash
sqlite3 -readonly ~/.local/share/opencode/opencode.db \
  "SELECT json_extract(data,'\$.model.id'), COUNT(*), SUM(json_extract(data,'\$.tokens.input')),
          SUM(json_extract(data,'\$.tokens.output')+json_extract(data,'\$.tokens.reasoning')),
          SUM(json_extract(data,'\$.tokens.cache.read')), ROUND(SUM(json_extract(data,'\$.cost')),4)
   FROM session_message WHERE type='assistant' GROUP BY 1 ORDER BY 2 DESC;"
```

Then message-level `tokens`/`cost` fields are aggregated to compute the user's true per-request profile (7.8k input / 1.1k output+reasoning / 146k cache read), peak burst rates (630 req/h), and rolling 5h/7d/30d spend. Only aggregates are used; no session content, titles, or client data. **Note (Oct 25):** the Sep 15–Oct 1 calibration comes from the primary machine's v1 database (this repo's second machine has only a v2 DB). The v2 DB now has 1,419 DeepSeek messages at 8.2k in / 1.25k out / 153k cache — within ~5% of the frozen profile — but it is used only as a sanity check, not a new baseline.

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
| Zen pricing/models + free models | https://opencode.ai/docs/zen/ · https://opencode.ai/v2/docs/console/models/ |
| Whole-user telemetry | https://opencode.ai/data |
| Changelog (v2) + releases (v1) | https://opencode.ai/changelog · https://github.com/anomalyco/opencode/releases |
| Model list JSON | https://opencode.ai/inference/go/v1/models · https://opencode.ai/inference/v1/models |
| Roster change tracker | https://julien.cloud/opencode-go-models/ |
| Intelligence index | https://artificialanalysis.ai/leaderboards/models · https://artificialanalysis.ai/changelog |
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
| **Gemini 4 Argon (new on Go)** | https://artificialanalysis.ai/models/gemini-4-argon · https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-4-argon/ |
| **Reflection Beam (Beam Free)** | https://artificialanalysis.ai/models/reflection-beam · https://reflection.ai/blog/introducing-beam |
| **Step 5 open weights** | https://huggingface.co/stepfun-ai/Step-5-Preview |
| **OmO releases / v2 port status** | https://github.com/code-yeongyu/oh-my-openagent/releases · issues #6169/#9389 · PRs #9391/#9415 |
| **Oct 25 roster additions** | https://artificialanalysis.ai/models/kimi-k3-1-pro · https://artificialanalysis.ai/models/minimax-m3-1-flash |
| **Go billing / payment methods (UPI)** | https://opencode.ai/v2/docs/console/billing |
| **Z.ai GLM Coding Plan** | https://docs.z.ai/devpack/overview · https://docs.z.ai/devpack/usage-policy |
| **Xiaomi MiMo Token Plan** | https://mimo.mi.com/docs/en-US/price/token-plan · FAQ https://mimo.mi.com/docs/en-US/quick-start/faq/account · /faq/payment |
| **Kimi Code** | https://www.kimi.com/code/docs/en/kimi-code/models.html · https://www.kimi.ai/membership/pricing |
| **MiniMax M Plan** | https://www.minimax.io/m-plan · https://platform.minimax.io/docs/m-plan/intro |
| **StepFun Step Plan** | https://platform.stepfun.ai/docs/en/step-plan/overview · https://platform.stepfun.ai/docs/en/guides/pricing/details |
| **Alibaba Token Plan (Singapore-only)** | https://www.alibabacloud.com/help/en/model-studio/token-plan-personal-overview |
| **Meta Muse Code** | https://dev.meta.ai/products/muse-code · https://dev.meta.ai/docs/muse-code/subscriptions |
| **Regional availability** | https://ai.google.dev/gemini-api/docs/available-regions · https://docs.x.ai/docs/advanced-api-usage/regions |

---

## 4. Update procedure (quarterly, or on any roster change)

1. **Fetch Go docs** and diff the roster/limits against `analysis/01`. Record additions/removals, cap changes, free-model windows, privacy-table changes and restricted-model settings.
2. **Re-fetch AA pages** for every Go model; capture Intelligence Index **with version**, speed, TTFT, $/task, verbosity. Update `analysis/02` master table.
3. **Check independent boards** (LMArena, Vals, Terminal-Bench, OSWorld) for new Go-model entries — and correct any stale rankings you carried forward.
4. **Recalibrate your profile** with the SQL above (or the burn script pattern in `analysis/04`): recompute cost/request, rolling-window peaks, and capacity per model at Go prices.
5. **Re-run the value math** (`AA ÷ $/req`; `AA × req/mo`) and update tiers and jump analysis in `analysis/05`.
6. **Re-run the Go-vs-direct break-even** (`analysis/12`) and the plan ranking (`analysis/13`): refresh list prices, caps, credit conversions, and quoted quotas. Normalize every plan to **$/heavy-request at the frozen profile** — do not compare token prices, credits and “× usage” directly.
7. **Re-check India availability** (`analysis/14`): country/region selectable, phone rule, payment instrument, inference region. Fetch the vendor billing/FAQ page, not just the marketing page. Update the verdict (🟢/🟡/🔴) and the pre-payment checklist.
8. **Verify privacy policies** — DeepSeek ZDR expiry, any Contributor-SKU terms (now only Muse Spark), free-model zero-retention claims, and any new stealth/free models.
9. **Update the HTML** — the file was generated by a script; simplest path is to ask an agent to regenerate `opencode-go-analysis.html` from the updated markdown (data tables at the top of the generator).
10. **Commit** with a dated message.

*(Fast prompts for a future agent: see §8.)*

## 5. Second-wave topics (Oct 1, 2026) and their refresh triggers

| File | Refresh trigger |
|---|---|
| `08-oh-my-opencode.md` | OMO releases (esp. official v2 support), category renames, fallback-chain changes (`doctor --verbose` is ground truth) |
| `09-opencode-v1-vs-v2.md` | v2 releases (LSP status, history migrator fixes, plugin API freeze), v1 EOL announcement, sharing changes |
| `10-plugins-and-stacks.md` | New ecosystem entries, MCP deprecations, v2 ports of v1 plugins |
| `11-amazing-additions.md` | Any change in your stack (new Azure services, new RPA targets, new repos) — re-run the 80/20 ranking |
| `12-opencode-vs-direct.md` | Any Go or direct list-price change; any new specialist plan that undercuts a single model |
| `13-best-value-coding-plans.md` | Any plan price/credit/quota change; new coding plans; annual-discount changes |
| `14-india-availability.md` | Country/region lists, phone-verification rules, payment methods, inference-region blocks |

---

## 6. Rules of thumb learned in this cycle

1. **Never quote an AA score without its index version.** v4.1.1 scores are ~15–20 points higher than v4.3.2 for the same models (v4.3.2, with the Sep 19 methodology patch, is still current as of Oct 16).
2. **Terminal-Bench version + harness matters more than the model.** TB2.1 vendor vs Vals can differ by 20 points.
3. **Vendor benchmarks are marketing** until an independent run exists; mark them.
4. **The docs' estimated requests assume light traffic.** Heavy agentic users divide by 3–7×.
5. **Cache-read pricing dominates real agent costs.** A model with 10× cheaper cache can be cheaper in practice than a model with half the output price.
6. **Reasoning effort is the biggest cost lever** (3.6–6.5× on Kimi K3).
7. **Free/stealth models are the highest-variance choice** — great value, unknown identity/policies; keep them off critical and sensitive work. **But check the terms per model now:** the Oct 16 free twins (DeepSeek/GLM) are zero-retention, unlike most stealths.
8. **Roster churn is weekly — now literally.** Oct 12–25 added Beam Free, Argon, four Zen free models, paid-ified Step 5, then added K3.1 Pro + M3.1 Flash and removed Space Bunny + LongCat 2.5 Free. Any analysis older than a week is stale; re-run the diff procedure above.
9. **Contributor SKUs are a pricing category — and they can exit it.** Gemini 4 Argon was documented as a training Contributor SKU on Oct 16 and as **ZDR/not trained** on Oct 25. Only Muse Spark 1.3/1.2 Contributor still trains. Re-read the privacy table every cycle; do not carry a data-policy claim forward.
10. **A plan's advertised unit is not comparable.** Dollars, credits, requests and “× usage” are different currencies. Rank on **$/heavy-request at your own token profile**, then adjust for AA quality, quota transparency, OpenCode compatibility, privacy and **India access**. A plan that cannot be bought from India has no rank at all.
11. **Availability is a gate, not a footnote.** Check country selectability and the phone-country rule before doing value math. Alibaba Token Plan (Singapore-only, phone must match) and Meta Muse Code (US-first) are excluded no matter how cheap they look.

---

## 7. Refresh log

| Date | What changed | Files touched |
|---|---|---|
| Oct 1, 2026 | Full research wave (8 agents) — initial dossier | all |
| Oct 13, 2026 | Roster refresh: Haiku 5.5, Step 5 Free, DS cap $80, Space Bunny paid; OmO 5.1.32; v1.19.0/v2.0.28 | all |
| Oct 16, 2026 | Argon on Go; Step 5 paid + open weights; Beam Free; Zen free twins (zero-retention); Grok 4.6/K2.6/M2.7 removed; v2.0.31 on this machine; OmO 5.1.34 (Argon chains, dual-host still in review); telemetry refresh | all + HTML + README |
| Oct 25, 2026 | K3.1 Pro + M3.1 Flash on Go; Space Bunny + LongCat 2.5 Free removed; Argon corrected to ZDR/50%-off $30; Step 5 back to $15; 1017 checkpoint AA 45; Vals v2.2 / LMArena Vision corrections; v2.1.4 + v1.19.4; OmO 5.1.48; new India, Go-vs-direct and best-value-plan analyses; UPI as the India-first payment path | all + README + RESEARCH-GUIDE + HTML |

## 8. Fast prompts for a future agent (refreshed)

- *"Fetch https://opencode.ai/docs/go/ and diff the model roster, monthly limits and estimated requests against analysis/01-go-roster-and-limits.md; update the file and list changes."*
- *"Fetch https://opencode.ai/docs/zen/ and list every free model with its retention/training terms; diff against analysis/06-free-models-and-privacy.md."*
- *"For each model in the Go roster, fetch its Artificial Analysis model page and record Intelligence Index vX.Y.Z, output speed, TTFT and $/task; update analysis/02-benchmarks.md."*
- *"Recompute my token profile from the local v2 DB (`session_message`, type='assistant') read-only and refresh analysis/04-limits-and-burn-rate.md capacity tables."*
- *"Check https://github.com/code-yeongyu/oh-my-openagent/pulls (esp. #9391/#9415) for the v2 dual-host rollout status; update analysis/08 and analysis/09."*
- *"Re-scrape the opencode ecosystem page + awesome-opencode for new plugins/MCPs; update analysis/10."*
- *"Check anomalyco/opencode releases (v1 and v2) and reconstruct the version deltas since the last refresh; update analysis/09."*
- *"Audit India availability for every plan in analysis/13: can you select India at signup, is a +91 number accepted, which payment instruments are documented, and is inference region-blocked? Update analysis/14 and the India columns in 12/13/README."*
- *"Recompute the Go-vs-direct break-even for every Go model at the frozen profile (7.8k in / 1.1k out / 146k cache) using current list prices; update analysis/12."*
- *"Rank every coding plan on $/heavy-request at the frozen profile, then adjust for AA quality, quota transparency, OpenCode support, privacy and India access; update analysis/13."*
