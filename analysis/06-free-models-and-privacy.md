# 06 — Free Models, Privacy & Local Options

> **Snapshot: October 1, 2026.** Data policies change without notice — re-verify before sending client/PHI data.

---

## 1. Free models available on Go/Zen

| Model | Provider | Zero-retention? | Trained on? | Notes |
|---|---|---|---|---|
| **Space Bunny Free** | stealth (MiniMax-family fingerprint?) | ✅ on OpenCode route | ❌ (OpenCode says no) | #1 model by tokens (58T/wk); 1M ctx, vision; fast; tool-param wrapping bug; identity unconfirmed |
| **LongCat 2.5 Preview Free** | Meituan | ✅ | ❌ | Free ~2 weeks (to ~Oct 10); no public benchmarks/card; LongCat-2.0 numbers (SWE Pro 59.5) are the only proxy |
| **MiMo-V2.6-Flash Free** | Xiaomi | ? | ✅ may train | Same weights family as paid MiMo; use only for open-source work |
| **MiMo-V2.5 Free** | Xiaomi | ? | ✅ may train | Weaker (AA 25) |
| **Ling 3.0 Flash Fin Free** | InclusionAI | ? | ✅ may train | Finance-oriented |
| **Nemotron 3 Ultra Free** | NVIDIA | ❌ logged | ✅ trial terms | **Do not submit personal/confidential data** |
| **Nemotron 3.5 Lightning Free** | NVIDIA | ❌ logged | ✅ trial terms | Same warning |
| **Big Pickle** | stealth | ❌ | ✅ data used to improve model | Identity unknown (GLM-family audit); 95%+ of one user's stream errors |
| **Muse Spark 1.3 Contributor Free** | Meta | ❌ | ✅ explicitly | Free/discounted in exchange for training rights |
| **Jev 1.13 Free** | TypeSafe AI | prompts not used for training | ❌ | Not a chat model — structured decision API |

**Rules of thumb:**
- Free + "feedbacks/improve the model" = **do not use for client work, PHI, credentials, or proprietary code**.
- Space Bunny / LongCat 2.5 free previews are the only free options with a stated **zero-retention** policy (still stealth, so treat with caution).
- Free models keep working **after your Go limits run out** — they are your floor, not your daily driver.

---

## 1b. Muse Spark Contributor: same model, two contracts

**Verified Oct 1, 2026.** `muse-spark-1.3` and `muse-spark-1.3-contributor` are the **same weights/specs** (1M context, same modalities, reasoning efforts, tools). They are two separate SKUs that differ in price, rate limits, and data rights. Independent analyses agree: "same weights, different terms."

| | muse-spark-1.3 (Standard) | muse-spark-1.3-contributor |
|---|---|---|
| Input / Output / Cached (per 1M) | $1.25 / $4.25 / $0.15 | **$0.10 / $0.20 / $0.002** |
| Prompts & completions | "not used to improve our products" | **"used to improve our products"** — Meta may train on them |
| Rate limits (per team) | 3,000 RPM / 4M TPM | **100 RPM** / 3M TPM |
| Geographic/end-user rules | Standard policy | Extra restrictions, some regions excluded |

