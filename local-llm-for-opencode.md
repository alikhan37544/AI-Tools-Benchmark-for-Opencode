# Local LLM Analysis for OpenCode

> **Updated: August 19, 2026** | Hardware: Ryzen 9 5900XT (16C) + RTX 5060 Ti 16GB + 64GB DDR4

## TL;DR

| Role | Model | Quant | VRAM | Speed | Quality |
|------|-------|-------|------|-------|---------|
| **Daily Driver** | Qwen 3.6 35B-A3B | Q3_K_M | ~16.6 GB | ~80-100 tok/s | ~88% of frontier |
| **Autocomplete/FIM** | Qwen 2.5 Coder 14B | Q4_K_M | ~9 GB | ~34 tok/s | Best local FIM |
| **Fast Fallback** | Qwen 2.5 Coder 7B | Q5_K_M | ~5.5 GB | ~70-80 tok/s | Good for quick tasks |
| **Max Quality** | Qwen3-Coder 32B | Q4_K_M | ~18.4 GB | ~22 tok/s (offload) | Best local coding |

---

## Your Hardware at a Glance

| Component | Spec | LLM Relevance |
|-----------|------|---------------|
| **CPU** | Ryzen 9 5900XT (16C/32T, Zen 3) | Good for CPU offload, AVX2 (no AVX-512) |
| **GPU** | RTX 5060 Ti 16GB GDDR7 | Blackwell arch, 448 GB/s, native FP4 |
| **RAM** | 64GB DDR4 | Can hold ~70B model weights for offload |
| **PSU** | 1000W+ | No power throttling |
| **Cooling** | 9-fan case | Can sustain full throttle indefinitely |

### What Fits Where

| Location | Max Model Size | Notes |
|----------|---------------|-------|
| **GPU only (16GB VRAM)** | ~20B at Q4_K_M, ~27B at IQ3_XXS | Fastest inference |
| **GPU + CPU offload (80GB total)** | ~34B-70B at Q4 | Slower, layers split |
| **CPU only (64GB RAM)** | ~70B at Q3_K_M (~36GB weights) | Slowest, DDR4 bottleneck |

---

## Recommended Models

### Tier 1: Best for OpenCode (16GB VRAM)

#### Qwen 3.6 35B-A3B (MoE) — The New Default
- **Params:** 35B total, 3B active per token (MoE)
- **Quantization:** Q3_K_M (~16.6 GB VRAM)
- **Speed:** ~80-100 tok/s
- **SWE-bench Verified:** 73.4%
- **Context:** 262K tokens
- **License:** Apache 2.0
- **Why:** MoE means only 3B params active per token, so it's fast despite being 35B total. Fits in 16GB at Q3_K_M. Strong tool calling support.

#### Qwen 2.5 Coder 14B — The FIM King
- **Params:** 14B
- **Quantization:** Q4_K_M (~9 GB VRAM)
- **Speed:** ~34 tok/s
- **HumanEval:** 89.9%
- **Context:** 128K tokens
- **License:** Apache 2.0
- **Why:** Best local model for Fill-in-the-Middle (autocomplete). Only current-gen model with full FIM support. Use for tab-complete in IDE.

#### Qwen3-Coder 32B — Max Local Quality
- **Params:** 32B
- **Quantization:** Q4_K_M (~18.4 GB — needs partial CPU offload)
- **Speed:** ~22 tok/s (4-5 layers offloaded)
- **HumanEval+:** 84.1%
- **Context:** 256K tokens
- **License:** Apache 2.0
- **Why:** Best coding quality you can get locally. Usable with partial offload but slower.

### Tier 2: Strong Alternatives

| Model | Params | Quant | VRAM | Speed | Best For |
|-------|--------|-------|------|-------|----------|
| **DeepSeek Coder V2 Lite** | 16B (2.4B active) | Q4_K_M | ~10 GB | ~45 tok/s | Fast MoE coding |
| **Gemma 4 12B** | 12B | Q4_K_M | ~8 GB | ~50+ tok/s | Generalist + coding |
| **Codestral 22B** | 22B | Q4_K_M | ~14 GB | ~22 tok/s | FIM alternative |
| **Phi-4 14B** | 14B | Q6_K | ~11.5 GB | ~49 tok/s | Math/STEM tasks |
| **Llama 3.3 14B** | 14B | Q5_K_M | ~10 GB | ~58 tok/s | General reasoning |

### Tier 3: Budget/Fast

| Model | Params | Quant | VRAM | Speed | Best For |
|-------|--------|-------|------|-------|----------|
| **Qwen 2.5 Coder 7B** | 7B | Q5_K_M | ~5.5 GB | ~70-80 tok/s | Quick tasks, autocomplete |
| **DeepSeek-Coder 6.7B** | 6.7B | Q4_K_M | ~4.5 GB | ~100 tok/s | Ultra-fast coding |
| **Phi-3 3.8B** | 3.8B | Q4_K_M | ~2.3 GB | ~110-120 tok/s | Instant responses |

---

## Performance Estimates (RTX 5060 Ti 16GB)

