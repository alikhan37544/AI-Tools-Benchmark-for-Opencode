# 11 — Amazing Additions: Personalized Power-Up Playbook

> **Snapshot: October 1, 2026.** Built for YOUR stack: Azure DevOps everywhere (Pipelines/Repos, no GitHub Actions), `az login` agent access, Playwright/Puppeteer/Selenium RPA + captcha work, a 578-check visual QA suite, voicebot/telephony (Asterisk ARI, Kafka, Redis, Realtime), OCR/document AI incl. Arabic, PHI/medical data, 40+ repos.
> Each item is rated **Value** (how much it changes your day) × **Effort** (to install). Start at the top.

---

## 0. The 80/20 list (do these first)

| # | Addition | Value | Effort | Section |
|---|---|---|---|---|
| 1 | `azure-devops` SKILL.md + ADO MCP on `--authentication azcli` | ★★★★★ | 30 min | §1 |
| 2 | Nightly autonomous build-health check (scheduler + `opencode run`) | ★★★★★ | 1 h | §1 + §5 |
| 3 | `browser-ops` skill: Playwright-CLI-first doctrine + POM + storageState | ★★★★★ | 1–2 h | §2 |
| 4 | Pipeline-failure auto-triage recipe (logs → diagnosis → PR) | ★★★★☆ | 1 h | §1 |
| 5 | PHI-safe permission design + `.env` guard + gitleaks in loop | ★★★★☆ | 1 h | §4 |
| 6 | Per-repo AGENTS.md everywhere + global conventions (memory that survives) | ★★★★☆ | 2–3 h | §3 |
| 7 | `opencode-notify` for Ralph loops + wakatime/quotas awareness | ★★★☆☆ | 20 min | §5 |
| 8 | ARI/Kafka/Redis/Realtime triage skills for voicebot work | ★★★★☆ | 2 h | §6 |
| 9 | Azure DI cost-ladder skill (classify → layout → prebuilt → LLM vision) | ★★★★☆ | 2 h | §7 |
| 10 | Oh My OpenCode Ultimate (Sisyphus + background agents + Ralph) | ★★★★★ | 2–4 h | `08` |

---

## 1. Azure autonomy: from `az login` trick to a system

You already give the agent your `az login` session — that was the unlock. The system around it:

### Install (v1; v2 deltas in `10`)

```jsonc
{ "mcp": { "azure-devops": { "type": "local",
    "command": ["npx", "-y", "@azure-devops/mcp", "YOUR-ORG",
      "-d", "core", "repositories", "pipelines", "work-items", "search",
      "--authentication", "azcli"],
    "enabled": true,
    "environment": { "ado_mcp_project": "YourProj",
      "REQUESTS_CA_BUNDLE": "{env:REQUESTS_CA_BUNDLE}",
      "NODE_EXTRA_CA_CERTS": "{env:NODE_EXTRA_CA_CERTS}" } } } }
```

`--authentication azcli` reuses your `az login` — no PAT in config. Prefer the **local** MCP for OpenCode (remote Entra MCP + OpenCode is untested); add remote later for Entra-only teams (`https://mcp.dev.azure.com/{org}` + `X-MCP-Toolsets`/`X-MCP-Readonly` headers).

### `~/.config/opencode/skills/azure-devops/SKILL.md`

