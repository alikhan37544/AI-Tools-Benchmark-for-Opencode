# 08 — Oh My OpenCode (now oh-my-openagent / OmO): The Complete Guide + Go Model Map for Heavy Work

> **Snapshot: October 1, 2026.** Primary sources: [code-yeongyu/oh-my-openagent](https://github.com/code-yeongyu/oh-my-openagent) (69.7k★), [omo.dev/docs](https://omo.dev/docs), [opensoft/oh-my-opencode](https://github.com/opensoft/oh-my-opencode) fork, [opencode.ai/docs](https://opencode.ai/docs/) + [opencode.ai/v2/docs](https://opencode.ai/v2/docs/).
> **Naming (important):** the project renamed to **oh-my-openagent (OmO)**. The npm package is still `oh-my-opencode` (dual-published); install with `bunx oh-my-openagent install`. Do NOT `bunx omo` — unrelated package by a different author. Config files accept both `oh-my-openagent.json[c]` and legacy `oh-my-opencode.json[c]`.

---

## 1. What it is: three editions

| Edition | Host | What you get | Install |
|---|---|---|---|
| **Ultimate (omo for OpenCode)** | OpenCode v1 | Full harness: 11 agents, 52+ lifecycle hooks, 26 tools, slash commands, Team Mode, ulw/Ralph loops, hashline edits, built-in MCPs | `bunx oh-my-openagent install` (TUI walks you through providers) |
| **Light (omo for Codex CLI)** | Codex CLI | Portable pieces: rules, comment-checker, git-bash, LSP, ultrawork, ulw-loop, telemetry — no agent orchestration | `npx lazycodex-ai install` |
| **OmO Native (`omo-ai`)** | Standalone (`senpi` engine) | OMO built in, no OpenCode host needed; `omo setup` imports providers/MCPs/skills | `curl -fsSL https://get.omo.dev/install.sh \| bash`, then `omo` |

Non-interactive install: `bunx oh-my-openagent install --no-tui --platform=opencode …`. Requires OpenCode ≥1.4.0. Verify with `bunx oh-my-openagent doctor --verbose`.

Config locations (4.x legacy): project `.opencode/oh-my-opencode.json` > user `~/.config/opencode/oh-my-opencode.json`. New unified (5.x): `~/.omo/omo.jsonc` + `.omo/omo.jsonc`, with `[opencode]` / `[native]` / `[codex]` blocks and `profiles.<name>` layers. A migration engine imports legacy configs once (`oh-my-openagent config migrate --dry-run`).

---

## 2. The agents (who does what)

| Agent | Role | Default model thinking |
|---|---|---|
| **Sisyphus** | Main orchestrator. Plans with todos, delegates to specialists, verifies, never stops halfway. Prompt built against Claude-style instruction following; thinking budget 32k, maxTokens 64k | Claude Opus chain → **Kimi K2.6/K3** → GLM fallback |
| **Sisyphus-Junior** | Worker executor (cannot delegate; mid-tier model is fine — intelligence lives in the prompt) | Sonnet-class |
| **Atlas** | Execution conductor: reads plan, accumulates wisdom in `.sisyphus/notepads/<plan>/`, verifies independently. Used with `/start-work`, never alone | Opus/Sonnet-class |
| **Prometheus (+ Metis/Momus → plan-consultant/plan-reviewer in 5.x)** | Strategic planner (interview mode, Tab or `@plan`), gap analysis, ruthless plan review with resubmit loop | Opus-class; reviewer often GPT Astra-class |
| **Oracle → `architect` category** | Read-only high-IQ consultant: architecture, debugging after 2+ failures, security/perf review. Cannot write/edit | GPT/Opus-class |
| **Librarian** | Reference grep: official docs (Context7), OSS examples (grep.app/GitHub), evidence-based. Cannot write | Cheap (Big Pickle / GLM / Luna-fast class) |
| **Explore** | Blazing-fast codebase grep. Cannot write | Cheapest/fastest (Nano / Haiku / Grok-class) |
| **Multimodal-Looker** | Visual specialist: PDFs/images/diagrams → text (saves main-context tokens) | Gemini-flash class |
| **Frontend UI/UX Engineer** | Frontend persona (bold direction, anti-slop). In current docs: `visual-engineering` category + `frontend` skill | Gemini 3 Pro / Fable-class |

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

---

## 4. The machinery: hooks, tools, Team Mode, loops

- **52+ lifecycle hooks:** IntentGate keyword detection (`ultrawork|ulw`, `team-mode`, `hyperplan`), **todo-continuation-enforcer** (forces the agent back when todos are incomplete), **comment-checker** (strips AI slop), think-mode, context injection (AGENTS.md/README/rules), output truncation (tool/grep truncators, aggressive truncation experimental), compaction preservation, session recovery, model/runtime fallbacks, background notifications, telemetry (anonymous PostHog, off via `OMO_SEND_ANONYMOUS_TELEMETRY=0`). Disable via `disabled_hooks`.
- **26 tools:** full LSP suite (diagnostics/rename/goto/references/symbols), AST-grep (25 langs), `call_omo_agent` / `delegate_task` / `background_output` / `background_cancel`, session tools (list/read/search), hash-anchored `LINE#ID` edits, skill/MCP loaders, 12 `team_*` tools.
- **Team Mode (OFF by default):** lead + up to 8 members, shared mailbox + task list, optional tmux grid, `teams.<name>` (8 members / 4 parallel / 120 min), DAG up to 64 nodes (`mass ulw`).
- **Loops:** `ultrawork|ulw` (explore→research→implement→diagnostics→done), `/ralph-loop` (until `<promise>DONE</promise>`, default 100 iters), `/ulw-loop` (ralph+ultrawork), `/cancel-ralph`, `/goal`.
- **Skills/commands/MCPs:** `playwright` (browser), `git-master` (atomic commits), `frontend`, `lsp`, `ultrawork`, `team-mode`, `review-work`, `debugging`, `security-review`, `visual-qa`; `/init-deep`, `/refactor`, `/handoff`, `/hyperplan`; built-in MCPs `websearch` (Exa), `context7`, `grep_app` (+ skill-scoped `playwright`, `git_bash`, `lsp`). Full Claude Code compat layer (commands/agents/skills/MCPs/hooks).

---

## 5. Go model map for VERY heavy work (the money section)

OMO multiplies volume: one `ultrawork` fans out to main + researchers + workers + verifier + retries — **plan for 3–5× requests vs single-agent, 6–12× for `mass ulw` / Team Mode / Ralph loops**. Divide every allowance below by ~4 for OMO-week planning. Numbers use your calibrated profile (7.8k in / 1.1k out / 146k cache per request); docs estimates are ~3–7× lighter (see `04`).

**Rule 0:** the orchestrator (Sisyphus primary) is the ONE slot where intelligence matters most. Upstream validates **Kimi K3 (max)** as the Go main-agent rung — nothing else on Go is documented as a supported primary. Everything else is negotiable.

| OMO slot | Best Go pick | Reasoning | Allowance math |
|---|---|---|---|
| **sisyphus primary** | **kimi-k3, max** | Only Go main-agent rung (Claude-like); AA 44 | $15 tier: 90/wk, 179/mo (you) → **~22 OMO-req/wk**. Ration it: primary does planning/delegation, not bulk reads |
| **ultrabrain / deep-high / unspecified-low** | **mimo-v2.6-pro, max** | AA 46 (top verified Go); matches upstream 2nd rung | $15 tier: 1,537/wk, 3,074/mo (you) → **~380 OMO-req/wk** |
| **unspecified-high / artistry / deep executor** | **glm-5.3, max** | AA 45, Claude-like; upstream 2nd/3rd rung | $15 tier: 140/wk, 279/mo (you) → **~35 OMO-req/wk**. Use sparingly |
| **oracle / architect consults** | **grok-4.7, xhigh** (fallback mimo-v2.6-pro) | AA 46; upstream rung; consults are low-volume | 79/wk, 158/mo (you) → **~20 OMO consults/wk** |
| **plan-reviewer** | **glm-5.3, max** (bulk alt: glm-5.3-flash high) | Review needs teeth; flash variant for volume | same as above / 4,918/wk (you) for flash |
| **plan-consultant (Metis)** | **kimi-k3, max** | Upstream 3rd rung; gap analysis needs Claude-like | shares primary's 90/wk budget — keep consults tight |
| **librarian** | **mimo-v2.6-flash, low** (fallback deepseek-v4.1-flash max) | Docs/OSS grep needs AA ~38, not 46 | 16,586/wk, 33,171/mo (you) → **~4,100 OMO-req/wk** |
| **explore** | **deepseek-v4.1-flash, max** (fallback mimo-v2.6-flash low) | Upstream has deepseek-flash rung; AA 39 | 9,558/wk, 19,117/mo (you) → **~2,400 OMO-req/wk** |
| **visual-engineering** | **kimi-k3, max** (bulk CSS: glm-5.3-flash) | Upstream visual chain ends at kimi-k3 | ration; flash does 4,918/wk (you) |
| **multimodal-looker** | **deepseek-v4-flash-vision-exp** | Only Go vision-billed route | 2,362/wk, 4,724/mo (you) → **~600 OMO-req/wk** |
| **quick** | **mimo-v2.6-flash, low** | Upstream quick tail; cheapest correct | ~4,100 OMO-req/wk |
| **writing** | **glm-5.3-flash, low** | AA 42 prose at volume (avoid Contributor for client docs — trains on data) | 4,918/wk (you) |
| **deep-low bulk research** | **qwen3.7-plus, medium** (alt: glm-5.3-flash) | $60 tier volume for evidence-settleable research | 2,799/wk (you) |

### Config A — max intelligence (survives ~2–4 heavy OMO days)

```jsonc
{ // ~/.config/opencode/oh-my-openagent.jsonc  (legacy base; 5.x: ~/.omo/omo.jsonc [opencode])
  "$schema": "https://raw.githubusercontent.com/code-yeongyu/oh-my-openagent/dev/assets/omo.schema.json",
  "[opencode]": {
    "agents": {
      "explore": { "model": "opencode-go/deepseek-v4.1-flash", "reasoning": "max" },
      "librarian": { "model": "opencode-go/mimo-v2.6-flash", "reasoning": "low" },
      "plan-consultant": { "model": "opencode-go/kimi-k3", "reasoning": "max" },
      "plan-reviewer": { "model": "opencode-go/glm-5.3", "reasoning": "max" }
    },
    "categories": {
      "visual-engineering": { "model": "opencode-go/kimi-k3", "reasoning": "max" },
      "ultrabrain": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "deep-low": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "deep-high": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "artistry": { "model": "opencode-go/glm-5.3", "reasoning": "max" },
      "quick": { "model": "opencode-go/mimo-v2.6-flash", "reasoning": "low" },
      "unspecified-low": { "model": "opencode-go/mimo-v2.6-pro", "reasoning": "max" },
      "unspecified-high": { "model": "opencode-go/glm-5.3", "reasoning": "max" },
      "writing": { "model": "opencode-go/qwen3.8-max", "reasoning": "max" },
      "architect": { "model": "opencode-go/grok-4.7", "reasoning": "xhigh" }
    }
  }
}
// Main session model: opencode-go/kimi-k3. Look_at vision: opencode-go/deepseek-v4-flash-vision-exp.
```

### Config B — sustainable heavy daily driver (survives full workweeks except primary)

Same as A, except: `plan-reviewer` → `glm-5.3-flash` high; `deep-low` → `qwen3.7-plus` medium; `artistry` → `glm-5.3-flash` max; `writing` → `glm-5.3-flash` low; `architect` → `mimo-v2.6-pro` max; `unspecified-high` → `mimo-v2.6-pro` max; plus:

```jsonc
"background_task": { "defaultConcurrency": 5,
  "providerConcurrency": { "opencode-go": 10 },
  "modelConcurrency": { "opencode-go/kimi-k3": 2 } },
"experimental": { "aggressive_truncation": true },
"disabled_hooks": ["comment-checker"],
"telemetry": { "enabled": false }
```

Tradeoff: ~(a) is ~0.5–1 AA smarter on artistry/writing/review but 15–30× fewer weekly requests on those slots. (b) keeps top AA (46) where it matters — orchestrator-adjacent reasoning — and pushes 80% of volume to $60/$30-tier models.

### Avoid as OMO orchestrator/worker

- **Muse Spark Contributor / any free model as primary or for client work** — trains-on-data terms (§6: Contributor policy bans sensitive/confidential/personal data), time-limited free windows, regional limits.
- **MiniMax M3/M2.7, Qwen3.7 Plus, Hy3, Kimi K2.6/K2.7, MiMo-V2.5 as orchestrator** — AA 23–29, no main-agent validation; fine only for `quick`/`explore`/`librarian` at low/off.
- **Grok 4.6/4.7, Qwen3.8 Max, Kimi K3, GLM-5.3 as bulk workers** — 5h caps (32–220 vanilla req) die in one Ralph afternoon; cap their concurrency (`modelConcurrency`) and keep them on consult/review slots.
- **Weak-model orchestration generally** — long mechanics-driven prompts get ignored → bad delegation specs, nested-delegation loops, write-attempts by read-only agents → retry burn.

### Frontier escalation (one slot matters)

When Go fails (lost delegation, plan-reviewer never reaches APPROVE, architecture hallucinations), escalate **primary → ultrabrain → plan-reviewer, in that order**; leave the other ~80% of volume on Go. You already have GitHub Copilot access serving Claude/GPT lanes — pin only the primary there (e.g. `claude-opus-5-5`) while explore/librarian/quick stay on Go Flash. Zen pay-go is the alternative overflow.

### Cost-control knobs that actually work

`experimental.aggressive_truncation: true` + tool-output truncators (biggest saver) · `background_task` concurrency caps (`opencode-go: 10`, `kimi-k3: 2`) · `maxDepth: 1` against nested delegation · `reasoning: low/off` for quick/explore/librarian/writing, `max` only for ultrabrain · `goal.enabled: false` unless Ralphing · `team_mode` OFF unless `mass` needed · disable `comment-checker` for bulk runs (never disable `team-tool-gating`, write/bash guards, `tool-pair-validator`) · watch the [console](https://opencode.ai/auth) weekly meter.

---

## 6. OpenCode v1 vs v2 compatibility matrix

| OMO | OpenCode v1 (`opencode.json` + `plugin`) | OpenCode v2 (`opencode.jsonc` + `plugins`) |
|---|---|---|
| 4.x legacy (`oh-my-opencode.json`, Sisyphus/Oracle/Librarian/Explore) | ✅ Supported (needs ≥1.0.132; installer wants ≥1.4.0) | ❌ Broken (`plugin` key, `prompt/permission/tools`, `scout`, TUI keys rejected) |
| 4.19.x (unified migration to `~/.omo/omo.jsonc`) | ✅ Supported, coexistence path | ⚠️ Partial — migration moves files; no native v2 plugin mapping shipped; needs 5.x build |
| 5.x beta (unified `omo.jsonc`, canonical `reasoning`) | ✅ Supported | ⚠️ Requires v2-compatible plugin build; pin versions, test hooks/`permissions[]`/`#variant`; official v2-support note still in progress |
| **OmO Native 5.0+** (`omo-ai`, own engine) | ✅ Side-by-side (never touches OpenCode files; `omo setup` imports) | ✅ Independent — **the safe v2-era path** before Ultimate-v2 stabilizes |
| opensoft fork `dev` | ✅ Same as upstream | ⚠️ Same as upstream (no extra v2 layer); check fork releases |

Migration: `oh-my-openagent config migrate [--dry-run]`; `prompt`→`system`, `permission:{…}`→`permissions[]`, `variant/reasoningEffort`→`reasoning`, `plugin`→`plugins`, split `tui.json`, verify with `doctor --verbose`. Known v2 gaps if you port: LSP runtime dead, share unimplemented, programmatic MCP config-only, always-on background service.

---

## 7. opensoft fork vs official — which to choose

Fork ([opensoft/oh-my-opencode](https://github.com/opensoft/oh-my-opencode), ~1.2k★): battery-included curated defaults (Sisyphus Opus 4.5 High, Oracle GPT 5.2, Frontend Gemini 3 Pro, Librarian Sonnet, Explore Grok), async/background subagents first-class, published `sisyphus-prompt.md`, explicit OAuth/impersonation warnings. Choose the fork for frozen curated defaults + async-team emphasis. Choose official for OmO Native 5.x, `mass ulw` graphs, Kibitzer memory, unified config, migration support, Codex Light edition.

---

## 8. Community + tokenmaxxing notes

Embedded reception is strong (Cursor cancellations, 8k eslint warnings in a day, 45k-line overnight rewrites via Ralph). Documented complaints: token burn, complexity, Claude-dependence (weak without Claude-class orchestrator — which is exactly why Kimi K3 matters on Go), Anthropic blocking OpenCode API traffic attributed to OMO (prefer API keys/Zen/Go/Kimi/GLM over OAuth subscription tricks), Windows proxy/PATH friction. Tokenmaxxing doctrine: `ulw` over full `ultrawork`; `resume=session_id` over new tasks; `background_cancel(all=true)` before final answers; stop after 2 fruitless iterations; `lsp_diagnostics` per unit + project-level verify, never trust subagent claims; concurrency caps (Opus-class 2–3, cheap providers 10–20); cheap models for explore/librarian/quick.

---

**Next:** [09 — v1 vs v2](./09-opencode-v1-vs-v2.md) · [10 — Plugins & Stacks](./10-plugins-and-stacks.md) · [11 — Amazing Additions](./11-amazing-additions.md)
