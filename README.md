# Awesome GPU for AI

**LLM-first GPU Guide, VRAM Requirements, Benchmarks, and AI Workload Compatibility**

A practical GPU reference for AI builders — with a strong focus on local LLM inference, VRAM requirements, model compatibility, and GPU selection for real-world AI workloads.

> The first question for any local AI project: *Does it fit in VRAM?*

[![GPU Platforms](https://img.shields.io/badge/GPU-CUDA%20%7C%20ROCm%20%7C%20Metal-blue?style=for-the-badge)](https://developer.nvidia.com/cuda-gpus)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=for-the-badge)](CONTRIBUTING.md)
[![Last Updated](https://img.shields.io/badge/Updated-2026--04-orange?style=for-the-badge)]()

---

## 🔥 Start Here — Choose Your Path

| I'm building... | Go to... | Why |
|-----------------|----------|-----|
| **Local LLMs** | 👇 [awesome-gpu-for-llm](https://github.com/airdropkalami/awesome-gpu-for-llm) | LLM-specific VRAM tables, model compatibility, tokens/sec benchmarks |
| **Image Generation / SD** | See Section 7 | SDXL benchmarks, tool comparisons |
| **Training / Fine-tuning** | See Section 7 | Training GPU recommendations |
| **Not sure what I need** | See Section 1 | Quick decision guide |

**This repo** covers general AI workloads + links to the specialized LLM repo.

---

## 1. Quick Start: GPU for Local LLMs

| Scenario | Recommended GPU | Why |
|---|---|---|
| 7B models / beginner | RTX 4060 / 4060 Ti | Affordable entry point |
| 13B models | RTX 4070 Ti Super / RTX 4090 | Better VRAM headroom |
| 34B models | RTX 4090 / RTX 3090 | 24GB VRAM class |
| 70B+ models | Cloud GPU / multi-GPU | Local single-GPU gets expensive |

> **For detailed LLM benchmarks and model compatibility → [awesome-gpu-for-llm](https://github.com/airdropkalami/awesome-gpu-for-llm)**

---

## 2. LLM VRAM Requirements

| Model Size | Minimum VRAM | Comfortable VRAM | Practical Recommendation |
|---|---:|---:|---|
| 7B | 6–8GB | 8–12GB | Entry GPU is enough |
| 13B | 10–12GB | 16GB | Mid-range GPU |
| 34B | 20GB | 24GB | RTX 3090 / 4090 class |
| 70B | 40GB+ | 48–80GB+ | Cloud or multi-GPU |

**The Rule**: VRAM determines *what you can run* — compute determines *how fast it runs*.

**Quick Formula**:
```
VRAM = Model Weights + KV Cache + Runtime Overhead

FP16: Parameters × 2 bytes
INT8:  Parameters × 1 byte
Q4:    Parameters × 0.5 bytes
```

---

## 3. GPU Recommendation Tiers

### Entry Tier — RTX 4060 / RTX 4060 Ti

| Spec | Value |
|------|-------|
| VRAM | 8–16GB |
| Best for | 7B models, testing LLMs |
| Price | $300–400 new |
| Can run | Llama 3.1 8B, Mistral 7B |

### Best Value — RTX 4070 Ti Super

| Spec | Value |
|------|-------|
| VRAM | 16GB |
| Best for | 13B models, SDXL |
| Price | $700–900 |
| Why | Excellent VRAM/price ratio |

### Best Overall — RTX 4090

| Spec | Value |
|------|-------|
| VRAM | 24GB |
| Best for | 13B–34B models, any AI workload |
| Price | $1,500–1,800 new, $1,000–1,400 used |
| Why | Dominates all consumer AI workloads |

### Budget 24GB — Used RTX 3090

| Spec | Value |
|------|-------|
| VRAM | 24GB |
| Best for | 13B–34B models |
| Price | $500–700 used |
| Why | Best price/performance in used market |

### High-End — RTX 5090

| Spec | Value |
|------|-------|
| VRAM | 32GB |
| Best for | Any single-GPU workload |
| Price | $2,000+ |

---

## 4. Model Compatibility Matrix

| Model | Type | Min GPU | Recommended | Quantization |
| --------- | ---- | ------- | --------------- | ------------- |
| Llama 3.1 8B | LLM | RTX 3060 | RTX 4060 | FP16, Q4, Q8 |
| Llama 3.1 70B | LLM | RTX 4090 ×2 | Cloud | Q4, Q8 |
| Mistral 7B | LLM | RTX 3060 | RTX 4060 | FP16, Q4 |
| Mixtral 8x7B | LLM | RTX 4070 | RTX 4090 | Q4 |
| Qwen 2.5 14B | LLM | RTX 4070 | RTX 4090 | FP16, Q4 |
| DeepSeek 33B | LLM | RTX 4090 | RTX 4090 | Q4 |
| SDXL 1024×1024 | SD | RTX 4070 | RTX 4090 | 16GB min |
| Flux Dev | SD | RTX 4090 | RTX 4090 24GB | Needs 20GB+ |

> For full interactive LLM compatibility: **[awesome-gpu-for-llm](https://github.com/airdropkalami/awesome-gpu-for-llm)** → Model Compatibility Matrix

---

## 5. Benchmark Reference

### Tokens/sec — LLM Inference (Q4_K_M, 2048 context)

> *Full benchmark dataset available in [awesome-gpu-for-llm](https://github.com/airdropkalami/awesome-gpu-for-llm)*

| GPU | VRAM | 7B | 13B | 34B | 70B |
|-----|------|---:|---:|---:|---:|
| RTX 4060 | 8GB | 35 | 18 | ❌ | ❌ |
| RTX 4070 | 12GB | 45 | 22 | ❌ | ❌ |
| RTX 4090 | 24GB | 80 | 45 | 18 | ⚠️ |
| RTX 3090 | 24GB | 70 | 40 | 15 | ⚠️ |
| A100 | 80GB | 120 | 80 | 40 | 25 |

> **Notes**: Q4_K_M quantization. Framework: llama.cpp. Values vary by model and system config.

### Image Generation — Stable Diffusion XL (1024×1024, DPM++ 2M Karras)

| GPU | VRAM | Seconds/img | Throughput |
|-----|------|-------------|------------|
| RTX 4090 | 24GB | 3–4s | 15–17 img/min |
| RTX 3090 | 24GB | 4–5s | 12–15 img/min |
| RTX 4070 Ti Super | 16GB | 5–7s | 9–12 img/min |
| RTX 3060 | 12GB | 8–12s | 5–7 img/min |

> **Detailed SD benchmarks**: [bestgpuforai.com/best-gpu-for-stable-diffusion](https://bestgpuforai.com/best-gpu-for-stable-diffusion)

---

## 6. Cloud vs Local Decision

### Use Local GPU When:

- ✅ Daily inference usage (20+ hours/week)
- ✅ Privacy is critical (data never leaves your machine)
- ✅ Consistent, predictable performance
- ✅ Active development requiring fast iteration

### Use Cloud GPU When:

- ✅ Running 70B+ models regularly
- ✅ Occasional burst compute needs
- ✅ Want flexibility to switch GPU types
- ✅ Experimenting with various model sizes

**Break-even**: Local cheaper if you use GPU >20 hours/week.

| Provider | Strength | Ref |
|----------|----------|-----|
| [RunPod](https://app.runpod.io?r=7a4cz5kl) | Best for LLMs | Use ref `7a4cz5kl` |
| [Vast.ai](https://vast.ai) | Competitive pricing | Ask for deals |

> Full TCO analysis: [bestgpuforllm.com/tco-calculator](https://bestgpuforllm.com/tco-calculator)

---

## 7. General AI Workloads

### Training & Fine-tuning

| Workload | Min GPU | Recommended |
|----------|---------|-------------|
| Fine-tune 7B (FP16) | RTX 4090 24GB | RTX 4090 |
| Fine-tune 13B (Q4) | RTX 4090 24GB | RTX 4090 ×2 |
| Full training runs | A100/H100 | Multi-GPU setup |

> **Guide**: [bestgpuforai.com/best-gpu-for-deep-learning](https://bestgpuforai.com/best-gpu-for-deep-learning)

### Image Generation

| Tool | Best GPU | Notes |
|------|----------|-------|
| Automatic1111 | RTX 4070+ | Most popular, large ecosystem |
| ComfyUI | RTX 4070+ | Node-based, flexible |
| Fooocus | RTX 4060+ | Simplified UI, quality focus |
| SD WebUI Forge | RTX 3060+ | Memory-optimized |

> **Guide**: [bestgpuforai.com/best-gpu-for-stable-diffusion](https://bestgpuforai.com/best-gpu-for-stable-diffusion)

### Embedded / Edge AI

| Use Case | Recommended |
|----------|-------------|
| Jetson Orin | NVIDIA Jetson AGX Orin |
| Raspberry Pi + Hailo | Hailo-8L |
| Apple Neural Engine | Apple M-series chip |

---

## 8. Framework Quick Reference

### For LLMs

| Framework | Best For | NVIDIA | AMD ROCm | Apple MLX |
|-----------|----------|--------|----------|-----------|
| [Ollama](https://ollama.com) | Easiest setup | ✅ | ⚠️ | ✅ |
| [llama.cpp](https://github.com/ggerganov/llama.cpp) | Quantized models | ✅ | ✅ | ❌ |
| [vLLM](https://docs.vllm.ai) | High-throughput | ✅ | ❌ | ❌ |
| [LM Studio](https://lmstudio.ai) | GUI experience | ✅ | ❌ | ✅ |
| [Open WebUI](https://openwebui.com) | Self-hosted ChatGPT | ✅ | ⚠️ | ✅ |

> **Detailed framework comparison**: [awesome-gpu-for-llm](https://github.com/airdropkalami/awesome-gpu-for-llm) → Framework Support

---

## Links to Detailed Guides

### LLM Resources → [awesome-gpu-for-llm](https://github.com/airdropkalami/awesome-gpu-for-llm)

| Guide | What It Covers |
| ----- | -------------- |
| [Best GPU for Ollama](https://bestgpuforllm.com/best-gpu-for-ollama) | Ollama setup and GPU recommendations |
| [How Much VRAM for LLM?](https://bestgpuforllm.com/how-much-vram-for-local-llm) | Detailed VRAM breakdown |
| [RunPod vs Vast.ai](https://bestgpuforllm.com/runpod-vs-vast-ai) | Cloud GPU comparison |
| [GPU Comparison Tool](https://bestgpuforllm.com/compare) | Interactive GPU table |
| [VRAM Calculator](https://bestgpuforllm.com/vram-calculator) | Estimate requirements |
| [Tokens/sec Predictor](https://bestgpuforllm.com/tokens-per-second) | Speed estimation |

### General AI Resources → [bestgpuforai.com](https://bestgpuforai.com)

| Guide | What It Covers |
| ----- | -------------- |
| [Best GPU for AI](https://bestgpuforai.com/best-gpu-for-ai) | General AI GPU guide |
| [Best GPU for Stable Diffusion](https://bestgpuforai.com/best-gpu-for-stable-diffusion) | SDXL and Flux |
| [Best GPU for Deep Learning](https://bestgpuforai.com/best-gpu-for-deep-learning) | Training and fine-tuning |
| [Automatic1111 vs ComfyUI](https://bestgpuforai.com/automatic1111-vs-comfyui) | Tool comparison |
| [Nvidia vs AMD for AI](https://bestgpuforai.com/nvidia-vs-amd-for-ai) | Platform choice |

---

## ⚠️ Common Mistakes

### ❌ Buying for Benchmarks Instead of Real Workloads

Synthetic benchmarks run in ideal conditions. Your actual AI workload has different memory patterns.

**Fix**: Focus on VRAM compatibility first, then speed.

### ❌ Ignoring VRAM Requirements

You cannot optimize around insufficient VRAM.

**Fix**: Know your target model's VRAM needs before buying.

### ❌ Overbuying for Your Model Size

A $1,600 GPU for 7B models is wasteful.

**Fix**: Match GPU to your actual model size. Upgrade when you hit limits.

### ❌ Forcing Everything Local

Cloud exists for valid reasons.

**Fix**: Use local for daily drivers, cloud for experiments and large models.

---

## Contributing

Contributions welcome! Please submit PRs for:

- New benchmark results (include testing conditions)
- GPU releases and pricing updates
- Model compatibility improvements
- Framework updates

**When adding benchmark data, please include**:
- GPU model and VRAM
- Model and quantization level
- Framework and version
- Context length used
- Average tokens/sec over 100+ token generation

---

## Why This Repo Exists

Most GPU guides are:

- ❌ Too generic — not aligned with real AI workloads
- ❌ Marketing-focused — optimized for affiliate clicks
- ❌ Outdated — prices and availability change fast

This repo focuses on:

- ✅ Real usage patterns developers actually encounter
- ✅ Actual constraints (VRAM first, compute second)
- ✅ Practical decisions (not theoretical benchmarks)

---

## TL;DR — Final Decision Guide

| If you... | Do this |
|-----------|---------|
| Just testing LLMs | RTX 4060 |
| Run 7B–13B daily | RTX 4070 Ti Super |
| Need 13B–34B performance | RTX 4090 |
| Want 24GB on budget | Used RTX 3090 |
| Need 70B+ models | Cloud GPU |
| Do heavy SD/training | RTX 4090 ×2 or A100 |

**The best GPU is not the most expensive one. It's the one that fits your model in VRAM, matches your budget, and doesn't overbuy for your actual needs.**

---

**⭐️ If this helped, consider starring the repo!**

[![Star on GitHub](https://img.shields.io/github/stars/airdropkalami/awesome-gpu-for-ai?style=social)](https://github.com/airdropkalami/awesome-gpu-for-ai)
[![Follow on X](https://img.shields.io/twitter/follow/thurmon_demich?style=social)](https://twitter.com/thurmon_demich)