On **OpenCode Go, the listed "Muse Spark 1.3/1.2 Contributor" is the Contributor SKU** (hence Go's $0.10/$0.20/$0.002 rates); the no-training Standard SKU is on Zen at $1.25/$4.25/$0.15.

### What "must not submit sensitive, confidential, or personal information" means

Meta's Contributor policy, verbatim:

> "You must not submit sensitive, confidential, or personal information to the Discounted Services. This means you — and your end users — should not send inputs that contain any personal or confidential information. If your use case involves processing personal information, please use Standard Services."
> — [Meta AI Developer Help Center](https://dev.meta.ai/help/policies-and-privacy/contributor-tier)

> "Discounted Services: Meta may use your Content, including Inputs and Outputs, to train, develop, evaluate, and improve Meta's AI models… Meta may use Content for evaluation, safety, abuse, quality, and policy review."
> — [Meta Model API Legal — Commitments](https://dev.meta.ai/legal/commitments)

"Bar" means **contractually prohibited**, not merely unwise. Using Contributor for such data breaches Meta's terms, and you carry responsibility for what your agent sends.

### What counts as "Content" — the whole agent turn

Meta defines Content as inputs you provide **or authorize the Services to access** (prompts, documents, code, other data) **and** the generated responses. In an agentic OpenCode run that is:

- the typed prompt and the agent's reasoning/plan output;
- **every file the agent reads**, including ones you never opened (the explore agent authorized them);
- **tool results**: grep matches, stack traces, test logs, SQL rows, API responses, git diffs;
- **documents/screenshots** the model processes (Muse Spark is multimodal);
- **generated code** — your new implementation is a completion and is also Content;
- any secret that leaks into those paths (.env values, PATs, connection strings, customer records, PHI).

A prompt scrubber is not enough: if a tool can fetch confidential workspace content after your request, it still gets sent.

### Green light vs red light

**Reasonable on Contributor:** greenfield prototypes, personal learning, open-source repos, throwaway experiments, benchmarks/eval harnesses, synthetic data/boilerplate, code you'd be fine publishing. Test: *"Would I be fine if this exact content appeared in a future Meta training set?"*

**Never on Contributor:** any client work (NDA/contractual duty), medical/insurance/PHI pipelines (even "just OCR"), proprietary code that is the business asset, anything with credentials/tokens/security findings in context, production agent traffic where you can't enumerate tool access, end-user traffic without documented consent/eligibility. Test: *"Does anyone else own or regulate this data?"*

### The agentic trap (why this is a hard rule here)

Sessions on this machine read insurance/claims repos, run DB queries, grep logs, and process Arabic medical documents. A Contributor model in that loop receives the files, query results, and document images automatically — not just your question. **Never make a Contributor model a default or fallback in client projects.**

### Safeguards if you do use it

1. Pin the model ID explicitly; never put it in `small_model` or as a global default.
2. Isolate it to a project config in public/personal repos only.
3. Classify data before routing: client names, PHI, credentials, NDA code → Contributor is out.
4. Restrict tools/read paths so the agent cannot fetch confidential context mid-run.
5. Watch 100 RPM (per team) — agent fan-out will throttle.
6. Meta says it accepts zero-data-retention requests on Contributor; ask if needed, but the data-class ban still applies.
7. Log what leaves the machine for Contributor sessions.

The economics: the discount (~$1.15 per 1M input tokens) is what Meta effectively pays for your data. It is a trade, not a sale — and there is no undo button on a training leak.

---

## 2. Paid-model privacy posture (for your medical/insurance work)

| Route | Retention/training | Safe for PHI/client code? |
|---|---|---|
| GLM-5.3 / 5.3-Flash / 5.2 (Z.ai) | OpenCode states zero-retention, no training | ✅ (MIT weights for Flash/5.2; verify) |
| MiMo-V2.6-Pro/Flash paid | OpenCode zero-retention | ✅ |
| Kimi K3/K2.7/K2.6 | Zero-retention per OpenCode; open weights | ✅ |
| Qwen3.8 Max/Flash, Qwen3.7 Plus | Zero-retention per OpenCode | ✅ |
| DeepSeek V4.1 Flash/V4 Pro | Zero-retention listed, but the ZDR agreement showed validity **through Sep 30, 2026** — renewal unconfirmed as of Oct 1 | ⚠️ re-verify |
| Grok 4.6/4.7 | Zero-retention per OpenCode | ✅ |
| GPT 6/5.6 Luna | OpenAI API, **30-day retention** per OpenAI policy | ⚠️ for non-PHI; note your CV client contract bans OpenAI models entirely |
| Claude (Zen only, not Go) | Anthropic 30-day retention | ⚠️ same |
| **Muse Spark Contributor (paid)** | **Trains on prompts/completions; terms ban sensitive/confidential/personal data** (Standard SKU does neither) | ❌ never for client/PHI — see §1b |
| Space Bunny / Big Pickle | varies | ❌ for critical/PHI |

OpenCode hosts all models in the US. Enterprise/team workspace admins can disable specific models workspace-wide — useful if you ever onboard others.

---

## 3. Local LLMs — your RTX 5060 Ti 16GB + 64GB RAM machine

Go is now so cheap for near-frontier models that local inference is **not** a cost play for coding agents anymore; it's a **privacy and offline** play. The realistic local use cases:

| Use case | Recommendation |
|---|---|
| Offline/air-gapped code completion | Qwen3-Coder / Qwen3.8-27B class, 4-bit, ~30–40 tok/s on 16GB |
| Private PHI pre-processing (no network) | A 14B–27B model for redaction/formatting; accept lower quality |
| Fast autocomplete (FIM) | Qwen2.5-Coder 14B or Devstral Small 2 (384K ctx) |
| Experimentation | LM Studio (you already run it on :1234) or Ollama |

Given the price and quality of DeepSeek V4.1 Flash / GLM-5.3-Flash on Go, the local box is best kept for: (a) zero-network sensitive transforms, (b) autocomplete, (c) learning. Don't expect a 16GB GPU to replace the Go roster for agentic coding in 2026.

Source context: prior local research in this repo's history; current model recommendations should be re-checked against [ollama.com/library](https://ollama.com/library) and [HuggingFace trending](https://huggingface.co/models?pipeline_tag=text-generation&sort=trending) at update time.

---

## 4. Data-hygiene checklist for agentic work

1. Block training/free routes at the config level for client projects (see `07-recommended-config.md`).
2. Keep secrets out of prompts: use `.env` + tools that read env vars, never paste PATs into chat.
3. For Azure DevOps requests, let the agent run `az`/`git` with credentials from the keychain/environment — not from conversation context.
4. Remember that **session titles, plans and summaries** are generated by a small model — they still contain snippets. Some OpenCode deployments use cheap models (often a DeepSeek/Qwen flash) for titles.
5. Your local OpenCode DB currently stores session content (and is ~39GB). If a client requires it, prune old sessions or use per-project workspaces.
6. When in doubt, run the sensitive-transform steps on the local model.

---

**Next:** [07 — Recommended Config](./07-recommended-config.md)
