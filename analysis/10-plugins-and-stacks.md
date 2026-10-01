# 10 — Best Plugins, MCPs, Skills & Daily-Life Tooling

> **Snapshot: October 1, 2026.** Sources: [opencode.ai/docs/ecosystem](https://opencode.ai/docs/ecosystem/) (official, PR-welcome), [awesome-opencode](https://github.com/awesome-opencode/awesome-opencode) (10.4k★), [opencode.im](https://opencode.im/) (community hub, JS-rendered), Reddit r/opencodeCLI setup threads, plugin repos.
> You are on **v1** (`@opencode-ai/plugin` 1.18.1). V1 snippets below; v2 deltas noted (`plugin`→`plugins`, `mcp.{name}`→`mcp.servers.{name}`, `enabled:false`→`disabled:true`, snake_case OAuth, `opencode mcp add/list/auth`).

---

## 1. How plugins work (30 seconds)

```jsonc
// opencode.json (v1)
{ "$schema": "https://opencode.ai/config.json",
  "plugin": ["oh-my-opencode", "opencode-dynamic-context-pruning", "opencode-notify"] }
```

npm plugins auto-install via Bun (cached in `~/.cache/opencode/node_modules/`); local files load from `.opencode/plugins/` (project) and `~/.config/opencode/plugins/` (global); load order global → project. A plugin can add tools, hooks (`tool.execute.before/after`, `chat.*`, `permission.ask`, `session.idle`, …), agents, commands, skills and MCPs. **V2 requires `Plugin.define({id,setup(ctx)})` — v1 plugins do not run there.**

---

## 2. Most-mentioned plugins (community-verified)

| Plugin | What it does | Why it's loved |
|---|---|---|
| **oh-my-opencode / -slim** | Mega-harness: Sisyphus/Oracle/Explore/Librarian agents, LSP/AST tools, session tools, built-in Exa/Context7/grep_app MCPs. Slim = fewer tokens | The single biggest capability jump; see `08` |
| **opencode-antigravity-auth** (+ multi-auth fork) | Google Antigravity OAuth → free Gemini/Claude quota, multi-account rotation | Free frontier quota… with ToS/ban risk (see §6) |
| **opencode-openai-codex-auth / gemini-auth** | Route ChatGPT Plus/Pro or Gemini plan instead of API credits | Cheaper frontier overflow |
| **opencode-dynamic-context-pruning** | Prunes obsolete tool outputs (LLM-decided compact) | Noticeably longer effective sessions; test per model (weak models dislike it) |
| **opencode-notify / notificator** | Native OS notifications + sounds on idle/permission/error | Essential for long Ralph loops (note: one is archived Sep 2026, v1-only — use native v2 sounds there) |
| **opencode-wakatime** | WakaTime AI-coding metrics | Know where your 12,973 requests actually went |
| **opencode-quotas / mystatus** | Footer quota dashboards + predictions (Antigravity/Codex/Copilot) | Avoid surprise walls |
| **cc-safety-net / vibeguard / envsitter-guard** | Block destructive git/fs; block `.env` reads (fingerprints only); redact secrets/PII | PHI-safe agent operation — see `11` |
| **opencode-worktree / multiplexer / background-agents / history-search** | Zero-friction worktrees; 16-in-1 orchestration; async delegation; fast session switching | Parallel repos without chaos |
| **openspec / plannotator / conductor / ralph-rlm** | Spec-driven dev; plan-review UI with annotations | Fewer "wrong direction" marathons |
| **opencode-morph-fast-apply** | 10k+ tok/s edits via Morph API | Burns far fewer output tokens = saves limits |
| **opencode-tavily / supermemory / honcho** | Search CLI; persistent memory (Supermemory/Honcho) | Memory that survives compaction |
| **opencode-scheduler / devcontainers / direnv / skillful** | cron jobs; multi-branch containers; env; lazy skill loader | Nightly autonomous checks — see `11` |

Reddit consensus pattern: `oh-my-opencode-slim + context7 + history-search + multiplexer`, and a growing "fewer MCPs, more CLIs+skills" minimalism to save tokens.

---

## 3. MCP servers that matter (ranked)

Official warning, twice: *"MCP servers add to your context… add only the servers you need."* Sweet spot is **3–6 servers**; past ~10, tool choice degrades. OMO already ships Exa/Context7/grep_app + Playwright/LSP skills — **don't duplicate those**.

| MCP | Why | Install (v1) | Cost / notes |
|---|---|---|---|
| **Context7** | Version-aware library docs; kills hallucinated APIs. 2 tools, tiny footprint | remote `https://mcp.context7.com/mcp` (+ `CONTEXT7_API_KEY` for limits) | Free. Most-recommended docs MCP |
| **Playwright** | Real browser: navigate/click/fill/screenshot/PDF/video/tracing | local `npx @playwright/mcp@latest` (`--isolated`, opt-in `pdf,devtools` caps) | Free/local. Prefer the **CLI+skill** for bulk work (token-cheaper) — see `11` |
| **Exa *or* Tavily (pick one)** | Semantic web search/fetch | remote `https://mcp.exa.ai/mcp` / `https://mcp.tavily.com/mcp` | Freemium keys. Never two search MCPs |
| **Grep.app (`gh_grep`)** | Code examples across public GitHub; cheap | remote `https://mcp.grep.app` | Free, low token |
| **GitHub (official)** | Issues/PRs/search/Actions | remote `https://api.githubcopilot.com/mcp/` + PAT, or local Docker | **Token hog** — filter via `X-MCP-Toolsets` |
| **Sequential-thinking / memory** | Stepwise reasoning; cross-session memory (`mem0`, `server-memory`, Supermemory, Honcho) | `npx -y @modelcontextprotocol/server-sequential-thinking` etc. | Local/free except hosted memory tiers. Cloud memory = never for PHI |
| **Postgres/MySQL/SQLite/filesystem/fetch** | Read-only DB inspection; scoped files; URL fetch | `npx -y @modelcontextprotocol/server-postgres <conn>` / `server-filesystem <dirs>` | Free. **Read-only DB user + per-agent scoping** |
| **Docker/K8s/cloud CLIs** | Prefer CLIs over MCPs (cheaper): `az`, `kubectl`, `docker` via bash + a SKILL.md | No MCP — skill wrapper | Cloud costs only. "Context7, Tavily, cloud provider CLI. Superpowers." |
| **Azure DevOps** | Pipelines/Repos/PRs/artifacts/WI (your CI!) | local `npx -y @azure-devops/mcp <org>` (`--authentication azcli`) or remote `https://mcp.dev.azure.com/{org}` | PAT/Entra. Full recipes in `11` |
| **Sentry / Linear / Jira / Slack** | Triage stack traces; project state in/out | remote per docs (`https://mcp.sentry.dev/mcp`, `https://mcp.linear.app/sse`) | OAuth/PAT, scope narrowly |
| **LSP / ast-grep** | Prefer **OMO built-in** LSP/AST tools over a separate MCP | OMO plugin | Free/local |

Per-agent scoping pattern: global `"tools": {"gh_*": false}`, enable per agent (`investigate: tools: {postgres_ro_*, context7_*: true}`).

---

## 4. Skills, rules, UX polish

- **Skills** (`SKILL.md` + frontmatter `name/description`): discovered at `.opencode/skills/`, `~/.config/opencode/skills/`, `.claude/skills/`; loaded on demand via `skill` tool; per-agent permission. Your highest-ROI custom skills: `azure-devops` (build triage), `browser-ops` (Playwright CLI), `ari-telephony`, `kafka-ops`, `doc-intel` — all with copy-paste starters in `11`.
- **Rules**: `AGENTS.md` (project + global `~/.config/opencode/AGENTS.md`), `/init` generator, `instructions:["AGENTS.md","docs/*.md"]` globs. **Commit per-project AGENTS.md** (you already do in 6 repos — extend to all).
- **UX wins**: themes ([docs/themes](https://opencode.ai/docs/themes/)), keybinds, formatters, `autotitle/smart-title/zellij-namer`, `md-table-formatter`. Small, but daily.
- **IDE/ACP/remote**: run `opencode` in VS Code/Cursor/Windsurf terminal for auto-extension (`EDITOR="code --wait"`); ACP backends (`opencode acp` + VSCode ACP/VSACP clients); rich bridges (opencode-to-vscode-bridge 71 tools); Neovim/Obsidian; remote via `opencode serve` + Tailscale/VPN, SSH+tmux/zellij, CodeNomad mobile.

---

## 5. Three copy-paste stacks

**(a) Backend-heavy TS/Python** — OMO (+slim) + DCP + notify + safety-net; MCPs: context7, gh_grep, read-only postgres; `instructions: ["AGENTS.md"]`.

**(b) Browser / visual QA** — OMO-slim + notify; MCPs: playwright (scoped to an `rpa-healer` agent), context7. Live MCP for healing/exploration, CLI+scripts+POM for the 578-check suite. Full doctrine in `11`.

**(c) Docs-heavy integration** — skillful + handoff; MCPs: context7, exa (or tavily), sentry (`opencode mcp auth sentry`).

**Azure DevOps users:** local ADO MCP with `--authentication azcli` (reuses your `az login` — the trick you already love) + the `azure-devops` skill; remote `https://mcp.dev.azure.com/{org}` for Entra teams. v2: `mcp.servers.ado`, `disabled`, snake_case OAuth. Full config + recipes in `11`.

---

## 6. Anti-recommendations (what to avoid)

| Avoid | Why |
|---|---|
| **MCP/tool bloat (>6–10 servers)** | Context tax, worse tool choice, faster limit burn. Start 0–3, add on repeated manual paste |
| **Two search MCPs / two LSP providers / OMO + other hook plugins** | Conflicting overrides, double hooks, duplicate edit tools. Use `disabled_skills`/`disabledMcps` to dedupe |
| **Antigravity/Codex OAuth proxy plugins** | ToS violations, ban/shadow-ban reports. Isolate credentials, expect breakage |
| **Abandoned v1-only plugins on v2** | Silent `SchemaError`/load fails. Check `plugin list`, logs, migration guide first |
| **DCP + very weak models** | Pruning confuses some models; test per model |
| **Unvetted plugins with `tool.execute.before` + `shell.env` + network** | No official blocklist exists — pin versions, audit hooks, check stars/commits |
| **Unscoped GitHub MCP** | Token hog; always filter toolsets |

Measure before pruning: `opencode mcp list/debug`, token tracking, and per-agent tool scoping.

---

**Next:** [08 — Oh My OpenCode](./08-oh-my-opencode.md) · [09 — v1 vs v2](./09-opencode-v1-vs-v2.md) · [11 — Amazing Additions](./11-amazing-additions.md)
