# Awesome GPU for AI / LLM Inference

<p align="center">
  <img src="https://img.shields.io/badge/GPU-CUDA%20%7C%20ROCm%20%7C%20Metal-blue?style=for-the-badge" alt="GPU Platforms">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License">
  <img src="https://img.shields.io/badge/PRs-Welcome-brightgreen?style=for-the-badge" alt="PRs Welcome">
</p>

A curated guide to choosing the right GPU for AI and LLM inference workloads. Covers VRAM requirements, token/sec benchmarks, and real-world recommendations.

**[bestgpuforllm.com](https://bestgpuforllm.com)** — LLM-specific GPU guides and benchmarks  
**[bestgpuforai.com](https://bestgpuforai.com)** — General AI, image generation, and training GPU guides

---

## Quick Start: How Much VRAM Do You Need?

### For LLM Inference

| Model Size | FP16 (full precision) | INT4 (quantized) | Recommended GPU |
|-----------|----------------------|-------------------|-----------------|
| 7B | 14 GB | 4-5 GB | RTX 3060 12GB |
| 13B | 26 GB | 7-8 GB | RTX 3090 24GB |
| 34B | 68 GB | 18-20 GB | RTX 4090 24GB + Q4 |
| 70B | 140 GB | 35-40 GB | Dual RTX 3090 or A100 |

For detailed LLM benchmarks, visit [bestgpuforllm.com](https://bestgpuforllm.com)

### For Image Generation / Stable Diffusion

| GPU | VRAM | SDXL Performance | Best For |
|-----|------|------------------|----------|
| RTX 4090 | 24GB | ~3-4 sec/img | Production, highest quality |
| RTX 3090 | 24GB | ~4-5 sec/img | Excellent value |
| RTX 4070 Ti Super | 16GB | ~5-7 sec/img | SDXL with room for variants |
| RTX 3060 | 12GB | ~8-12 sec/img | Entry-level SDXL |

Learn more at [bestgpuforai.com/best-gpu-for-stable-diffusion](https://bestgpuforai.com/best-gpu-for-stable-diffusion)

---

## GPU Benchmarks

### LLM Token Generation Speed (tokens/sec)

| GPU | 7B Q4_K_M | 13B Q4_K_M | 34B Q4_K_M |
|-----|-----------|------------|------------|
| RTX 4090 | 45-55 | 28-35 | 12-16 |
| RTX 3090 | 38-48 | 24-30 | 10-14 |
| RTX 3080 | 30-40 | 18-24 | - |
| RTX 3060 | 22-28 | 12-16 | - |
| RX 7900 XTX | 28-35 | 14-18 | - |

*Testing conditions: Llama 2/3, context length 2048, separate prefill/decode.*

For full benchmark methodology, see our [GPU comparison tool](https://bestgpuforllm.com/compare/).

### Image Generation Speed (Stable Diffusion XL 1024×1024)

| GPU | Seconds per Image | Throughput |
|-----|------------------|------------|
| RTX 4090 | 3-4s | 15-17 img/min |
| RTX 3090 | 4-5s | 12-15 img/min |
| RTX 4070 Ti Super | 5-7s | 9-12 img/min |
| RTX 4070 | 6-8s | 7-10 img/min |
| RTX 3060 | 8-12s | 5-7 img/min |

Full benchmarks at [bestgpuforai.com/best-gpu-for-stable-diffusion](https://bestgpuforai.com/best-gpu-for-stable-diffusion)

---

## GPU Recommendations by Use Case

### Local LLM Inference

**Best Overall**: RTX 3090 24GB
- Best price/performance ratio in the used market ($500-700)
- Handles 13B models at full FP16, 34B at Q4
- Excellent availability

**Budget Pick**: RTX 3060 12GB
- Can run 7B models smoothly, 13B with quantization
- New cards still widely available

**Maximum Performance**: RTX 4090 24GB
- Fastest consumer GPU for LLM inference
- Best for developers who value speed over cost

→ [Full LLM GPU recommendations](https://bestgpuforllm.com/best-gpu-for-ollama)

### Image Generation / Stable Diffusion

**Best Value**: RTX 4070 Ti Super
- 16GB VRAM, excellent for SDXL and ComfyUI workflows
- Good used market availability

**Dream Setup**: RTX 4090
- 24GB handles any SD configuration including Flux
- Fastest image generation at 1024×1024

→ [Full SD GPU recommendations](https://bestgpuforai.com/best-gpu-for-stable-diffusion)

### AI Training / Fine-tuning

**Single GPU Training**: RTX 4090 24GB
- Supports full model fine-tuning up to 7B at FP16

**Multi-GPU Setup**: RTX 3090 ×2 or ×4
- NVLink not required for inference
- For production training, consider A100 or H100

→ [Training GPU guides](https://bestgpuforai.com/best-gpu-for-deep-learning)

---

## VRAM Calculator

Use our calculator to estimate how much VRAM you need for your model:

**Formula**: `VRAM = (Parameters × Bytes per Weight) + KV Cache + Overhead`

### Weight Precision

| Precision | Bytes per Parameter | 7B Requirements | 13B Requirements |
|-----------|--------------------|-----------------|-------------------|
| FP16 | 2 bytes | 14 GB | 26 GB |
| INT8 | 1 byte | 7 GB | 13 GB |
| INT4 | 0.5 bytes | 3.5 GB | 6.5 GB |
| Q4_K_M | ~0.5 bytes | 4-5 GB | 7-8 GB |

### KV Cache Calculation

```
KV Cache (GB) = 2 × Layers × HiddenSize × SequenceLength × BytesPerValue ÷ 1024³
```

For Llama-family models (32 layers, hidden_size 4096):
- 2048 context: ~1 GB
- 4096 context: ~2 GB
- 8192 context: ~4 GB

### Runtime Overhead

| Framework | Overhead |
|-----------|----------|
| llama.cpp | 1-2 GB |
| Ollama | 2-3 GB |
| vLLM | 2-4 GB |
| transformers + HF | 3-5 GB |

Try our interactive calculator: [bestgpuforllm.com/vram-calculator](https://bestgpuforllm.com/vram-calculator)

---

## Choosing Between Cloud vs Local

| Factor | Local GPU | Cloud (RunPod/Vast.ai) |
|--------|-----------|----------------------|
| Cost (long term) | One-time purchase | Hourly usage |
| Privacy | Full control | Data leaves machine |
| Availability | Always on | Pay for what you use |
| Performance | Know your hardware | Variable by instance |
| Best for | Daily users, developers | Experiments, batch jobs |

### Break-even Analysis

- Regular use (>20 hours/week): Local is cheaper long-term
- Occasional use (<10 hours/week): Cloud is more cost-effective
- Privacy-sensitive workloads: Always local

For a full cost comparison, see our [TCO calculator](https://bestgpuforllm.com/tco-calculator).

---

## Framework Compatibility

### LLM Frameworks

| Framework | NVIDIA | AMD ROCm | Apple MLX | Notes |
|-----------|--------|----------|-----------|-------|
| llama.cpp | ✅ | ✅ | ❌ | Best for quantized models |
| Ollama | ✅ | ⚠️ | ✅ | Easiest setup, good defaults |
| vLLM | ✅ | ❌ | ❌ | Fastest for batching |
| text-generation-webui | ✅ | ✅ | ❌ | Most flexible |
| LM Studio | ✅ | ❌ | ✅ | Great GUI, good presets |

### Image Generation

| Tool | NVIDIA | AMD ROCm | Notes |
|------|--------|----------|-------|
| Automatic1111 | ✅ | ⚠️ | Most popular, extensive ecosystem |
| ComfyUI | ✅ | ⚠️ | Node-based, extremely flexible |
| SD WebUI Forge | ✅ | ❌ | Memory-optimized |
| Fooocus | ✅ | ❌ | Simplified, quality-focused |

→ [Full framework guides](https://bestgpuforai.com)

---

## GPU Architecture Comparison

### NVIDIA CUDA (Recommended)

- Best LLM framework support (vLLM, Ollama, llama.cpp)
- Excellent driver ecosystem and CUDA optimization
- Broad model compatibility across all frameworks
- Best tensor core performance for AI workloads

### AMD ROCm (Improving)

- Better raw price/performance per dollar
- Linux-only for most features
- ROCm support improving but still behind CUDA for AI
- No vLLM support yet (critical for high-throughput)

### Apple Silicon (MLX)

- Excellent for local inference on Mac
- Very efficient unified memory bandwidth
- Limited to Llama/Mistral with MLX optimization
- No Windows/Linux equivalent yet

→ [Full architecture analysis](https://bestgpuforai.com/nvidia-vs-amd-for-ai)

---

## Latest GPU Recommendations

### Best GPUs for AI (2026)

1. **RTX 4090** — Best overall performance, 24GB VRAM
2. **RTX 3090** — Best value for 24GB, used market excellent
3. **RTX 4070 Ti Super** — Best 16GB option for SDXL
4. **RTX 3060 12GB** — Best budget entry point

→ [Full buying guide](https://bestgpuforai.com/best-gpu-for-ai)

### Budget Builds (Under $500)

1. **RTX 3060 12GB** — Best all-around budget AI GPU
2. **RTX 2060 12GB** — Good secondary option
3. **RX 6600 XT** — AMD alternative, Linux ROCm only

→ [Budget guides](https://bestgpuforai.com/best-budget-gpu-for-ai)

---

## Contributing

Contributions welcome! Please read the contribution guidelines and submit PRs for:

- New benchmark results (please include testing conditions)
- Additional GPU recommendations
- Corrections or updates to existing data
- Framework compatibility updates

When adding benchmark data, please include:
- GPU model and VRAM
- Model and quantization level
- Framework and version
- Context length used
- Average tokens/sec over 100+ token generation

---

## Resources

### LLM Tools
- [GPU Comparison Tool](https://bestgpuforllm.com/compare/) — Interactive GPU comparison table
- [VRAM Calculator](https://bestgpuforllm.com/vram-calculator/) — Estimate VRAM requirements
- [TCO Calculator](https://bestgpuforllm.com/tco-calculator/) — Compare cloud vs local costs
- [Tokens/sec Predictor](https://bestgpuforllm.com/tokens-per-second/) — Estimate inference speed

### Image Generation
- [Best GPU for Stable Diffusion](https://bestgpuforai.com/best-gpu-for-stable-diffusion)
- [Automatic1111 vs ComfyUI](https://bestgpuforai.com/automatic1111-vs-comfyui)
- [Flux GPU Requirements](https://bestgpuforai.com/best-gpu-for-flux)

### General AI
- [Best GPU for AI](https://bestgpuforai.com/best-gpu-for-ai)
- [Deep Learning GPU Guide](https://bestgpuforai.com/best-gpu-for-deep-learning)
- [Fine-tuning GPU Recommendations](https://bestgpuforai.com/best-gpu-for-fine-tuning)

---

## License

MIT License - feel free to use, share, and contribute.