# 09 — OpenCode v1 vs v2: Differences, Advantages, Disadvantages (+ OMO on Each)

> **Snapshot: October 1, 2026.** Sources: [opencode.ai/docs](https://opencode.ai/docs/) (v1), [opencode.ai/v2/docs](https://opencode.ai/v2/docs/) (v2), [opencode.ai/v2/docs/migrate-v1](https://opencode.ai/v2/docs/migrate-v1/) (migration bible), [changelog](https://opencode.ai/changelog), GitHub issues, Reddit r/opencode/r/opencodeCLI.
> Versions seen: v1 `1.18.34` (Sep 30, 2026, still maintained); v2 `2.0.x` stable (`2.0.16` era) after a July–Sep beta.

---

## 1. What v2 actually is

A **rewrite with a new architecture**, not a feature bump: one shared Hono/SQLite background server backing TUI + Desktop + Web + Docker + SDK clients (v1 was a standalone TUI + `opencode serve`). Drivers: Bun→Node migration (memory bloat fixes), Tauri→Electron desktop (consistent Chromium rendering), redesigned server API + generated clients.

Install channels (separate — **do not mix**):

| | v1 | v2 |
|---|---|---|
| curl | `https://opencode.ai/install` | `https://opencode.ai/v2/install` |
| npm | `npm i -g opencode-ai` | `npm i -g @opencode/cli` |
| brew | `anomalyco/tap/opencode` | `anomalyco/tap/opencode-v2` |

Beta ran side-by-side (`opencode` + `opencode2`); stable v2 **replaces** the `opencode` binary — remove package-managed v1 first, and never point v1 at v2-converted config files (same paths!).

---

## 2. Feature comparison

| Area | v1 | v2 |
|---|---|---|
| Runtime | TUI owns sessions; `opencode serve` for sharing | Shared background service owns sessions/config/integrations (`--standalone` / `--server` overrides; `opencode service …`) |
| Clients | TUI + CLI + `opencode web` | TUI + Desktop + Web + Docker + generated SDK clients, synced by default; `opencode mini`, `opencode pair` |
| Tabs/sessions | Single-session TUI | Multi-tab parallel sessions, per-tab models, foreground/background child-session manager |
| Plugins | `plugin: […]`, `(input)=>{tool,event,…}` with Bun `$` helper | **`plugins: […]` + `Plugin.define({id,setup(ctx)})` — V1 plugins DO NOT run; must be reimplemented** |
| Agents | `agent:{prompt,model,variant,permission,tools,…}`, `scout` exists | `agents:{system,model:"provider/model#variant",permissions[],steps,…}`; `scout` removed; `.opencode/agents/*.md` preferred |
| Permissions | `permission:{bash/edit: allow/ask}`, `tools:{…:false}` | Ordered `permissions[]` (last-match-wins), `bash→shell`, `task→subagent`; Console-managed policies incl. hard-deny |
| MCP | `mcp:{name:{type,command,enabled,timeout}}` | `mcp:{servers:{name:{…disabled,timeout:{catalog,execution}}}}`; snake_case OAuth; `codemode`; config-only (no programmatic registration) |
| Config | `opencode.json` + layered `tui.json` | `opencode.jsonc` + single global `cli.json` (`OPENCODE_CLI_CONFIG`); v1.18.24+ reads supported v2 fields |
| Skills | `skills:{paths[],urls[]}` | `skills:["./team-skills","https://…"]` ordered array; `.opencode/skill/` compat |
| Rules/refs | `instructions[]`, `reference{}` | `references{}` (plural), `reference` deprecated; `instructions[]` accepted but prefer `AGENTS.md` |
| Commands | `command:{…}` in `command/` | `commands:{…}` in `commands/`, delegated runs auto-background |
| Providers/auth | `auth.json` file; `/connect`; custom `{npm,api,options}`; Zen `opencode/<id>`, Go `opencode-go/<id>` | Credentials move to **SQLite** (imports `auth.json` once, never writes back); `opencode auth login/list/switch/logout`; custom `{package,settings,headers/body,env[]}`; same Zen/Go IDs/endpoints |
| LSP | Full runtime + diagnostics in tool results | **Accepted but inert: no LSP runtime, no diagnostics** — use lint/typecheck |
| Share | `share: manual/auto/disabled`, `/share` | Accepted but **not supported yet** |
| Compaction | `{auto,prune,reserved}` + `tail_turns` | `{auto,keep:{tokens},buffer}` + checkpoints; old keys ignored with warning |
| Sessions/history | `session/message/part` SQLite | `session_v2/…`; **V1 history not visible initially**, migrator tracked separately (corrupt-row 500s reported) |
| IDE/ACP/GitHub/GitLab/Data pages | Dedicated v1 pages | Partially missing as dedicated pages (IDE/ACP/GitHub/GitLab/Data) — verify before relying |
| Models | `model#variant`, `small_model`, `variants{}`, `temperature/top_p` top-level | `model: provider/model#variant`, `variants[{id,settings}]`; legacy agent fields warn; per-model request `headers/body` |

---

## 3. v1 → v2 migration checklist

1. **Backup everything**: `opencode.json(c)`, `auth.json`, `~/.local/share/opencode/` (the 39 GB DB!), custom `plugins/`, `skills/`, `commands/`.
2. **Remove package-managed v1** before installing v2 (same binary name now).
3. Get models/creds/agents/permissions/MCP working **before** porting plugins or API clients.
4. `autoshare:true` → `share:"auto"`; `permission:{bash:{…}}` → `permissions:[…]`; `agent:{x:{prompt,…}}` → `agents:{x:{system,…}}`; `plugin:[…]` → `plugins:[…]` (**plus reimplementation** — rename alone fails); `mcp:{name}` → `mcp:{servers:{name}}`, `enabled:false` → `disabled:true`, `clientId` → `client_id`; `command/` → `commands/`; `reference` → `references`; `snapshot:false` → `snapshots:false`; `compaction:{…reserved}` → `{keep:{tokens},buffer}`; provider `npm/api/options.apiKey` → `package/settings` (+`headers/body/env[]`); model `id/tool_call` → `modelID/capabilities`; `small_model` → `agents.title.model`; local plugin dir `.opencode/plugin/` → `.opencode/plugins/`.
5. Ask OpenCode itself to convert (`Migrate my OpenCode configuration… preserve behavior`), then verify with `opencode debug paths` + a smoke session.
6. Re-auth providers (credentials move to SQLite); re-`connect` Zen/Go; confirm Go uses `zen/go/v1/…` endpoints with `opencode-go/<id>` (a Go key on `zen/v1/…` 401s).

Full field-by-field reference: [migrate-v1](https://opencode.ai/v2/docs/migrate-v1/).

---

## 4. Advantages of v2 (why upgrade)

- One backend, three interfaces, sessions synced everywhere (TUI/Desktop/Web/Docker) with less per-window resource use.
- Memory-bloat fixes (Node) + consistent rendering (Electron).
- Multi-tab parallel sessions with per-tab models + a real foreground/background child-session manager — the single biggest workflow upgrade for heavy users.
- Cleaner config ergonomics (ordered permissions, `providers/settings`, `keep/buffer`) while v1 config still loads.
- Better server API + generated clients + embedded SDK + plugin RPC/service discovery for automation builders.
- Anecdotal cache-hit improvements (unverified — treat as claim, not fact).

## 5. Disadvantages / risks of v2 (why wait)

- **Three intentional breaks**: new plugin API, new server API/clients, `tui.json`→`cli.json`. Every v1-style plugin fails (`SchemaError…`); some fail silently with exit 0.
- **LSP dead, share unimplemented**, background service always-on surprise, early missing `/model`, custom providers not picked up in early builds.
- **History gaps**: v1 sessions invisible at first; migrator 500s on corrupt rows / huge (>9k-message) sessions.
- IDE/ACP/GitHub/GitLab/Data pages partially missing.
- Early-adopter bug surface: deferred transform throws bricking catalogs, `{id,server}` silently dropped.

## 6. Who should stay on v1 (for now)

- Anyone depending on **oh-my-opencode hooks/tools** (no official v2 support shipped yet — see §7), programmatic MCP registration, LSP diagnostics, `/share`, IDE flows, `opencode serve` integrations, large history, or custom gateways.
- v1 is **still maintained** (1.18.34, Sep 30, 2026: signing, macOS, gateway, Gemini, Bedrock, Copilot fixes). No published v1 end-of-life date.
- Practical rule: run v2 isolated (`--standalone`, separate DB backup); switch when your plugin stack is green.

## 7. OMO on v1 vs v2

| OMO | OpenCode v1 | OpenCode v2 |
|---|---|---|
| 4.x legacy | ✅ Supported (≥1.0.132; installer ≥1.4.0) | ❌ Broken |
| 4.19.x unified migration | ✅ Supported + coexistence | ⚠️ Partial (no native v2 plugin mapping; needs 5.x) |
| 5.x beta | ✅ Supported | ⚠️ Requires v2-compatible plugin build; pin versions; official v2-support note still in progress |
| **OmO Native 5.0+** | ✅ Side-by-side (never touches OpenCode files) | ✅ Independent — **the safe v2-era path** |
| opensoft fork `dev` | ✅ Same as upstream | ⚠️ Same as upstream; check fork releases |

Notes: OMO is fragile to v1 minor breaks too (agent-registration and silent-hook regressions have happened). A community **slim fork** (`alvinunreal/oh-my-opencode-slim`) ships a dual v1+v2 package and documents the v2 port deltas — useful reference if you experiment on v2. Do not upgrade a production OMO install to v2 until `code-yeongyu` publishes v2 support; if you must try v2, use OmO Native or the slim dual build in isolation.

---

**Next:** [08 — Oh My OpenCode](./08-oh-my-opencode.md) · [10 — Plugins & Stacks](./10-plugins-and-stacks.md) · [11 — Amazing Additions](./11-amazing-additions.md)
