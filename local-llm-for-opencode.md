# Local LLM Analysis for OpenCode

> **Updated: August 19, 2026** | Hardware: Ryzen 9 5900XT (16C) + RTX 5060 Ti 16GB + 64GB DDR4

## TL;DR

| Role | Model | Quant | VRAM | Speed | Quality |
|------|-------|-------|------|-------|---------|
| **Best New** | Qwen3.8-27B | Q4_K_M | ~17 GB | ~30-40 tok/s | SWE-bench Pro 61.7% |
| **Best MoE** | Gemma 4 26B (MoE) | Q3_K_M | ~16 GB | ~95+ tok/s | Frontier reasoning |
| **Daily Driver** | Qwen 3.6 35B-A3B | Q3_K_M | ~16.6 GB | ~80-100 tok/s | SWE-bench 73.4% |
| **Autocomplete** | Qwen 2.5 Coder 14B | Q4_K_M | ~9 GB | ~34 tok/s | HumanEval 89.9% |
| **Agentic Coding** | Devstral Small 2 24B | Q4_K_M | ~15 GB | ~25-30 tok/s | SWE-bench 65.8% |
| **Fast Fallback** | Qwen 2.5 Coder 7B | Q5_K_M | ~5.5 GB | ~70-80 tok/s | Good for quick tasks |

---

## Your Hardware

| Component | Spec | LLM Relevance |
|-----------|------|---------------|
| **CPU** | Ryzen 9 5900XT (16C/32T, Zen 3) | Good for CPU offload, AVX2 (no AVX-512) |
| **GPU** | RTX 5060 Ti 16GB GDDR7 | Blackwell arch, 448 GB/s, native FP4 |
| **RAM** | 64GB DDR4 | Can hold ~70B model weights for offload |
| **PSU** | 1000W+ | No power throttling |
| **Cooling** | 9-fan case | Can sustain full throttle indefinitely |

---

## Latest Models (August 2026)

### NEW: Qwen3.8-27B (Released Aug 14, 2026)
- **Params:** 28B dense
- **Type:** Image-Text-to-Text (multimodal, vision-language)
- **License:** Apache 2.0
- **Context:** 262K native (1M via YaRN)
- **GGUF:** Available via `unsloth/Qwen3.8-27B-GGUF` on HuggingFace
- **Ollama:** Not yet in library, use GGUF directly
- **VRAM:** ~17GB at Q4_K_M (tight but fits)
- **Benchmarks:**
  - SWE-bench Pro: 61.7% (beats cited Claude Opus 4.6 Max at 53.4%)
  - Terminal-Bench 2.1: 73.0%
  - GPQA Diamond: 89.2%
  - Artificial Analysis Intelligence: 52
- **Downloads:** 1M+ in 3 days on HuggingFace
- **Key:** Massive jump from Qwen3.6-27B (Intelligence 38 → 52)

### NEW: Gemma 4 (Released Aug 2026)
- **Sizes:** E2B, E4B, 12B, 26B (MoE), 31B (Dense)
- **Type:** Vision + Tools + Thinking + Audio
- **Context:** 128K (small), 256K (medium)
- **License:** Apache 2.0
- **Ollama:** Available now
- **Benchmarks (31B):**
  - MMLU Pro: 85.2%
  - LiveCodeBench v6: 80.0%
  - Codeforces ELO: 2150
  - AIME 2026: 89.2%
- **MoE 26B:** 25.2B total, 3.8B active, 8 active/128 total experts
- **VRAM:** E2B 7.2GB, E4B 9.6GB, 12B 7.6GB, 26B MoE ~18GB, 31B ~20GB

### NEW: Devstral Small 2 (Mistral)
- **Params:** 24B
- **Type:** Vision + Tools (agentic coding)
- **Context:** 384K
- **License:** Apache 2.0
- **VRAM:** ~15GB at Q4_K_M
- **SWE-bench Verified:** 65.8%
- **Highlights:** Multi-file editing, codebase exploration, software engineering agents

### Qwen3-Coder-Next
- **Params:** 80B total, 3B active (MoE)
- **Context:** 256K
- **Training:** 800K executable tasks + RL
- **VRAM:** ~52GB at Q4_K_M (not for 16GB)

### ByteDance Seed-2.0-Code (Aug 12)
- **Type:** Code-specialized
- **Details:** New entrant, limited info available

---

## Recommended Models for Your Hardware

### Tier 1: Best for OpenCode (Full GPU, 16GB VRAM)

| Model | Params | Quant | VRAM | Speed | Quality | Context | License |
|-------|--------|-------|------|-------|---------|---------|---------|
| **Qwen3.8-27B** | 28B | Q4_K_M | ~17 GB | ~30-40 tok/s | SWE-bench Pro 61.7% | 262K | Apache 2.0 |
| **Gemma 4 26B (MoE)** | 25.2B (3.8B active) | Q3_K_M | ~16 GB | ~95+ tok/s | Frontier reasoning | 256K | Apache 2.0 |
| **Gemma 4 12B** | 12B | Q4_K_M | ~7.6 GB | ~50+ tok/s | MMLU Pro 85.2% | 256K | Apache 2.0 |
| **Qwen 3.6 35B-A3B** | 35B (3B active) | Q3_K_M | ~16.6 GB | ~80-100 tok/s | SWE-bench 73.4% | 262K | Apache 2.0 |
| **Devstral Small 2 24B** | 24B | Q4_K_M | ~15 GB | ~25-30 tok/s | SWE-bench 65.8% | 384K | Apache 2.0 |
| **Qwen 2.5 Coder 14B** | 14B | Q4_K_M | ~9 GB | ~34 tok/s | HumanEval 89.9% | 128K | Apache 2.0 |
| **DeepSeek Coder V2 Lite** | 16B (2.4B active) | Q4_K_M | ~10 GB | ~45 tok/s | HumanEval 81.1% | 128K | MIT |

