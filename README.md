# 🚀 Awesome GPU for AI

**VRAM, LLM Compatibility, and Real-World GPU Recommendations (2026)**

A practical, developer-focused guide to choosing the right GPU for AI workloads — including local LLMs, Stable Diffusion, training, and inference.

> If you are building with AI locally, your biggest constraint is not compute — it's VRAM.

[![GPU Platforms](https://img.shields.io/badge/GPU-CUDA%20%7C%20ROCm%20%7C%20Metal-blue?style=for-the-badge)](https://developer.nvidia.com/cuda-gpus)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen?style=for-the-badge)](CONTRIBUTING.md)

---

# 🧠 TL;DR — Quick GPU Guide

| Use Case | Recommended GPU |
| -------------------- | --------------- |
| Beginner / 7B models | RTX 4060 |
| Most users / 13B–34B | RTX 4090 |
| Budget 24GB | Used RTX 3090 |
| Large models (70B+) | Cloud GPU |

---

# 📊 VRAM Requirements (LLMs)

| Model Size | Min VRAM | Comfortable VRAM | Notes |
| ---------- | -------- | ---------------- | ------------------------- |
| 7B | 6GB | 8GB | Very easy to run locally |
| 13B | 10GB | 16GB | Best balance |
| 34B | 20GB | 24GB | High-end consumer GPUs |
| 70B | 40GB+ | 48GB+ | Usually cloud / multi-GPU |

> **Rule**: VRAM determines *what you can run* — compute determines *how fast it runs*

**Why this table matters**: Most GPU guides list prices and benchmarks. This table tells you the minimum you actually need — so you don't overbuy or underbuy.

---

# 🧩 GPU Recommendations

## 🔹 Budget Tier

| GPU | VRAM | Best For |
|-----|------|----------|
| RTX 4060 | 8GB | 7B models, light SD |
| RTX 4060 Ti | 16GB | 7B–13B models |

*Good for*: 7B–13B models, light Stable Diffusion
*Limitation*: VRAM ceiling for larger models

## 🔹 Best Value Tier

| GPU | VRAM | Best For |
|-----|------|----------|
| RTX 4090 | 24GB | 13B–34B models, SDXL, training |
| RTX 4070 Ti Super | 16GB | SDXL, mid-size models |

*Best overall*: RTX 4090 — handles any consumer AI workload
*Price*: $1,500–1,800 new, $1,000–1,400 used

## 🔹 Used Value Pick

| GPU | VRAM | Best For |
|-----|------|----------|
| RTX 3090 | 24GB | 13B–34B models, excellent value |

*Why*: Still one of the best price/performance GPUs for LLM inference
*Price*: $500–700 used — hard to beat for 24GB

## 🔹 High-End / No Compromise

| GPU | VRAM | Best For |
|-----|------|----------|
| RTX 5090 | 32GB | Any model, maximum performance |
| A100/H100 | 40–80GB | Production, 70B+ models |

*Only if*: Budget is not a concern and you need maximum headroom

---

# 🤖 Model Compatibility (Quick Reference)

| Model | Min GPU | Recommended | Notes |
| --------- | ------- | --------------- | ------- |
| Llama 3.1 8B | RTX 3060 | RTX 4060 | Smooth at Q4 |
| Llama 3.1 70B | RTX 4090 ×2 | Cloud recommended | Needs ~48GB |
| Mistral 7B | RTX 3060 | RTX 4060 | Very efficient |
| Mixtral 8x7B | RTX 4070 | RTX 4090 | Epic mode needs ~24GB |
| Qwen 2.5 14B | RTX 4070 | RTX 4090 | Good balance |
| DeepSeek 33B | RTX 4090 | RTX 4090 | Q4 fits in 24GB |

> For full model compatibility, see: [bestgpuforllm.com/compare](https://bestgpuforllm.com/compare)

---

# ⚖️ Local vs Cloud: When to Use Each

## Use Local GPU When:

- You run inference daily (20+ hours/week)
- Privacy matters (your data stays on your machine)
- You want consistent performance without hourly costs
- You're actively developing / iterating

## Use Cloud GPU When:

- You need 70B+ models
- You only run inference occasionally
- You want to experiment without hardware cost
- Batch processing with variable demand

**Break-even**: If you use GPU >20 hours/week, local is cheaper long-term.

### Cloud Platforms We Recommend

| Platform | Strength | Ref Link |
|----------|----------|----------|
| [RunPod](https://app.runpod.io?r=7a4cz5kl) | Best for LLMs | Use ref `7a4cz5kl` |
| [Vast.ai](https://vast.ai) | Competitive pricing | Ask for deals |

> Full cost comparison: [TCO Calculator](https://bestgpuforllm.com/tco-calculator)

---

# ⚠️ Common Mistakes (And How to Avoid Them)

## ❌ Mistake 1: Buying for Benchmarks

Benchmarks ≠ your real workload.

- Synthetic tests run in ideal conditions
- Your actual use case has different memory patterns
- Focus on VRAM compatibility first, speed second

## ❌ Mistake 2: Ignoring VRAM Requirements

You cannot optimize around insufficient VRAM.

- A RTX 4090 with 24GB cannot run a 70B model
- Quantization helps but has quality tradeoffs
- Start with the model you want, then find the GPU that fits

## ❌ Mistake 3: Overbuying for Your Model Size

A $1,600 GPU for a 7B model is overkill.

- 7B models run fine on RTX 4060
- You don't need 24GB if you're only running 7B models
- Save money for electricity or more VRAM later

## ❌ Mistake 4: Forcing Everything Local

Cloud exists for a reason.

- 70B models are expensive to run locally
- If you only need occasional access, cloud is smarter
- Use local for daily drivers, cloud for experiments

---

# 🛠️ Framework Quick Reference

## For LLMs

| Framework | NVIDIA | AMD ROCm | Apple MLX | Best For |
|-----------|--------|----------|-----------|----------|
| [Ollama](https://ollama.com) | ✅ | ⚠️ | ✅ | Easiest setup |
| [llama.cpp](https://github.com/ggerganov/llama.cpp) | ✅ | ✅ | ❌ | Quantized models |
| [vLLM](https://docs.vllm.ai) | ✅ | ❌ | ❌ | High-throughput batching |
| [LM Studio](https://lmstudio.ai) | ✅ | ❌ | ✅ | Best GUI experience |

## For Image Generation

| Tool | NVIDIA | AMD ROCm | Best For |
|------|--------|----------|----------|
| [Automatic1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui) | ✅ | ⚠️ | Most popular |
| [ComfyUI](https://github.com/comfyanonymous/ComfyUI) | ✅ | ⚠️ | Node-based workflows |
| [Fooocus](https://github.com/lllyasviel/Fooocus) | ✅ | ❌ | Quality focus, easy use |

> For detailed framework benchmarks, visit [bestgpuforai.com](https://bestgpuforai.com)

---

# 📚 Detailed Guides (Back to Your Sites)

## From bestgpuforllm.com

- [Best GPU for Ollama](https://bestgpuforllm.com/best-gpu-for-ollama) — Getting started with Ollama
- [How Much VRAM for LLM?](https://bestgpuforllm.com/how-much-vram-for-local-llm) — Detailed VRAM breakdown
- [RunPod vs Vast.ai](https://bestgpuforllm.com/runpod-vs-vast-ai) — Cloud comparison

## From bestgpuforai.com

- [Best GPU for AI](https://bestgpuforai.com/best-gpu-for-ai) — General AI GPU guide
- [Best GPU for Stable Diffusion](https://bestgpuforai.com/best-gpu-for-stable-diffusion) — SDXL focused
- [Best GPU for Deep Learning](https://bestgpuforai.com/best-gpu-for-deep-learning) — Training recommendations

---

# 🧮 VRAM Calculator (Quick Version)

For a 7B model at FP16:
```
Weights: 7B × 2 bytes = 14 GB
KV Cache (2048 ctx): ~1 GB
Overhead: ~2 GB
Total: ~17 GB → Need 24GB GPU
```

For a 13B model at Q4_K_M:
```
Weights: 13B × 0.5 bytes = 6.5 GB
KV Cache (2048 ctx): ~2 GB
Overhead: ~2 GB
Total: ~10.5 GB → RTX 4070 or better
```

> Full interactive calculator: [VRAM Calculator](https://bestgpuforllm.com/vram-calculator)

---

# 🤝 Contributing

Contributions welcome! Please submit PRs for:

- New benchmark results (include testing conditions)
- GPU releases and pricing updates
- Model compatibility improvements
- Framework compatibility updates

**When adding benchmark data, please include**:
- GPU model and VRAM
- Model and quantization level
- Framework and version
- Context length used
- Average tokens/sec over 100+ token generation

---

# ⭐️ Why This Repo Exists

Most GPU guides have these problems:

- ❌ Too generic — not aligned with real workloads
- ❌ Optimized for affiliate clicks — not developer needs
- ❌ Outdated prices — no longer relevant

This repo focuses on:

- ✅ Real usage patterns
- ✅ Actual constraints (VRAM first)
- ✅ Practical decisions (not marketing fluff)

---

# 📌 Final Note

The best GPU is not the most expensive one.

It's the one that:

- ✅ Matches your model size
- ✅ Fits your budget
- ✅ And avoids unnecessary cost

If you get those 3 right, you're already ahead of most people building local AI setups.

---

**⭐️ If this helped you, consider starring the repo!**

[![Star on GitHub](https://img.shields.io/github/stars/airdropkalami/awesome-gpu-for-ai?style=social)](https://github.com/airdropkalami/awesome-gpu-for-ai)
[![Follow on X](https://img.shields.io/twitter/follow/thurmon_demich?style=social)](https://twitter.com/thurmon_demich)