```md
---
name: azure-devops
description: Triage ADO pipelines/PRs via az CLI + ADO MCP. Build logs, JMESPath, variable-groups, az ssh tunnels.
---
Defaults: `az devops configure --defaults organization=https://dev.azure.com/YOUR-ORG project=Proj`
Prefer MCP read-only tools; use `az` for variable-groups/releases/artifacts-universal.
Logs: fetch failed log ID only, `tail -c 20k`, grep `##[error]`.
Never print PATs/tokens; use `az login` cache or keychain `$AZURE_DEVOPS_EXT_PAT`.
```

### Read-only vs write allowlists

Read-only agent allows: `az pipelines runs list/show*`, `az pipelines build list*`, `az pipelines runs artifact list/download*`, `az repos pr list/show*`, `az repos list/show*`, `az pipelines variable-group list/show*` + `variable list*`. Deny: `az account get-access-token*`, `az pipelines run*`, `az repos pr create*`, `az pipelines delete*`, `*--password*`, `*PAT*`, `printenv`. Write-enabled triage additionally allows `az pipelines run*`, `az repos pr create/update/set-vote*`, reviewer add, variable update, artifact upload.

### Recipe A — pipeline-failure auto-triage (the money workflow)

Trigger: `az pipelines runs list --result failed --top 1` (poll) or a Service Hook. Steps: (1) failed run status + **failed log tail only** (`tail -c 20k`, never whole MBs logs — token burn); (2) correlate with recent commits/diff; (3) patch on a new branch; (4) open PR titled `Fixes build <id>: <root cause>` with log excerpt in a thread comment. Needs `pipelines+repos+wit` toolsets.

### Recipe B — nightly build-health report

`launchd` (02:00) → `opencode run --auto` with read-only permission: list top-20 runs, group by pipeline/result, fetch 2–3 failed tails, write `docs/build-health/YYYY-MM-DD.md` (+ wiki upsert). This is your "check status autonomously" trick, running while you sleep. (`opencode-scheduler` plugin wraps the same idea if you prefer it.)

### Recipe C — PR auto-review

Nightly `az repos pr list --status active`: fetch changes + touched files, run `git diff --check`/build/lint, post severity-tagged thread comments. Keep vote/auto-complete human-gated.

### Auth ladder (best → worst for agents)

1. **Your `az login`** (dev laptop agent; MCP `azcli` reuses it; Entra auto-refresh).
2. **Managed identity** (Azure-hosted schedulers; no secret at all).
3. **Service principal** (headless automation; must be added to org/project explicitly).
4. **PAT** (fallback only; org-scoped, 30d max, keychain-stored, never in prompts; global PATs retire Dec 2026).

### Gotchas that will bite you (all verified)

- **Corporate TLS proxy:** `REQUESTS_CA_BUNDLE` + `NODE_EXTRA_CA_CERTS` with your combined PEM; `az login` (MSAL) historically ignores the bundle — fix is a valid CA with AKI, and allow-list `mcp.dev.azure.com:443`.
- **NSG-blocked ports:** `az ssh vm` (+ `-L` tunnels) or Bastion/jumpbox; VMSS needs per-instance NAT-pool info.
- **PAT rotation:** inventory owner/purpose/scope/expiry; org-scoped short-lived replacements; audit `Token.Pat*` events.
- **Rate limits:** honor `Retry-After`; prefer batch APIs + webhooks over polling in schedulers.
- **Log truncation is a cost control:** always `list` → failed log ID → tail/grep `##[error]`.
- ADO MCP has **no variable-group CRUD, no classic Releases, no universal-publish** — use `az pipelines variable-group`, `az pipelines release`, `az artifacts universal` for those.

---

## 2. Browser automation & RPA: the CLI-first doctrine

Microsoft's own 2026 guidance: **CLI+skill is more token-efficient** (no giant tool schemas/ARIA trees in context); **live MCP wins for exploratory healing and long autonomous runs**. Your rule:

> **Live-drive to discover + heal. Freeze into scripts + POM for repeatable runs. Never live-drive 578 checks.**

### `browser-ops` skill (`.opencode/skills/browser-ops/SKILL.md`)

```md
---
name: browser-ops
description: Browser tasks MUST USE playwright-cli first (open/snapshot/find/click/fill/screenshot/pdf/tracing/video/route/state-save). MCP only for exploratory healing. Never paste raw DOM; use refs.
---
1. `playwright-cli open <url>` → `snapshot --depth=4` or `find "<text>"`
2. Act with refs; prefer role/testid locators
3. Evidence: `screenshot`, `tracing-start/stop`, `video-start/stop`
4. Persist: `state-save auth.json` / `state-load auth.json`; sessions `-s=<name>`
5. Breakage: `generate-locator <ref>` → patch POM → re-run single spec
```