### Tokens Per Second by Model Size

| Model Size | Q4_K_M (tok/s) | Q8_0 (tok/s) | Notes |
|------------|----------------|--------------|-------|
| **3-4B** | 110-120 | 80-90 | Instant, great for autocomplete |
| **7B** | 70-80 | 55-65 | Sweet spot for speed |
| **14B** | 34-41 | 25-30 | Good balance |
| **20B (MXFP4)** | 43-92 | N/A | Blackwell-optimized |
| **27B (IQ3_XXS)** | 20-30 | N/A | Tight fit, quality tradeoff |
| **35B-A3B (MoE)** | 80-100 | N/A | Only 3B active, very fast |
| **32B (partial offload)** | 18-22 | N/A | 4-5 layers on CPU |

### Context Length Impact (Qwen3 8B, Q4_K_M)

| Context | tok/s | Relative |
|---------|-------|----------|
| 4K | 69.2 | 100% |
| 16K | 51.4 | 74% |
| 32K | 38.9 | 56% |
| 64K | 25.8 | 37% |

---

## Inference Software

### Recommended: Ollama (Easiest)

```bash
# Install
curl -fsSL https://ollama.ai/install.sh | sh

# Pull models
ollama pull qwen3-coder:32b
ollama pull qwen2.5-coder:14b

# Auto-starts on http://localhost:11434
```

### Alternative: llama.cpp (Best Performance)

```bash
# Build with CUDA
git clone https://github.com/ggml-org/llama.cpp
cd llama.cpp
cmake -B build -DGGML_CUDA=ON -DCMAKE_CUDA_ARCHITECTURES=120a-real
cmake --build build -j$(nproc)

# Serve
./build/bin/llama serve \
  -hf unsloth/Qwen3-Coder-32B-GGUF:Q4_K_M \
  --n-gpu-layers 99 \
  --ctx-size 32768
```

### OpenCode Config

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "ollama/qwen3-coder:32b",
  "small_model": "ollama/qwen2.5-coder:14b",
  "provider": {
    "ollama": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama (local)",
      "options": {
        "baseURL": "http://localhost:11434/v1"
      },
      "models": {
        "qwen3-coder:32b": { "name": "Qwen3-Coder 32B" },
        "qwen2.5-coder:14b": { "name": "Qwen 2.5 Coder 14B" }
      }
    }
  }
}
```

---

## Local vs Cloud: The Honest Gap

| Task | Local Best (32B) | Cloud Best (Opus 5) | Gap |
|------|------------------|---------------------|-----|
| Easy coding tasks | 72.9% | 88.0% | ~15 points |
| Hard coding tasks | 40.0% | 88.0% | ~48 points |
| Code completion | ~90% | ~95% | ~5 points |
| Multi-file editing | ~40% | ~85% | ~45 points |
| HumanEval (synthetic) | ~90% | ~95% | ~5 points |

### Where Local Models Excel
- Code completion (single-line/function)
- Simple function generation
- Boilerplate/templates
- Code explanation
- Privacy-sensitive code
- Offline/air-gapped use
- Zero marginal cost

### Where You Need Cloud Models
- Complex multi-file refactoring
- SWE-bench style real-world issues
- Large codebase understanding (100K+ context with reasoning)
- Production code generation
- Cross-language projects
- Complex debugging across multiple files

---

## The Sweet Spot Strategy

```
┌─────────────────────────────────────────────────┐
│  LOCAL (free, private, fast)                     │
│  ├─ Qwen 2.5 Coder 14B → Autocomplete/FIM      │
│  ├─ Qwen 3.6 35B-A3B  → Daily coding chat      │
│  └─ DeepSeek Coder 7B  → Quick fixes            │
│                                                  │
│  CLOUD (when local isn't enough)                 │
│  ├─ OpenCode Go ($10/mo) → Kimi K3, Luna        │
│  ├─ Zen credits          → Claude Sonnet 5      │
│  └─ Direct API           → Claude Opus 5        │
└─────────────────────────────────────────────────┘
```

---

## Hardware Optimization Tips

1. **Set `-ngl 999`** in llama.cpp to offload all layers to GPU
2. **Use `-t 12`** for threads (sweet spot for Ryzen 5900XT, not all 32)
3. **Enable KV cache quantization** (`cache-type-k q8_0`) to save ~30% VRAM
4. **Use MXFP4 quantization** on Blackwell for best quality/size ratio
5. **Monitor with `nvidia-smi`** — leave 1-2GB headroom for KV cache
6. **DDR4 impact:** Only matters for CPU-offloaded layers (~11% of GPU speed)

---

## Sources

- [llama.cpp benchmarks](https://github.com/ggml-org/llama.cpp)
- [Ollama model library](https://ollama.ai/library)
- [Qwen 2.5 Coder](https://huggingface.co/Qwen/Qwen2.5-Coder)
- [Aider leaderboard](https://aider.chat/docs/leaderboards/)
- [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA)
- [Hardware Corner RTX 5060 Ti benchmarks](https://hardware-corner.net)