### Tier 2: Partial CPU Offload (Higher Quality, Slower)

| Model | Params | Quant | VRAM+RAM | Speed | Quality |
|-------|--------|-------|----------|-------|---------|
| **Qwen3-Coder 32B** | 32B | Q4_K_M | ~18.4 GB (4-5 layers on CPU) | ~22 tok/s | HumanEval+ 84.1% |
| **Qwen 3.6 27B** | 27B | Q4_K_M | ~17 GB (tight) | ~20-30 tok/s | SWE-bench 77.2% |

### Tier 3: Budget / Ultra-Fast

| Model | Params | Quant | VRAM | Speed | Best For |
|-------|--------|-------|------|-------|----------|
| **Qwen 2.5 Coder 7B** | 7B | Q5_K_M | ~5.5 GB | ~70-80 tok/s | Quick tasks |
| **DeepSeek-Coder 6.7B** | 6.7B | Q4_K_M | ~4.5 GB | ~100 tok/s | Ultra-fast |
| **Gemma 4 E4B** | ~4B | Q4_K_M | ~9.6 GB | Very fast | Multimodal + audio |
| **Phi-4 14B** | 14B | Q6_K | ~11.5 GB | ~49 tok/s | Math/STEM |

### Skip These (Outclassed in 2026)
- CodeLlama (all sizes) — massively outclassed
- StarCoder 2 — outclassed by Qwen 2.5 Coder
- Yi Coder — superseded
- Granite Code — not competitive
- DeepSeek R1 distilled — reasoning overhead too expensive at 16GB

---

## Performance Estimates (RTX 5060 Ti 16GB)

### Tokens Per Second by Model Size

| Model Size | Q4_K_M (tok/s) | Notes |
|------------|----------------|-------|
| 3-4B | 110-120 | Instant |
| 7B | 70-80 | Sweet spot for speed |
| 14B | 34-41 | Good balance |
| 20B (MXFP4) | 43-92 | Blackwell-optimized |
| 27B (Q4, tight) | 20-40 | Fits with Q4 on 16GB |
| 35B-A3B (MoE) | 80-100 | Only 3B active |
| 32B (partial offload) | 18-22 | 4-5 layers on CPU |

### Context Length Impact (Qwen3 8B, Q4_K_M)

| Context | tok/s | Relative |
|---------|-------|----------|
| 4K | 69.2 | 100% |
| 16K | 51.4 | 74% |
| 32K | 38.9 | 56% |
| 64K | 25.8 | 37% |

---

## Local vs Cloud: The Honest Gap

| Task | Local Best (32B) | Cloud Best (Opus 5) | Gap |
|------|------------------|---------------------|-----|
| Easy coding tasks | 72.9% | 88.0% | ~15 points |
| Hard coding tasks | ~40% | 88.0% | ~48 points |
| Code completion | ~90% | ~95% | ~5 points |
| Multi-file editing | ~40% | ~85% | ~45 points |
| SWE-bench Pro | 61.7% (Qwen3.8-27B) | 96% (Opus 5) | ~34 points |

### Where Local Wins
- Code completion, simple functions, boilerplate
- Privacy-sensitive code
- Offline/air-gapped use
- Zero marginal cost, no rate limits

### Where You Need Cloud
- Complex multi-file refactoring
- SWE-bench style real-world issues
- Large codebase understanding
- Production code generation

---

## The Hybrid Strategy

```
LOCAL (free, private, fast)
├─ Qwen3.8-27B          → Daily coding (NEW, best local)
├─ Gemma 4 12B/26B-MoE  → Fast reasoning + multimodal
├─ Qwen 2.5 Coder 14B   → Autocomplete / FIM
└─ DeepSeek Coder 7B    → Quick fixes

CLOUD (when local isn't enough)
├─ OpenCode Go ($10/mo)  → Kimi K3, Luna, Qwen3.8 Max
├─ Zen credits           → Claude Sonnet 5
└─ Direct API            → Claude Opus 5
```

---

## Quick Setup

### Ollama (Recommended)
```bash
curl -fsSL https://ollama.ai/install.sh | sh
ollama pull qwen3.6:27b
ollama pull gemma4:12b
ollama pull qwen2.5-coder:14b
```

### For Qwen3.8-27B (not on Ollama yet)
```bash
# Download GGUF from HuggingFace
huggingface-cli download unsloth/Qwen3.8-27B-GGUF Qwen3.8-27B-Q4_K_M.gguf

# Serve with llama.cpp
llama serve -m Qwen3.8-27B-Q4_K_M.gguf --n-gpu-layers 99 --ctx-size 32768 --threads 12
```

### OpenCode Config
```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "ollama/qwen3.6:27b",
  "small_model": "ollama/qwen2.5-coder:14b",
  "provider": {
    "ollama": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama (local)",
      "options": { "baseURL": "http://localhost:11434/v1" }
    }
  }
}
```

### Hardware Optimization
| Setting | Value | Why |
|---------|-------|-----|
| `--n-gpu-layers` | 999 | Offload everything to GPU |
| `--threads` | 12 | Sweet spot for Ryzen 5900XT |
| `cache-type-k` | q8_0 | Saves ~30% VRAM |
| Context size | 32768 | Balance capability/VRAM |

---

## Sources

- [unsloth/Qwen3.8-27B-GGUF](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF)
- [Ollama Library](https://ollama.ai/library)
- [Gemma 4 on Ollama](https://ollama.ai/library/gemma4)
- [Devstral Small 2](https://ollama.ai/library/devstral-small-2)
- [llama.cpp](https://github.com/ggml-org/llama.cpp)
- [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA)