```jsonc
{ "mcp": { "playwright": { "type": "local",
    "command": ["npx", "@playwright/mcp@latest", "--isolated", "--caps=pdf,devtools"], "enabled": true } },
  "tools": { "playwright*": false },
  "agent": { "rpa-healer": { "tools": { "playwright*": true } } } }
```

### Self-healing loop (your heal-bot, formalized)

Locator priority: `getByRole` > `getByLabel` > placeholder/alt/title > `getByTestId` (explicit contract) > CSS/XPath last — long chains are documented bad practice. Locators re-query DOM per action (free healing) + auto-wait + web-first assertions. On breakage: snapshot + console + tracing → `generate-locator` → **patch the POM in one place** → re-run `--retries=1 --trace=on-first-retry`. Record human demos with `codegen` to emit role-first code.

### Captchas: the decision framework (important for your portals)

reCAPTCHA is now **Google Cloud Fraud Defense** (risk scoring 0.0–1.0, not a static image) — vision-model bypass rates from your benchmark tool do **not** transfer to Enterprise. Rule: own site/test keys → automate freely; **production insurance/gov portals → human-in-the-loop** (pause, route to operator, log trace+video+console as audit trail); prefer APIs/`storageState`/official bulk channels. No citable ToS clause permits automating credentialed claim submission without written authorization. Vision-solving or farming third-party portals = ToS violation + audit risk.

### 578-check visual QA at scale

`toHaveScreenshot` goldens per browser+platform (`maxDiffPixels`, `stylePath` to hide volatiles, `mask`/`maskColor`, `animations:'disabled'`); `fullyParallel` + **`--shard=1/4…4/4` matrix + blob merge**; `trace/video: on-first-retry`; commit snapshots to git, large diffs to blob storage; generate baselines in the same env as CI; headed Chromium on the Azure VM for Enterprise-score portals. **Keep pixelmatch as the verdict; use vision models as the explainer** (benchmark candidate judges on your own goldens before trusting any).

### Extension tests

MV3 via `launchPersistentContext` + `--load-extension=./dist`, `waitForEvent('serviceworker')`, derive `extensionId` from worker URL, drive `chrome-extension://<id>/popup.html`. Sidecar pattern: extension holds portal session/DOM helpers, Playwright drives the page.

---

## 3. Memory that survives (40 repos, zero PHI leakage)

1. **Per-repo `AGENTS.md` everywhere** (`/init` generates; commit it): stack, build/test commands, "never commit .env, never memorize caller audio/PHI", pointer to `docs/conventions.md`. You have 6 — extend to all active repos. This is the highest-ROI memory: it rides along in context automatically.
2. **Global `~/.config/opencode/AGENTS.md`**: owner map of all repos, "no PHI in memory", "prefer Tesseract/YOLO before LLM vision", Azure defaults.
3. **OMO Kibitzer** (when you adopt OMO): local markdown git repo of lessons; a cheap model nudges the main agent before it repeats a mistake. No PHI leaves the box.
4. **Supermemory/mem0 only for non-PHI**: `recallMode direct`, `captureEveryNTurns: 3`, `<private>…</private>` exclusion, weekly refresh + forget stale; **cloud memory is OFF for PHI workdirs** (self-host or nothing).
5. Hygiene: `gitleaks dir` before any memory export; deny cloud memory in PHI projects.

---

## 4. Safety for PHI (the non-negotiable layer)

```jsonc
{ "permission": { "*": "ask",
    "read": { "*": "allow", "*.env": "deny", "*.env.*": "deny" },
    "edit": { "*": "ask", ".env*": "deny" },
    "bash": { "*": "ask", "rm -rf *": "deny", "git push *": "deny",
      "psql *": "deny", "mysql *": "deny", "*PHI*": "deny", "*patient*": "deny" },
    "webfetch": "ask", "websearch": "deny" },
  "share": "disabled" }
```

