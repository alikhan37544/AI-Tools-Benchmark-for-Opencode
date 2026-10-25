# 06 — Free Models, Privacy & Local Options

> **Snapshot: October 1, 2026; refreshed October 13, 16 and 25, 2026.** Data policies change without notice — re-verify before sending client/PHI data.
>
> 🆕 **Oct 25 — the important corrections:**
> - **Gemini 4 Argon is NOT a Contributor/training SKU on Go.** Go’s privacy table documents it as **“Not used / 0 days.”** The Oct 16 warning that Argon trains on your data is **withdrawn**. The current SKU is `gemini-4-argon` at $2/$10/$0.10 (50% off through Nov 30) with a $30 cap.
> - **The only paid models on Go that still train are Muse Spark 1.3/1.2 Contributor.** Everything else is “Not used” (with 30-day retention for Grok/GPT/Haiku/Beam).
> - **Free-list churn:** **Space Bunny Free, LongCat 2.5 Preview Free, LL Alpha Free, Muse Spark 1.3 Contributor Free and Exo Free are gone.** **Flint 40B Free** is new (30-day + may train). The zero-retention twins (**DeepSeek V4.1 Flash Free, GLM-5.3-Flash Free**) remain.
> - **DeepSeek ZDR is valid through October 31, 2026** — re-verify after that date.
> - **Step 5 is paid** ($1/$2.70/$0.10, $15 cap) and its open weights are on HuggingFace.

---

## 1. Free models available on Go/Zen

| Model | Provider | Zero-retention? | Trained on? | Notes |
|---|---|---|---|---|
| **DeepSeek V4.1 Flash Free** ⭐ | DeepSeek | ✅ | ❌ | Free twin of the daily driver (AA 39, 1M ctx, vision). The best zero-retention free workhorse on OpenCode. Limited time. |
| **GLM-5.3-Flash Free** ⭐ | Zhipu | ✅ | ❌ | AA 42, multimodal-in, MIT lineage. The best free model on the platform. Limited time. |
| **Beam Free** | Reflection AI | ❌ (30-day) | ❌ | 501B/23B MoE, AA 30, Apache-2.0 weights. Limited time + limited regions (**India is not excluded**). 30-day retention, no training. |
| **Flint 40B Free** 🆕 | stealth/unknown | ❌ (30-day) | ✅ may train | **NEW Oct 25.** 40B-class; data may improve the model. Non-sensitive exploration only. |
| **MiMo-V2.6-Flash Free** | Xiaomi | ? | ✅ may train | Free-period training may occur — open-source work only. |
| **Nemotron 3.5 Super VL Free / Nemotron 3 Ultra / 3.5 Lightning Free** | NVIDIA | ❌ logged | ✅ trial terms | Vision/agent trial endpoints; **do not submit personal/confidential data**. |
| **Big Pickle** | stealth | ❌ | ✅ data used to improve model | Identity unknown (GLM-family audit); high-variance reliability. |
| **Jev 1.13 Free** | TypeSafe AI | — | — | Structured-decision model, not a chat model. |

**Removed from the free list this cycle:** Space Bunny Free (paid/removed), LongCat 2.5 Preview Free (window ended), LL Alpha Free, Muse Spark 1.3 Contributor Free, Exo Free.

**Rules of thumb:**
- Free + “feedbacks/improve the model” = **do not use for client work, PHI, credentials, or proprietary code**.
- **The two ⭐ twins (DeepSeek + GLM) state zero-retention and no training** — the first free models strong enough (AA 39–42) and clean enough to carry real non-critical work. Still limited-time windows: keep a fallback lane configured.
- Free models keep working **after your Go limits run out** — they are your floor and a genuinely capable one.

---

## 1b. Muse Spark Contributor — the one remaining training SKU on Go

**Verified Oct 1, 2026; re-verified Oct 25.** `muse-spark-1.3` and `muse-spark-1.3-contributor` are the **same weights/specs**. They are two separate SKUs that differ in price, rate limits, and data rights.

