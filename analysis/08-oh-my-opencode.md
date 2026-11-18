# 08 — Oh My OpenCode (now oh-my-openagent / OmO): The Complete Guide + Go Model Map for Heavy Work

> **Snapshot: October 1, 2026, refreshed October 13, 16, 25 and November 17, 2026.** **Nov 17: AA v5.0.1 re-baseline applied** — every AA score and allowance in the model map (§5) is v5.0.1 / measured profile (heavy mix noted) unless labeled (v4.3.2).
> **Nov 18 delta:** usage re-based to the Nov 18 pull (**35,013 requests/30d: 3,457 in / 799 out / 198,806 cache-read** — DeepSeek **$0.00210/req → 47,619 req/mo**); **GLM-5.3 caps $15→$200 (Plus $400, Teams $205)** — it is a bulk lane now (3,331 req/mo measured, 20×), not a ration; **Argon retention corrected to 55-day** (worst on roster — privacy-safe escalation is K3.1 Pro). OpenCode **v2.3.2** is latest (v2.3.1: timed-out shell → background, background compaction summary, GPT-6.2 models in ChatGPT picker, plugin updates from Settings, comment-on-selection, read/glob/grep/Code-Mode shapes; v2.3.2: GPT-6.2 prompt caching on Responses routes + webfetch structured-output fix; v1 **1.19.6**); this machine still runs **v2.3.0** (upgrade pending).
> **Nov 17 delta:** OmO **5.1.75** is current (Nov 16). Since 5.1.48 the theme is **accounts + remote sessions**: `omo login` now signs in (the "accounts aren't available yet" refusal is gone), and the moment it completes it **enables remote sessions for the device** (`omo remote disable` opts out). The thread gateway can **wake a session that is not running** on this or another of your devices (senpi `2026.11.15-2`, device service 0.1.39); memory sync across devices landed with a wave of reliability fixes (5.1.73–5.1.75); computer-use v3 scaffolding keeps landing but is **not user-visible yet**. **OpenCode v2 dual-host support is still NOT shipped:** PR [#9391](https://github.com/code-yeongyu/oh-my-openagent/pull/9391) remains open — the branch has grown to carry the tools/hooks and agents slices (parity matrix at 13 live / 13 todo rows) and an external real-engine harness reports 26/28 checks passing on OpenCode 2.2.7 with two known bridge defects. This machine runs **OpenCode v2.3.0 (v2.3.2 latest — upgrade pending)**, so OmO Ultimate stays v1-only (v1 **1.19.6**) or OmO Native. The model-map advice below is **re-tuned on Nov 17–18: `gemini-4-argon` (AA 50) primary for non-client work (55-day retention), `kimi-k3.1-pro` (AA 46) escalation/fallback AND privacy-safe pick** (upstream's 5.1.47 K3.1 Pro prompts still cover the Kimi rung), MiMo-Pro reasoning slots, free-twin floor.
> **Oct 25 delta:** OmO **5.1.48** was current Oct 25. **5.1.47 added Kimi K3.1 Pro-specific Sisyphus/Atlas prompts** — upstream now handles the AA 55.1 (v4.3.2-era; 46 on v5.0.1) model that replaced K3 at the top of the Go roster. **5.1.48** shipped the `senpi 2026.10.25-2` engine, cut the 748-skill startup from **83s to 1.4s**, and added **nested task session trees** (child work is grouped under its parent instead of flooding the session list). **Gemini 4 Argon is now `gemini-4-argon` at $2/$10/$0.10 with a $30 cap and is documented ZDR/not trained** — the old Contributor caveat is withdrawn; **Step 5 is paid at a $15 cap** (4× promo ended); **LongCat 2.5 Preview Free is gone** (it returned as LongCat 2.5 Free in November). Primary sources: [code-yeongyu/oh-my-openagent](https://github.com/code-yeongyu/oh-my-openagent), [omo.dev/docs](https://omo.dev/docs), [OpenCode V2 migration issue #6169](https://github.com/code-yeongyu/oh-my-openagent/issues/6169), [opencode.ai/docs](https://opencode.ai/docs/) + [opencode.ai/v2/docs](https://opencode.ai/v2/docs/).
> **Naming (important):** the project renamed to **oh-my-openagent (OmO)**. The npm package is still `oh-my-opencode` (dual-published); install with `bunx oh-my-openagent install`. Do NOT `bunx omo` — unrelated package by a different author. Config files accept both `oh-my-openagent.json[c]` and legacy `oh-my-opencode.json[c]`.

---

## 1. What it is: three editions

| Edition | Host | What you get | Install |
|---|---|---|---|
| **Ultimate (omo for OpenCode)** | OpenCode v1 | Full harness: 11 agents, 52+ lifecycle hooks, 26 tools, slash commands, Team Mode, ulw/Ralph loops, hashline edits, built-in MCPs | `bunx oh-my-openagent install` (TUI walks you through providers) |
| **Light (omo for Codex CLI)** | Codex CLI | Portable pieces: rules, comment-checker, git-bash, LSP, ultrawork, ulw-loop, telemetry — no agent orchestration | `npx lazycodex-ai install` |
| **OmO Native (`omo-ai`)** | Standalone (`senpi` engine) | OMO built in, no OpenCode host needed; `omo setup` imports providers/MCPs/skills | `curl -fsSL https://get.omo.dev/install.sh \| bash`, then `omo` |

Non-interactive install: `bunx oh-my-openagent install --no-tui --platform=opencode …`. Requires OpenCode ≥1.4.0 (use **v1.18.x–1.19.x**, never v2 for Ultimate). Verify with `bunx oh-my-openagent doctor --verbose` — it prints the effective version, resolved models per slot, and capability fallbacks.

⚠️ **Version-channel trap (updated Nov 17):** latest is **5.1.75** (Nov 16); npm `oh-my-openagent` still serves the stale **4.19.4** Ultimate channel. 5.x ships via **GitHub releases / `omo-ai` / unpkg**. If `doctor` reports 4.x, you installed the stale channel — reinstall from GitHub. `omo login` now signs in and enables remote sessions for the device (the old "accounts aren't available yet" refusal is gone); `senpi 2026.11.15-2` is the matching native engine build.

Config locations (4.x legacy): project `.opencode/oh-my-opencode.json` > user `~/.config/opencode/oh-my-opencode.json`. New unified (5.x): `~/.omo/omo.jsonc` + `.omo/omo.jsonc`, with `[opencode]` / `[native]` / `[codex]` blocks and `profiles.<name>` layers. A migration engine imports legacy configs once (`oh-my-openagent config migrate --dry-run`).

---

## 2. The agents (who does what)

| Agent | Role | Default model thinking |
|---|---|---|
| **Sisyphus** | Main orchestrator. Plans with todos, delegates to specialists, verifies, never stops halfway. Prompt built against Claude-style instruction following; thinking budget 32k, maxTokens 64k | Claude Opus chain → **Kimi K2.6/K3** → GLM fallback |
| **Sisyphus-Junior** | Worker executor (cannot delegate; mid-tier model is fine — intelligence lives in the prompt) | Sonnet-class |
| **Atlas** | Execution conductor: reads plan, accumulates wisdom in `.sisyphus/notepads/<plan>/`, verifies independently. Used with `/start-work`, never alone | Opus/Sonnet-class |
| **Prometheus (+ plan-consultant / plan-reviewer in 5.x)** | Strategic planner (interview mode, Tab or `@plan`), gap analysis, ruthless plan review with resubmit loop | Opus-class; reviewer often GPT Astra-class |
| **Oracle → `architect` category** | Read-only high-IQ consultant: architecture, debugging after 2+ failures, security/perf review. Cannot write/edit | GPT/Opus-class |
| **Librarian** | Reference grep: official docs (Context7), OSS examples (grep.app/GitHub), evidence-based. Cannot write | Cheap (Big Pickle / GLM / Luna-fast class) |
| **Explore** | Blazing-fast codebase grep. Cannot write | Cheapest/fastest (Nano / Haiku / Grok-class) |
| **Multimodal-Looker** | Visual specialist: PDFs/images/diagrams → text (saves main-context tokens) | Gemini-flash class |
| **Frontend UI/UX Engineer** | Frontend persona (bold direction, anti-slop). In current docs: `visual-engineering` category + `frontend` skill | Gemini 3 Pro / Fable-class |
| **Hephaestus** | GPT-path worker (dedicated prompt path for GPT models; older GPT is a poor Sisyphus fit) | GPT-5.5-class |

**5.x renames (Oct 13):** `Metis/Momus` aliases are closed — the planner/reviewer are now the plan-gated **`plan-consultant` / `plan-reviewer`** agents (define custom agents if you still reference the old names). Architecture consults go through **`task(category:"architect")`**, not an agent. 11 agents, **54+** hooks.

Invoke: `@oracle …`, `delegate_task(category=…, background=…)`, `ultrawork`/`ulw`, `/ulw-plan` → `/ulw-execute`, `/ralph-loop "goal"`, `/start-work [plan]`, `/goal`, `/refactor`, `/init-deep`, `/remove-ai-slops`.

---

## 3. The category system (the real routing layer)

Sisyphus doesn't pick models — it picks a **category**, and the category maps to a model. Current built-ins:

| Category | Meaning | Upstream default (for reference) |
|---|---|---|
| `visual-engineering` | Frontend/UI/design | Fable-class max |
| `ultrabrain` | Hard logic/architecture | GPT Astra-class max |
| `deep-low` / `deep-high` | Default backend lane / escalation lane | GPT Sol-class medium → Astra high |
| `artistry` | Creative/novel work | Fable-class max |
| `quick` | Trivial/typo/single-file | Luna-fast / Haiku-class low |
| `unspecified-low` / `unspecified-high` | General fallbacks | Sonnet-medium / Opus-medium |
| `writing` | Docs/prose | Opus-class low |
| `architect` | Read-only design advice | consult lane |

Go-relevant fallback rungs already in upstream chains: `plan-consultant` → **kimi-k3 (max)**; `plan-reviewer` → … → **glm-5.2**; `unspecified-low` → **mimo-v2.6-pro (max)** → grok-4.7 (xhigh); `unspecified-high` → **glm-5.3 (max)** → kimi-k3 (max); `quick` tail → **mimo-v2.6-flash (low)**; explore/librarian tail → deepseek-flash / qwen3.7-plus / minimax-m2.7; visual chain → **kimi-k3 (max)**.

### 3b. Upstream default chains, verbatim (5.1.x, Oct 25 — override only what you must)

These are the exact fallback chains from upstream `configuration.md` / `omo-json.md`. Profiles: `daily-normal` = `claude-opus-5-5 (medium) → kimi-k3 (max) → glm-5.3 (max)`; `daily-heavy` = `claude-fable-5-1 (xhigh)`. **New in 5.1.34:** `gemini-4-argon (high)` sits directly ahead of the previous pro rung in the oracle/momus/plan-reviewer chains (GPT heads keep first place). **New in 5.1.47: K3.1 Pro-specific Sisyphus/Atlas prompts** — upstream's Kimi rungs now have a prompt path tuned for `kimi-k3.1-pro`. On Go, K3.1 Pro **strictly dominates K3** (AA 46 vs 17@low — K3 is unscored at max on v5.0.1; 191 vs 155 measured req/mo, same $15 cap), so the configs below pin K3.1 Pro with K3 as the fallback.

| Slot | Upstream chain (first = default) |
|---|---|
| agents `explore` / `librarian` | `kimi-for-coding-highspeed (off) → gpt-6-luna-fast (low) → **claude-haiku-5-5 (medium)** → deepseek-flash (max) → qwen3.7-plus → minimax-m2.7` |
| agents `plan-consultant` | `fable-5-1 (max) → opus-5-5 (max) → **kimi-k3 (max)**` |
| agents `plan-reviewer` | `gpt-6-astra (xhigh) → opus-5-5 (max) → **gemini-4-argon (high)** → gemini-3.1-pro (high) → glm-5.2` |
| `oracle` / `momus` consult chains | `gpt-6-astra → … → **gemini-4-argon (high)** → previous pro rung` |
| `ultrabrain` | `gpt-6-astra (max) → gpt-5.6-sol (max)` |
| `deep-low` | `gpt-6.1-sol (med) → gpt-6.1-sol-fast (med) → gpt-5.6-sol (med) → …` |
| `deep-high` | `gpt-6-astra (high)` (single) |
| `quick` | `gpt-6-luna-fast (low) → **haiku-5-5 (med)** → deepseek-flash (off) → qwen3.6-flash → minimax-m3/m2.7 → … → glm-5.3-flash → mimo-v2.6-flash` |
| `unspecified-low` | `sonnet-5-5 (med) → **mimo-v2.6-pro (max)** → grok-4.7 (xhigh) → gpt-6.1-sol → … → qwen3.8-max → deepseek-v4-pro → mimo-v2.5-pro` (upstream chain verbatim — `mimo-v2.5-pro` left the Go catalog Nov 17) |
| `unspecified-high` | `opus-5-5 (med) → **glm-5.3 (max) → kimi-k3 (max)**` |
| visual / artistry | `fable-5.1 (max) → kimi-k3 / opus-5-5 (max)` |
| `writing` | `opus-5-5 (low) → opus-4-6 (max)` (Claude-only upstream) |

**What this means for your Go configs below:** upstream already validates **kimi-k3 (max)** as the Go-reachable rung for orchestrator-adjacent slots (5.1.47 adds K3.1 Pro-specific prompts), **mimo-v2.6-pro (max)** for general reasoning, **glm-5.3 (max)** for review/artistry fallback, **gemini-4-argon (high)** for consults/review (vs the GPT heads), and **haiku-5-5** in the cheap tails. Configs A/B pin **`gemini-4-argon` (high)** as the Sisyphus primary — after the Nov 17 re-baseline it is both the AA ceiling (50) and the best top-end value, and it is already an upstream rung (5.1.34) — with **`kimi-k3.1-pro` (max)** substituted for K3 (it dominates on Go) as the escalation/fallback rung, so the **5.1.47 K3.1 Pro-specific Sisyphus/Atlas prompts** stay in play. One honest caveat: upstream's Sisyphus/Atlas prompt path is tuned for Claude- and Kimi-style models; Argon has no Sisyphus-specific prompt — if orchestration quality degrades (delegation loops, ignored plan mechanics), fall back to `kimi-k3.1-pro (max)`. Config C stays free-tier. `writing` has no Go rung upstream — Configs use `glm-5.3-flash (low)`.

---

## 4. The machinery: hooks, tools, Team Mode, loops

- **52+ lifecycle hooks:** IntentGate keyword detection (`ultrawork|ulw`, `team-mode`, `hyperplan`), **todo-continuation-enforcer** (forces the agent back when todos are incomplete), **comment-checker** (strips AI slop), think-mode, context injection (AGENTS.md/README/rules), output truncation (tool/grep truncators, aggressive truncation experimental), compaction preservation, session recovery, model/runtime fallbacks, background notifications, telemetry (anonymous PostHog, off via `OMO_SEND_ANONYMOUS_TELEMETRY=0`). Disable via `disabled_hooks`.
- **26 tools:** full LSP suite (diagnostics/rename/goto/references/symbols), AST-grep (25 langs), `call_omo_agent` / `delegate_task` / `background_output` / `background_cancel`, session tools (list/read/search), hash-anchored `LINE#ID` edits, skill/MCP loaders, 12 `team_*` tools.
- **Team Mode (OFF by default):** lead + up to 8 members, shared mailbox + task list, optional tmux grid, `teams.<name>` (8 members / 4 parallel / 120 min), DAG up to 64 nodes (`mass ulw`).
- **Loops:** `ultrawork|ulw` (explore→research→implement→diagnostics→done), `/ralph-loop` (until `<promise>DONE</promise>`, default 100 iters), `/ulw-loop` (ralph+ultrawork), `/cancel-ralph`, `/goal`.
- **Skills/commands/MCPs:** `playwright` (browser), `git-master` (atomic commits), `frontend`, `lsp`, `ultrawork`, `team-mode`, `review-work`, `debugging`, `security-review`, `visual-qa`; `/init-deep`, `/refactor`, `/handoff`, `/hyperplan`; built-in MCPs `websearch` (Exa), `context7`, `grep_app` (+ skill-scoped `playwright`, `git_bash`, `lsp`). Full Claude Code compat layer (commands/agents/skills/MCPs/hooks).

---

## 4b. Replacing your manual DeepSeek multi-agent workflow with OmO delegation

Today you run `deepseek-v4.1-flash` and hand-write prompts like *"spin up 3 agents: one explores X, one implements Y, report back"* — you are the orchestrator, and DeepSeek just executes. OmO flips this: **Sisyphus becomes the orchestrator** and your manual delegation prompts become unnecessary. What changes:

| Today (manual, DS V4.1 Flash) | With OmO (Sisyphus primary = Argon, escalation K3.1 Pro) |
|---|---|
| You write "spin up N agents to do A/B/C" | You write the *goal only*: `/ultrawork Add retry with backoff to the Kafka consumer` — Sisyphus plans, fans out researchers/workers, verifies |
| You specify per-agent instructions | `delegate_task(category="explore"\|"librarian"\|"quick"\|…, background=…)` picks the right specialist + model automatically |
| One model does everything (planning + grep + edits) | Planning/delegation runs on the smart primary; grep/edits run on cheap slots (Step 5 / Haiku / MiMo-Flash / DS Flash) |
| You babysit: "did agent 2 finish? merge results" | `todo-continuation-enforcer` + verifier agents refuse to stop halfway; Atlas accumulates wisdom in `.sisyphus/notepads/` |
| Repeat loops by re-prompting | `/ralph-loop "goal"` / `/ulw-loop` run until `<promise>DONE</promise>` (default 100 iters) |
| Your DS V4.1 Flash allowance funds all of it | Volume moves to free/cheap slots; DS V4.1 Flash becomes the *explore/looker* lane, not the driver |

**The one thing you keep doing:** the *goal* and the *constraints* ("don't start servers", "read-only DB", "this repo's PHI rules") — those live in AGENTS.md/skills now, not in per-task prompts. And keep approval gates on: OmO multiplies request volume 3–5×, so a runaway loop burns the $15-tier rations fast — hence `modelConcurrency` caps in the configs below.

**First-run recipe (v1 OpenCode):** install → `doctor --verbose` → paste **one** of Config A/B/C into `~/.omo/omo.jsonc` (5.x) → set session model to the config's primary → `/ultrawork <a real task>`. Start with B.

---

## 5. Go model map for VERY heavy work (the money section)

OMO multiplies volume: one `ultrawork` fans out to main + researchers + workers + verifier + retries — **plan for 3–5× requests vs single-agent, 6–12× for `mass ulw` / Team Mode / Ralph loops**. Divide every allowance below by ~4 for OMO-week planning. Numbers use the **measured fleet profile** (3,457 in / 799 out / 198,806 cache-read per request — 35,013 provider-side requests, Nov 18 pull); the frozen heavy mix (7.8k in / 1.1k out / 146k cache) is the conservative secondary and vendor (Console-published) estimates are ~3–7× lighter (see `04`).

**Rule 0:** the orchestrator (Sisyphus primary) is the ONE slot where intelligence matters most. Use **`gemini-4-argon` (high)**: **AA 50 — the Go ceiling** — plus Vals launch 69.24% (#1 Go agentic), not trained but **55-day retained (worst on roster — non-client work only)**, **862 req/mo** measured (728 heavy), and 50%-off through Nov 30. It is also an upstream rung (5.1.34). Escalation/fallback: **`kimi-k3.1-pro` (max)** (AA 46, **191 req/mo** measured / 269 heavy) — the upstream Kimi rung with **5.1.47 K3.1 Pro-specific Sisyphus/Atlas prompts**; use it for 1M-ctx/Max-effort work, for client/PHI planning, or if Argon orchestration degrades (Argon has no Sisyphus-specific prompt path). Everything else is negotiable. Community reports agree: Kimi K2.6/K3/K3.1 "behaves very similarly to Claude"; weak primaries (Haiku/Flash/free) cause delegation loops and half-finished work.

**Shared-budget warning:** several slots below share one model's allowance (e.g. Config B runs ultrabrain + deep + architect all on `mimo-v2.6-pro`). OMO-week math per slot assumes the full allowance — divide further when slots share. Free slots (`glm-5.3-flash-free`, `deepseek-v4.1-flash-free`, `beam-free`) share nothing and cost $0 while their windows last.

| OMO slot | Best Go pick | Reasoning | Allowance math |
|---|---|---|---|
| **sisyphus primary** | **gemini-4-argon, high** (escalation/fallback: kimi-k3.1-pro max) | AA 50 = Go ceiling + Vals #1 Go (launch 69.24%), not trained but 55-day retained; upstream rung since 5.1.34 | $30 tier: 431/wk, 862/mo measured (364/728 heavy) → **~108 OMO-req/wk**. Ration it: primary does planning/delegation, not bulk reads. Non-client only. Escalation: kimi-k3.1-pro (96/wk, 191/mo measured → ~24 OMO-req/wk; privacy-safe) |
| **plan-consultant (Metis)** | **kimi-k3.1-pro, max** | Upstream Kimi rung + 5.1.47 K3.1 Pro prompts; gap analysis needs Claude-like | 96/wk, 191/mo measured → **~24 OMO-req/wk** — shares K3.1 Pro's budget with the escalation rung, keep consults tight |
| **ultrabrain / deep-high / unspecified-low** | **mimo-v2.6-pro, max** | AA 30 (v5.0.1); matches upstream 2nd rung | $15 tier: 2,569/wk, 5,138/mo measured (1,537/3,074 heavy) → **~642 OMO-req/wk** |
| **unspecified-high / artistry / deep executor** | **glm-5.3, max** | AA 32, Claude-like; upstream 2nd/3rd rung | $200 tier: 1,666/wk, 3,331/mo measured (1,860/3,720 heavy) → **~416 OMO-req/wk**. Bulk lane now — spend freely |
| **oracle / architect consults** | **grok-4.7, xhigh** (fallback mimo-v2.6-pro) | AA 35; upstream rung; consults are low-volume | 68/wk, 135/mo measured (79/158 heavy) → **~17 OMO consults/wk** |
| **plan-reviewer** | **glm-5.3, max** (bulk alt: glm-5.3-flash high) | Review needs teeth; flash variant for volume | same as above (bulk lane now) / 4,359/wk (you) for flash |
| **librarian** | **mimo-v2.6-flash, low** (fallback deepseek-v4.1-flash max) | Docs/OSS grep needs AA ~27, not the 46+ tier | 23,728/wk, 47,455/mo measured (16,586/33,171 heavy) → **~5,932 OMO-req/wk** |
| **explore** | **deepseek-v4.1-flash, max** (alt: claude-haiku-5-5 medium) | Upstream has deepseek-flash rung; AA 33 (1017 ckpt; base unmeasured on v5.0.1) | 23,810/wk, 47,619/mo measured (16,129/32,258 heavy) → **~5,950 OMO-req/wk** |
| **free bulk coding** | **glm-5.3-flash-free, high** (alt: deepseek-v4.1-flash-free) | AA 28 zero-retention at $0 (DS free unmeasured on v5.0.1 — 33 via 1017 ckpt); Step 5's free window ended | unlimited (free window) → **unlimited OMO-req/wk** |
| **visual-engineering** | **kimi-k3, max** (bulk CSS: glm-5.3-flash) | Upstream visual chain ends at kimi-k3 (Design Arena #3 — not an AA pick; K3 is unscored at max, 17@low) | ration; flash does 4,359/wk (you) |
| **multimodal-looker** | **deepseek-v4.1-flash, max** | Native vision on the daily driver; retired vision-exp route merged into V4.1 | shares explore budget |
| **quick** | **claude-haiku-5-5, low/medium** (alt: mimo-v2.6-flash low) | Fastest Claude (AA 36 max — best cheap lab model); Sonnet-class coding in Copilot tests; upstream quick tail is Haiku-class | ~2,234/wk at ≤100K context (you, the subagent option) → **~559 OMO-req/wk** (measured 170k-prompt mix bills >100K: 447/wk) |
| **writing** | **glm-5.3-flash, low** | AA 28 prose at volume (avoid Contributor for client docs — trains on data) | 4,359/wk (you) |
| **deep-low bulk research** | **glm-5.3-flash-free, high** (alt: deepseek-v4.1-flash-free / beam-free) | AA 28 zero-retention at $0 — the new value bulk lane (Step 5 is paid now) | unlimited (free window) |

### Config A — HEAVY-MAX: maximum intelligence, everything maxed (burst-oriented, ~2–4 heavy days)

No compromises: the smartest validated Go pick per slot, every reasoning dial at maximum, verbosity guards on (see effort table below). Session model (Sisyphus primary): **`opencode-go/gemini-4-argon` at `high`** (AA 50 ceiling, 55-day retention — non-client only) — escalation/fallback **`opencode-go/kimi-k3.1-pro` at `max`** (the 5.1.47 Kimi prompts cover it). Paste into `~/.omo/omo.jsonc` (5.x):

```jsonc
{
  "$schema": "https://raw.githubusercontent.com/code-yeongyu/oh-my-openagent/dev/assets/omo.schema.json",
  "[opencode]": {
    "agents": {
      "explore": { "model": "opencode-go/deepseek-v4.1-flash", "reasoning": "max" },
      "librarian": { "model": "opencode-go/mimo-v2.6-flash", "reasoning": "low" },
      "multimodal-looker": { "model": "opencode-go/deepseek-v4.1-flash", "reasoning": "max" },
      "plan-consultant": { "model": "opencode-go/kimi-k3.1-pro", "reasoning": "max" },
      "plan-reviewer": { "model": "opencode-go/glm-5.3", "reasoning": "max" }
    },
    "categories": {
      "visual-engineering": { "model": "opencode-go/kimi-k3", "reasoning": "max" },
      "ultrabrain": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "deep-low": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "deep-high": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "artistry": { "model": "opencode-go/glm-5.3", "reasoning": "max" },
      "quick": { "model": "opencode-go/claude-haiku-5-5", "reasoning": "max" },
      "unspecified-low": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "unspecified-high": { "model": "opencode-go/glm-5.3", "reasoning": "max" },
      "writing": { "model": "opencode-go/glm-5.3", "reasoning": "max" },
      "architect": { "model": "opencode-go/grok-4.7", "reasoning": "xhigh" }
    },
    "background_task": { "defaultConcurrency": 5,
      "providerConcurrency": { "opencode-go": 10 },
      "modelConcurrency": { "opencode-go/gemini-4-argon": 2, "opencode-go/kimi-k3.1-pro": 2, "opencode-go/kimi-k3": 2, "opencode-go/glm-5.3": 2, "opencode-go/grok-4.7": 2, "opencode-go/qwen3.8-max": 2 } },
    "experimental": { "aggressive_truncation": true },
    "telemetry": { "enabled": false }
  }
}
// Look_at vision: opencode-go/deepseek-v4.1-flash (native vision). Final visual verify: opencode-go/qwen3.8-max (OSWorld #1, rationed ~8/day).
// Optional add (non-client work only): set "architect" to opencode-go/gemini-4-argon (high) — upstream rung since 5.1.34, not trained but 55-day retained; shares the primary's 862 req/mo budget.
```

Maxed-out notes: Kimi `max` on K3 is unscored on v5.0.1 (the only K3 score is 17 @low — measurement-artifact risk, don't over-read) and costs ~1.74× low — always `max`, temp 1.0, never switch models/effort mid-session (kills cache + quality). Argon `high` is the AA 50 ceiling and the primary; K3.1 Pro (AA 46) is the escalation ration on max. Grok `xhigh` needs `textVerbosity:low` (xhigh burns ~81K output tokens/task otherwise). Haiku `max` = AA 36 (vs 25 med, 19 low) — worth it here, not for volume. MiMo-Pro: any effort level behaves identically, keep max. Qwen Max `xhigh`, DS effort 100, Step `high`, GLM-5.3 `max` (default, can't disable thinking).

OMO-week budget (measured profile, weekly ÷ 4): primary Argon ~108 (non-client only) · K3.1 Pro escalation/consults ~24 · mimo-pro slots ~642 shared across ultrabrain/deep/unspecified-low · glm-5.3 slots ~416 shared (bulk lane now) · grok consults ~17 · Qwen Max verify ~26 shared with nothing (dedicated) · DS explore ~5,950 · mimo-flash ~5,932 · haiku-max (burns faster than the ~559 med estimate — watch it) · glm-flash writing (draws from the 1,090 pool). **5h burst ceilings:** Argon 172, K3.1 Pro 38, K3 31, mimo-pro 1,028, GLM-5.3 666, Grok 27 per 5h — a maxed Ralph afternoon can dent K3.1 Pro's 5h window (GLM-5.3's is now 13× roomier); that is what Config B fixes.

### Config B — VALUE-8H: maximum intelligence, minimum cost (best bang for buck — start here)

Intelligence first, priced for **8 hours of intermittent heavy programming per day**. Same premium-primary doctrine (the one slot where intelligence decides everything) — now **`gemini-4-argon` (AA 50)** rationed to **~29 plans/consults per day** (862 req/mo measured), planning/delegation only, never bulk; **`kimi-k3.1-pro` (AA 46, ~6/day)** is the escalation + plan-consultant rung (5.1.47 K3.1 Pro prompts). The value masterstroke: **`deep-low` runs on `glm-5.3-flash-free` (AA 28, zero-retention, $0)** — your old manual-DeepSeek bulk lane, now free and cleaner (the free DeepSeek twin is the alternate). Only one paid premium besides the primary: `mimo-v2.6-pro` (AA 30 at $0.00292/req measured) for reasoning; review/artistry/volume drop to `glm-5.3-flash`; consults move from Grok to mimo-pro (saves the $15 Grok allowance entirely):

```jsonc
{
  "$schema": "https://raw.githubusercontent.com/code-yeongyu/oh-my-openagent/dev/assets/omo.schema.json",
  "[opencode]": {
    "agents": {
      "explore": { "model": "opencode-go/deepseek-v4.1-flash", "reasoning": "max" },
      "librarian": { "model": "opencode-go/mimo-v2.6-flash", "reasoning": "low" },
      "multimodal-looker": { "model": "opencode-go/deepseek-v4.1-flash", "reasoning": "max" },
      "plan-consultant": { "model": "opencode-go/kimi-k3.1-pro", "reasoning": "max" },
      "plan-reviewer": { "model": "opencode-go/glm-5.3-flash", "reasoning": "high" }
    },
    "categories": {
      "visual-engineering": { "model": "opencode-go/kimi-k3", "reasoning": "max" },
      "ultrabrain": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "deep-low": { "model": "opencode/glm-5.3-flash-free", "reasoning": "high" },
      "deep-high": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "artistry": { "model": "opencode-go/glm-5.3-flash", "reasoning": "max" },
      "quick": { "model": "opencode-go/claude-haiku-5-5", "reasoning": "low" },
      "unspecified-low": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "unspecified-high": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "writing": { "model": "opencode-go/glm-5.3-flash", "reasoning": "low" },
      "architect": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" }
    },
    "background_task": { "defaultConcurrency": 5,
      "providerConcurrency": { "opencode-go": 10 },
      "modelConcurrency": { "opencode-go/gemini-4-argon": 2, "opencode-go/kimi-k3.1-pro": 2, "opencode-go/mimo-v2.6-pro": 4 } },
    "experimental": { "aggressive_truncation": true },
    "disabled_hooks": ["comment-checker"],
    "telemetry": { "enabled": false }
  }
}
```

Why this wins: the orchestrator is the AA 50 ceiling (Argon; the 5.1.47 K3.1 Pro prompts cover the escalation/consult rung), reasoning stays AA 30 (cheapest frontier-class per call), and ~70% of OMO volume (deep-low, explore, librarian, quick, writing) runs at $0–$0.003/req. The mimo-pro allowance (~180/day shared across ultrabrain/deep-high/unspecified/architect) covers an 8h heavy day because consults are low-volume by design.

**8h daily budgets (monthly ÷ 30, measured profile):** Argon ~29/day (non-client only) — when spent, escalate to K3.1 Pro ~6/day, then drop to the free GLM-5.3-Flash lane (AA 28, zero-retention) for the rest of the day; mimo-pro ~171/day shared; GLM-Flash ~291/day; DS ~1,590/day; haiku-medium ~149/day (AA 25 at medium — flip to max/AA 36 only for hard quick tasks); mimo-flash ~1,582/day; free twins ∞. A heavy 8h day burns roughly: 10–20 Argon + 4–6 K3.1 Pro + 60–100 mimo-pro + 200–400 Flash-tier + unlimited free twins — inside every cap with margin.

### Config C — ECO-24: super-duper min cost with best intelligence, runs 24/7 and never runs out

No Kimi, no MiMo-Pro, no Grok, no other ration model. Primary runs on **`glm-5.3-flash-free` (AA 28, zero-retention, $0)** — the free twins (GLM 28 / DeepSeek unmeasured on v5.0.1 — 33 via the 1017 ckpt) are better free lanes than the paid Step 5 that replaced the old free preview; everything else is $80/$60/$30-tier volume. **Design rule: every paid slot's sustained rate (monthly ÷ 730h) stays above its lane's continuous demand** — combined lanes give ~200 req/h of sustained capacity (measured) plus ∞ free lanes, so a 24/7 Ralph loop at 20–50 req/h spread across lanes never binds any cap. Expect a lower orchestration ceiling than A/B and keep tasks small:

```jsonc
{
  "$schema": "https://raw.githubusercontent.com/code-yeongyu/oh-my-openagent/dev/assets/omo.schema.json",
  "[opencode]": {
    "agents": {
      "explore": { "model": "opencode-go/mimo-v2.6-flash", "reasoning": "low" },
      "librarian": { "model": "opencode-go/mimo-v2.6-flash", "reasoning": "low" },
      "multimodal-looker": { "model": "opencode-go/deepseek-v4.1-flash", "reasoning": "medium" },
      "plan-consultant": { "model": "opencode/glm-5.3-flash-free", "reasoning": "high" },
      "plan-reviewer": { "model": "opencode-go/glm-5.3-flash", "reasoning": "high" }
    },
    "categories": {
      "visual-engineering": { "model": "opencode-go/glm-5.3-flash", "reasoning": "max" },
      "ultrabrain": { "model": "opencode-go/glm-5.3-flash", "reasoning": "max" },
      "deep-low": { "model": "opencode/glm-5.3-flash-free", "reasoning": "high" },
      "deep-high": { "model": "opencode-go/glm-5.3-flash", "reasoning": "max" },
      "artistry": { "model": "opencode-go/glm-5.3-flash", "reasoning": "max" },
      "quick": { "model": "opencode-go/mimo-v2.6-flash", "reasoning": "low" },
      "unspecified-low": { "model": "opencode-go/deepseek-v4.1-flash", "reasoning": "medium" },
      "unspecified-high": { "model": "opencode-go/glm-5.3-flash", "reasoning": "max" },
      "writing": { "model": "opencode-go/glm-5.3-flash", "reasoning": "low" },
      "architect": { "model": "opencode-go/glm-5.3-flash", "reasoning": "max" }
    },
    "background_task": { "defaultConcurrency": 5,
      "providerConcurrency": { "opencode-go": 10 } },
    "experimental": { "aggressive_truncation": true },
    "disabled_hooks": ["comment-checker"],
    "telemetry": { "enabled": false }
  }
}
// Main session model: opencode/glm-5.3-flash-free (fallback: opencode-go/glm-5.3-flash).
```

Honest limits of C: the free GLM lane is **not validated as a Sisyphus primary** (the Kimi rung — now K3.1 Pro — is the documented Go path) — if you see delegation loops, ignored plan mechanics, or read-only agents attempting writes, that is the weak-orchestrator failure mode: switch the session model to `gemini-4-argon` (or `kimi-k3.1-pro`) (= Config B) for that task. The free windows are limited (as Step 5's ending showed — it went paid Oct 15) — fallbacks are baked in: primary becomes `glm-5.3-flash` (AA 28, $60 tier, still 24/7-capable at ~14/h sustained) and B becomes the new floor.

**24/7 rotation (one shared allowance, normalized per model — the per-model limits are solo-usage figures, not separate pools):**
- **Night shift (unattended):** free GLM/DeepSeek primary + MiMo-Flash explore/librarian only. Smallest blast radius, $0 + deepest $60-tier allowance.
- **Day shift:** add DS V4.1 Flash explore/looker (~72/h sustained), GLM-Flash review/writing (~14/h), Haiku-medium quick (~7/h), LongCat/Qwen-Flash overflow lanes.
- **Rollover rule:** when the shared rolling-5h meter passes ~15% of the allowance, move volume to the highest solo-coverage lanes (free twins first — zero normalized draw — then MiMo-Flash/DeepSeek). Never chase a 429 with retries — fail that lane over, not through (429-retried-3× is how overnight quotas die).
- **Unattended safety (nobody home to click `ask` — and `ask` ≈ `deny` when nobody is home):** hard-`deny` destructive bash (`rm -rf *`, pushes, deploys, infra mutations, `*PAT*`/`*--password*`); keep `doom_loop` guards on; iteration caps on every Ralph loop (`-n`, default 10) with `<promise>COMPLETE|BLOCKED|DECIDE</promise>` exit codes; fresh context per iteration + state on disk (`tasks.json`/`progress.txt` + git commit per task) so compaction loss can't erase the night's work; `aggressive_truncation` on; one watchdog cron that checks agent health/output recency and pages you (Discord/Slack webhook) instead of letting a wedged loop spin till morning.

### The three configs at a glance

| | A — HEAVY-MAX | B — VALUE-8H | C — ECO-24 |
|---|---|---|---|
| Primary (session model) | gemini-4-argon high ($30; escalation kimi-k3.1-pro max) | gemini-4-argon high ($30; escalation kimi-k3.1-pro max) | **glm-5.3-flash-free ($0)** |
| Reasoning slots | mimo-v2.6-pro max (AA 30) | mimo-v2.6-pro max (AA 30) | glm-5.3-flash max (AA 28) |
| Bulk/executor lane | mimo-v2.6-pro max | **free GLM/DS twins ($0)** | **free GLM/DS twins ($0)** |
| Review | glm-5.3 max | glm-5.3-flash high | glm-5.3-flash high |
| Consult | grok-4.7 xhigh (opt. Argon — shares primary budget) | mimo-v2.6-pro max | glm-5.3-flash max |
| Explore/quick/writing | DS max / haiku-max / glm-5.3 max | DS max / haiku-med / glm-flash low | mimo-flash low / DS med |
| Designed for | burst quality, 8h heavy days in ~2–4 day sprints | **8h intermittent heavy, every day** | **24/7 continuous, never binds** |
| Ration-tier burn | Argon + K3.1 Pro + mimo-pro + GLM-5.3 + Grok all rationed | Argon (~32/day) + K3.1 Pro (~9/day) + mimo-pro (~180/day) | $0 |
| Survives | ~2–4 heavy OMO days, then rations recover | every workday (rations reset daily) | indefinitely (free windows permitting) |

\* Spend = allowance consumed, not extra cash — all inside the $10 Go plan.

### Effort ladder for max quality (verified Oct 25 — use per slot as configured above)

| Model | Max-quality setting | Cost vs default | Critical flags |
|---|---|---|---|
| Kimi K3.1 Pro | `max` (low/high/max; always reasons) | AA 46; 191 req/mo measured (269 heavy) | 1M ctx, vision; 5.1.47 Sisyphus/Atlas prompts; temp 1.0; keep full reasoning history |
| Kimi K3 (fallback) | `max` (low/high/max only, always reasons) | unscored at max on v5.0.1 (17 @low only); ~1.74× cost vs low | temp 1.0, return full `reasoning_content` every turn, never switch model/effort mid-session |
| MiMo-V2.6-Pro | any level on (none=off; all others identical) | no max gain — keep max | temp/top_p forced 1.0; keep reasoning across tool turns |
| GLM-5.3 | `max` (default; thinking can't be disabled) | baseline | — |
| **Gemini 4 Argon** | `high` (upstream rung; AA shows no max effort — High/Medium only) | **AA 50 — Go ceiling; not trained BUT 55-day retained**; 862 req/mo measured | non-client work only without a contract check; slow (~57s median consult) |
| Grok 4.7 | `xhigh` | ~81K output tokens/task at xhigh | **mandatory `textVerbosity:low`**; never set presence/frequency penalty or stop (400s); >200K prompt doubles rates |
| Qwen3.8 Max | `xhigh` (default; high/max are aliases) | thinking billed as output, 262K budget | temp 1.0 / top_p 0.95 in thinking |
| DeepSeek V4.1 Flash | effort 100 (1–100; default high=75) | scales linearly-ish | evals use temp 1.0 / top_p 0.95 |
| Claude Haiku 5.5 | `max` → AA 36 (xhigh 35, high 30, **med 25 default**, low 19) | 440M-token verbosity at max | **omit temp/top_p/top_k entirely** (≠1/≠0.99 = 400); max only where AA 36 matters |
| Step 5 (paid) | `high` (= max; low/med/high) | $15/mo cap (4× promo ended) | medium is default; high for code; open weights available |

### Slot budget math: sustained 24/7 rate vs 8h daily budget (your profile)

Rule: **monthly ÷ 730h is the binding sustained rate** for every paid model (tighter than the 5h and weekly windows for continuous use). Daily budget = monthly ÷ 30.

| Model | $/req | 5h / wk / mo | Sustained/h (24/7) | 8h-day budget | Role in configs |
|---|---|---|---|---|---|
| GLM-5.3-Flash Free / DS V4.1 Flash Free | $0 | ∞ | ∞ | ∞ | **B/C free lanes (zero-retention)** |
| Beam Free | $0 | ∞ | ∞ | ∞ | free overflow (no training, 30-day) |
| Muse Spark 1.3* | $0.00090 | 13,287 / 33,219 / 66,437 | 91 | 2,215 | not assigned (trains on data) |
| MiMo-V2.6-Flash | $0.00126 | 9,491 / 23,728 / 47,455 | 65 | 1,582 | explore/librarian/quick volume |
| DeepSeek V4.1 Flash | $0.00210 | 9,524 / 23,810 / 47,619 | 65 | 1,587 | explore/looker, B/C day shift |
| LongCat-2.0 | $0.00296 | 4,053 / 10,133 / 20,266 | 28 | 675 | C overflow lane |
| Claude Haiku 5.5 (>100K) | $0.01679 | 179 / 447 / 893 | 1.2 | 30 | measured 170k-prompt mix bills this tier |
| Claude Haiku 5.5 (≤100K) | $0.00336 | 893 / 2,234 / 4,467 | 6.1 | 149 | quick (med AA 25; max AA 36) — the subagent-context option |
| Qwen3.8 Flash | $0.00507 | 1,182 / 2,956 / 5,911 | 8.1 | 197 | C overflow lane |
| GLM-5.3-Flash | $0.00688 | 1,744 / 4,359 / 8,718 | 12 | 291 | review/writing/C-reasoning |
| MiMo-V2.6-Pro | $0.00292 | 1,028 / 2,569 / 5,138 | 7.0 | 171 | A/B reasoning (shared) |
| Step 5 (paid) | $0.02549 | 118 / 294 / 588 | 0.81 | 20 | B/C paid quality step-up |
| Gemini 4 Argon | $0.03478 | 172 / 431 / 862 | 1.2 | 29 | **A/B primary (non-client; 55-day)** + hard consults |
| Kimi K3.1 Pro | $0.07867 | 38 / 96 / 191 | 0.26 | 6.4 | A/B escalation + plan-consultant (5.1.47 prompts) |
| Kimi K3 (fallback) | $0.09700 | 31 / 78 / 155 | 0.21 | 5.2 | primary fallback |
| GLM-5.3 | $0.06004 | 666 / 1,666 / 3,331 | 4.6 | 111 | A review/artistry (+B overflow — bulk lane now) |
| Qwen3.8 Max | $0.07391 | 41 / 102 / 203 | 0.28 | 6.8 | A visual verify |
| Grok 4.7 | $0.11111 | 27 / 68 / 135 | 0.18 | 4.5 | A consults |

ECO-24 lane total: ∞ + 65 + 65 + 28 + 12 + 8.1 + 6.1 ≈ **184 req/h sustained** of solo-usage lane capacity — against the **one shared allowance** (normalized per model limit), a 24/7 loop at 20–50 req/h spread across lanes keeps the normalized draw far below the 5h sub-limit and cannot exhaust the pool. VALUE-8H heavy day (≈10–20 Argon + 6–9 K3.1 Pro + 60–100 mimo-pro + 200–400 Flash-tier + ∞ free twins) fits inside every daily budget with margin.

### Avoid as OMO orchestrator/worker

- **Muse Spark Contributor / any training-on-data or free-weak route as primary or for client work** — trains-on-data terms (Contributor policy bans sensitive/confidential/personal data), time-limited free windows, regional limits. (**Gemini 4 Argon is a different bucket now** — Go documents it not trained but **55-day retained** (corrected Nov 18); it stays the Config A/B primary for non-client work, with K3.1 Pro as the privacy-safe pick.) Exception that proves the rule: the **free GLM-5.3-Flash / DeepSeek V4.1 Flash twins** (zero-retention, AA 28 / unmeasured on v5.0.1 — 33 via the 1017 ckpt) are the free models worth trying as primary — Config C, with the caveats above.
- **MiniMax M3/M2.7, Qwen3.7 Plus, Hy3, Kimi K2.7, MiMo-V2.5 (dropped from Go Nov 17) as orchestrator** — AA 19 or unmeasured on v5.0.1 (M3 = 19), no main-agent validation; fine only for `quick`/`explore`/`librarian` at low/off.
- **Grok 4.7, Qwen3.8 Max, Kimi K3.1 Pro/K3 as bulk workers** — 5h caps (27–41 vanilla 5h requests on the measured profile) die in one Ralph afternoon; cap their concurrency (`modelConcurrency`) and keep them on consult/review slots. (GLM-5.3 graduated from this list Nov 18 — 666/5h at the $200 cap.)
- **Weak-model orchestration generally** — long mechanics-driven prompts get ignored → bad delegation specs, nested-delegation loops, write-attempts by read-only agents → retry burn.

### Frontier escalation (one slot matters)

When Go fails (lost delegation, plan-reviewer never reaches APPROVE, architecture hallucinations), escalate **primary → ultrabrain → plan-reviewer, in that order**; leave the other ~80% of volume on Go. You already have GitHub Copilot access serving Claude/GPT lanes — pin only the primary there (e.g. `claude-opus-5-5`) while explore/librarian/quick stay on Go Flash. Zen pay-go is the alternative overflow.

### Cost-control knobs that actually work

`experimental.aggressive_truncation: true` + tool-output truncators (biggest saver) · `background_task` concurrency caps (`opencode-go: 10`, `kimi-k3.1-pro: 2`) · `maxDepth: 1` against nested delegation · `reasoning: low/off` for quick/explore/librarian/writing, `max` only for ultrabrain · `goal.enabled: false` unless Ralphing · `team_mode` OFF unless `mass` needed · disable `comment-checker` for bulk runs (never disable `team-tool-gating`, write/bash guards, `tool-pair-validator`) · watch the [console](https://opencode.ai/auth) weekly meter.

---

## 6. OpenCode v1 vs v2 compatibility matrix

**Nov 17 status:** OpenCode v2 dual-host support is **still not shipped**. PR [#9391](https://github.com/code-yeongyu/oh-my-openagent/pull/9391) (additive scaffold: V1 untouched, `./v2` entry, parity matrix as CI test) remains **open**, but the branch has grown since mid-October: the tools/hooks and agents slices are now on it and the parity matrix sits at **13 live / 13 todo rows**; an external real-engine parity harness (fazulfi/omo-v2-contrib + a community fork) reports 26/28 checks passing against OpenCode 2.2.7, with two known bridge defects (agent temperature not reaching the provider; prompt to a session without an explicit model). The tools/hooks slice [#9415](https://github.com/code-yeongyu/oh-my-openagent/pull/9415) is also still open. **This machine is on OpenCode v2.3.0 (v2.3.2 latest — upgrade pending)**, so the practical options today are: (a) OmO Native 5.1.75 (safe on v2), or (b) keep a v1 **1.19.6** install for OmO Ultimate.

| OMO | OpenCode v1 (`opencode.json` + `plugin`) | OpenCode v2 (`opencode.jsonc` + `plugins`) |
|---|---|---|
| 4.x legacy (`oh-my-opencode.json`, Sisyphus/Oracle/Librarian/Explore) | ✅ Supported (needs ≥1.0.132; installer wants ≥1.4.0) | ❌ Broken (`plugin` key, `prompt/permission/tools`, `scout`, TUI keys rejected) |
| 4.19.x (unified migration to `~/.omo/omo.jsonc`) | ✅ Supported, coexistence path | ⚠️ Partial — migration moves files; no native v2 plugin mapping shipped; needs 5.x build |
| 5.x (5.1.75, Nov 16) | ✅ Supported | ❌ Not shipped — dual-host scaffold in review (PR #9391 open; tools/hooks + agents slices on the branch, parity 13 live / 13 todo; PR #9415; ~17 documented API gaps) |
| **OmO Native 5.0+** (`omo-ai`, own engine) | ✅ Side-by-side (never touches OpenCode files; `omo setup` imports) | ✅ Independent — **the safe v2-era path** before Ultimate-v2 stabilizes |
| opensoft fork `dev` | ✅ Same as upstream | ⚠️ Same as upstream (no extra v2 layer); check fork releases |

Migration: `oh-my-openagent config migrate [--dry-run]`; `prompt`→`system`, `permission:{…}`→`permissions[]`, `variant/reasoningEffort`→`reasoning`, `plugin`→`plugins`, split `tui.json`, verify with `doctor --verbose`. Known v2 gaps if you port: LSP runtime intentionally missing, history migrator partial, programmatic MCP config-only, always-on background service.

---

## 7. opensoft fork vs official — which to choose

Fork ([opensoft/oh-my-opencode](https://github.com/opensoft/oh-my-opencode), ~1.2k★): battery-included curated defaults (Sisyphus Opus 4.5 High, Oracle GPT 5.2, Frontend Gemini 3 Pro, Librarian Sonnet, Explore Grok), async/background subagents first-class, published `sisyphus-prompt.md`, explicit OAuth/impersonation warnings. Choose the fork for frozen curated defaults + async-team emphasis. Choose official for OmO Native 5.x, `mass ulw` graphs, Kibitzer memory, unified config, migration support, Codex Light edition.

---

## 8. Community + tokenmaxxing notes

Embedded reception is strong (Cursor cancellations, 8k eslint warnings in a day, 45k-line overnight rewrites via Ralph). Documented complaints: token burn, complexity, Claude-dependence (weak without Claude-class orchestrator — which is exactly why the Kimi K3.1 Pro rung matters on Go), Anthropic blocking OpenCode API traffic attributed to OMO (prefer API keys/Zen/Go/Kimi/GLM over OAuth subscription tricks), Windows proxy/PATH friction. Tokenmaxxing doctrine: `ulw` over full `ultrawork`; `resume=session_id` over new tasks; `background_cancel(all=true)` before final answers; stop after 2 fruitless iterations; `lsp_diagnostics` per unit + project-level verify, never trust subagent claims; concurrency caps (Opus-class 2–3, cheap providers 10–20); cheap models for explore/librarian/quick.

---

**Next:** [09 — v1 vs v2](./09-opencode-v1-vs-v2.md) · [10 — Plugins & Stacks](./10-plugins-and-stacks.md) · [11 — Amazing Additions](./11-amazing-additions.md)