Plus: a read-only `phi-readonly` subagent (edit deny, bash deny except grep); **read-only DB users** + scoped MCP tools (agent gets SELECT only, never a psql shell); `opencode-vibeguard` to redact secrets into `__VG_*__` placeholders before provider calls; `.env` read-guard plugin; `gitleaks` in the loop and pre-commit. DB rule is the big one: the agent should never hold a credentialed shell — only a scoped read-only tool.

---

## 5. Schedulers + notifications (autonomy while you sleep)

- **Nightly recipe**: `launchd` 02:00 → `opencode run --auto "Nightly: az build status (top 20), DI model version, kafka lag, redis memory; write logs/scheduler/$(date +%F).log; notify on fail"` with read-only permission (+ the RPA nightly via sharded Playwright). `opencode-scheduler` plugin wraps the same mechanics if you prefer managed jobs.
- **Notifications**: native v2 attention sounds, or `opencode-notify` on v1 (idle/permission/error) — mandatory once Ralph loops run for hours.
- **Awareness**: `opencode-wakatime` + `opencode stats --days 7 --models` so you see where requests go; `opencode-quotas` footer so walls never surprise you.

---

## 6. Voicebot/telecom triage skills

**`ari-telephony` skill**: `asterisk -rx "core show channels(verbose)"`, `pjsip show endpoints`, `ari show apps`; ARI `curl` for channels/bridges/playback/originate; correlate `channelId` → events websocket → bridge enter/leave → playback IDs. **Kafka skill**: `kafka-topics --describe`, consumer-group lag, console-consumer sample (`--max-messages 20`), Schema Registry `…/subjects/<topic>-value/versions/latest`, DLQ + redrive checks, `BACKWARD` compat. **Redis**: `INFO memory`, `XLEN`/`XREAD` streams, `--latency-history`. **Realtime QA loop**: record ARI audio → file-transcription vs realtime transcript WER → log deltas → replay. SIPp patterns: verify `sipp -h` locally before codifying.

---

## 7. OCR pipeline skill (cost ladder)

Azure DI v4.0 (GA; v3.0 retires Mar 2029): `prebuilt-read` + `prebuilt-layout` (`features=keyValuePairs,ocr.highResolution`) + prebuilts (invoice/receipt/idDocument/healthInsuranceCard.us/contract/…). **Arabic is supported** (printed + handwritten `ar`, auto-detect). Agent ladder (cheapest first): **custom classifier (1 cheap call) → layout/read for structure → prebuilt only on its class → LLM vision/Gemini only for confidence <0.8 crops + Arabic→English translate**. YOLO pattern: segment damage bbox → send the **crop, not the full page**, with DI polygon + confidence. `ocr.highResolution` only for small fonts/damage. Local fallbacks: `tesseract -l ara+eng`, YOLO seg. Eval harness like your captcha-benchmark: accuracy/latency/cost per doc on a golden set. (Azure pricing page was unreachable during research — confirm in portal.)

---

## 8. Install order for maximum wow-per-hour

1. ADO MCP (`azcli`) + `azure-devops` skill + read-only allowlist (30 min) → 2. nightly build-health job (1 h) → 3. `browser-ops` skill + POM + storageState (1–2 h) → 4. PHI-safe permissions + vibeguard + gitleaks (1 h) → 5. AGENTS.md sweep (2–3 h) → 6. notify + wakatime (20 min) → 7. ARI/Kafka/Redis/DI skills (one evening) → 8. OMO Ultimate (`08`) for orchestration + Ralph + background teams.

---

**Back to:** [08 — Oh My OpenCode](./08-oh-my-opencode.md) · [09 — v1 vs v2](./09-opencode-v1-vs-v2.md) · [10 — Plugins & Stacks](./10-plugins-and-stacks.md)