> **Correction (Oct 25):** the Oct 16 version of this file described **Gemini 4 Argon** as a second Contributor SKU. That is no longer true. Go’s current listing is `gemini-4-argon` (not “Contributor”), and the privacy table says **“Not used / 0 days.”** Treat Argon as **ZDR/no-training** on Go; the Zen Standard Argon SKU is the same model at 50% off through Nov 30. **Only Muse Spark 1.3/1.2 Contributor trains.**

| | muse-spark-1.3 (Standard) | muse-spark-1.3-contributor |
|---|---|---|
| Input / Output / Cached (per 1M) | $1.25 / $4.25 / $0.15 | **$0.10 / $0.20 / $0.002** |
| Prompts & completions | “not used to improve our products” | **“used to improve our products”** — Meta may train on them |
| Rate limits (per team) | 3,000 RPM / 4M TPM | **100 RPM** / 3M TPM |
| Geographic/end-user rules | Standard policy | Extra restrictions, some regions excluded |

On **OpenCode Go, the listed “Muse Spark 1.3/1.2 Contributor” is the Contributor SKU** (hence Go’s $0.10/$0.20/$0.002 rates); the no-training Standard SKU is on Zen at $1.25/$4.25/$0.15. **Meta Muse Code itself is not available in India** — Go is the practical route to Muse Spark, with the training caveat.

### What “must not submit sensitive, confidential, or personal information” means

Meta’s Contributor policy, verbatim:

> “You must not submit sensitive, confidential, or personal information to the Discounted Services. This means that you — and your end users — should not send inputs that contain any personal or confidential information. If your use case involves processing personal information, please use Standard Services.”
> — [Meta AI Developer Help Center](https://dev.meta.ai/help/policies-and-privacy/contributor-tier)

> “Discounted Services: Meta may use your Content, including Inputs and Outputs, to train, develop, evaluate, and improve Meta’s AI models… Meta may use Content for evaluation, safety, abuse, quality, and policy review.”
> — [Meta Model API Legal — Commitments](https://dev.meta.ai/legal/commitments)

“Ban” means **contractually prohibited**, not merely unwise. Using Contributor for such data breaches Meta’s terms, and you carry responsibility for what your agent sends.

### What counts as “Content” — the whole agent turn

Meta defines Content as inputs you provide **or authorize the Services to access** (prompts, documents, code, other data) **and** the generated responses. In an agentic OpenCode run that is:

- the typed prompt and the agent’s reasoning/plan output;
- **every file the agent reads**, including ones you never opened (the explore agent authorized them);
- **tool results**: grep matches, stack traces, test logs, SQL rows, API responses, git diffs;
- **documents/screenshots** the model processes (Muse Spark is multimodal);
- **generated code** — your new implementation is a completion and is also Content;
- any secret that leaks into those paths (.env values, PATs, connection strings, customer records, PHI).

A prompt scrubber is not enough: if a tool can fetch confidential workspace content after your request, it still gets sent.

### Green light vs red light

**Reasonable on Contributor:** greenfield prototypes, personal learning, open-source repos, throwaway experiments, benchmarks/eval harnesses, synthetic data/boilerplate, code you’d be fine publishing. Test: *“Would I be fine if this exact content appeared in a future Meta training set?”*

**Never on Contributor:** any client work (NDA/contractual duty), medical/insurance/PHI pipelines (even “just OCR”), proprietary code that is the business asset, anything with credentials/tokens/security findings in context, production agent traffic where you can’t enumerate tool access, end-user traffic without documented consent/eligibility. Test: *“Does anyone else own or regulate this data?”*

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
| Kimi K3.1 Pro / K3 / K2.7 | Zero-retention per OpenCode; K3 open weights | ✅ (still confirm) |
| Qwen3.8 Max/Flash, Qwen3.7 Plus | Zero-retention per OpenCode | ✅ |
| DeepSeek V4.1 Flash / V4 Pro | Zero-retention listed; ZDR agreement **valid through October 31, 2026** ✅ | ✅ (re-verify after Oct 31) |
| **DeepSeek V4.1 Flash Free / GLM-5.3-Flash Free** | **Zero-retention, no training per OpenCode docs** | ✅ for non-critical free work — the safest free options |
| Grok 4.7 | Go docs list **30-day retention, not used for training** | ⚠️ non-PHI/client-sensitive only until re-verified |
| GPT 6/5.6 Luna | OpenAI API, **30-day retention** per OpenAI policy | ⚠️ for non-PHI; note your CV client contract bans OpenAI models entirely |
| Claude Haiku 5.5 | Anthropic API, **30-day retention** per Anthropic policy | ⚠️ for non-PHI (Anthropic, not OpenAI — CV contract’s OpenAI ban doesn’t cover it; verify anyway) |
| Claude (Zen only, not Go) | Anthropic 30-day retention | ⚠️ same |
| **Gemini 4 Argon (Go)** | **“Not used / 0 days”** per Go’s privacy table — **no training** | ✅ for client/PHI after your own verification — **the Oct 16 training warning is withdrawn** |
| **Muse Spark Contributor (paid)** | **Trains on prompts/completions; terms ban sensitive/confidential/personal data** (Standard SKU does neither) | ❌ never for client/PHI — see §1b |
| **Beam Free** | 30-day retention (safety), **no training** | ⚠️ non-critical only |
| **Flint 40B Free** | **30-day retention; data may be used to improve the model** | ❌ not for sensitive/private work |
| **MiMo-V2.6-Flash Free** | May train during free period | ❌ non-sensitive only |
| **Nemotron free** | Logged; trial terms | ❌ not for sensitive/private work |
| **Big Pickle** | Data may improve the model | ❌ for critical/PHI |
| **Jev 1.13 Free** | Structured-decision model | — not a chat/coding model |
| Step 5 Preview (paid) | Zero-retention per OpenCode; **open weights (self-host option)** | ✅ (still confirm) |

OpenCode hosts all models in the US. Enterprise/team workspace admins can disable specific models workspace-wide — useful if you ever onboard others.

---

## 3. Local LLMs — your RTX 5060 Ti 16GB + 64GB RAM machine

Go is now so cheap for near-frontier models that local inference is **not** a cost play for coding agents anymore; it’s a **privacy and offline** play. The realistic local use cases:

| Use case | Recommendation |
|---|---|
| Offline/air-gapped code completion | Qwen3-Coder / Qwen3.8-27B class, 4-bit, ~30–40 tok/s on 16GB |
| Private PHI pre-processing (no network) | A 14B–27B model for redaction/formatting; accept lower quality |
| Fast autocomplete (FIM) | Qwen2.5-Coder 14B or Devstral Small 2 (384K ctx) |
| Experimentation | LM Studio (you already run it on :1234) or Ollama |

Given the price and quality of DeepSeek V4.1 Flash / M3.1 Flash / GLM-5.3-Flash on Go, the local box is best kept for: (a) zero-network sensitive transforms, (b) autocomplete, (c) learning. Don’t expect a 16GB GPU to replace the Go roster for agentic coding in 2026. **Step 5 Preview’s open weights** (600B/27B-active, BF16/FP8) are on HuggingFace — too big for the 5060 Ti at full precision, but FP8 + CPU offload or a quantized build is the first *frontier-adjacent* model you can self-host for zero-retention-sensitive work. **Kimi K3.1 Pro is 3T-class** — not a local candidate.

Source context: prior local research in this repo’s history; current model recommendations should be re-checked against [ollama.com/library](https://ollama.com/library) and [HuggingFace trending](https://huggingface.co/models?pipeline_tag=text-generation&sort=trending) at update time.

---

## 4. Data-hygiene checklist for agentic work

1. Block training/free routes at the config level for client projects (see `07-recommended-config.md`).
2. Keep secrets out of prompts: use `.env` + tools that read env vars, never paste PATs into chat.
3. For Azure DevOps requests, let the agent run `az`/`git` with credentials from the keychain/environment — not from conversation context.
4. Remember that **session titles, plans and summaries** are generated by a small model — they still contain snippets. Some OpenCode deployments use cheap models (often a DeepSeek/Qwen flash) for titles.
5. Your local OpenCode DB currently stores session content (and is ~39GB on the primary machine). If a client requires it, prune old sessions or use per-project workspaces.
6. When in doubt, run the sensitive-transform steps on the local model.
7. **Re-check DeepSeek ZDR after Oct 31, 2026** — the current agreement has an explicit expiry.

---

**Next:** [07 — Recommended Config](./07-recommended-config.md)
