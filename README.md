#Awesome GPU for AI / LLM Inference

<p align="center">
  <img src="https://img.shields.io/badge/GPU-CUDA%20%7C%20ROCm%20%7C%20Metal-blue?style=for-the-badge" alt="GPU Platforms">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License">
  <img src="https://img.shields.io/badge/PRs-Welcome-brightgreen?style=for-the-badge" alt="PRs Welcome">
</p>

A curated guide to choosing the right GPU for AI and LLM inference workloads. Covers VRAM requirements, token/sec benchmarks, and real-world recommendations.

---

## Quick Start: How Much VRAM Do You Need?

| Model Size | FP16 (full precision) | INT4 (quantized) | Recommended GPU |
|-----------|----------------------|-------------------|-----------------|
| 7B | 14 GB | 4-5 GB | RTX 3060 12GB |
| 13B | 26 GB | 7-8 GB | RTX 3090 24GB |
| 34B | 68 GB | 18-20 GB | RTX 4090 24GB + Q4 |
| 70B | 140 GB | 35-40 GB | Dual RTX 3090 or A100 |

For detailed benchmarks, visit [bestgpuforllm.com](https://bestgpuforllm.com)

---

## GPU Benchmarks

### Token Generation Speed (tokens/sec)

| GPU | 7B Q4_K_M | 13B Q4_K_M | 34B Q4_K_M |
|-----|-----------|------------|------------|
| RTX 4090 | 45-55 | 28-35 | 12-16 |
| RTX 3090 | 38-48 | 24-30 | 10-14 |
| RTX 3080 | 30-40 | 18-24 | - |
| RTX 3060 | 22-28 | 12-16 | - |
| RX 7900 XTX | 28-35 | 14-18 | - |

*Testing conditions: Llama 2/3, context length 2048, separate prefill/decode.*

For full benchmark methodology, see our [GPU comparison tool](https://bestgpuforllm.com/compare/).

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

### Stable Diffusion / Image Generation

**Best Value**: RTX 4070 Ti Super
- 16GB VRAM, excellent for SDXL
- Good used market availability

**Dream Setup**: RTX 4090
- 24GB handles any SD configuration
- Fastest image generation at 1024×1024

### Training / Fine-tuning

**Single GPU Training**: RTX 4090 24GB
- Supports full model fine-tuning up to 7B

**Multi-GPU Setup**: RTX 3090 ×2 or ×4
- NVLink not required for inference
- For training, consider A100 or H100

---

## VRAM Calculator

Use our calculator to estimate how much VRAM you need for your model:

**Formula**: `VRAM = (Parameters × Bytes per Weight) + KV Cache + Overhead`

- FP16: `Parameters × 2 bytes`
- INT8: `Parameters × 1 byte`
- INT4: `Parameters × 0.5 bytes`
- KV Cache (FP16): `2 × Layers × HiddenSize × SequenceLength ÷ 1024` GB
- Runtime overhead: 1-3 GB depending on framework

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

For a full cost comparison, see our [TCO calculator](https://bestgpuforllm.com/tco-calculator).

---

## GPU Architecture Comparison

### NVIDIA CUDA (Recommended)

- Best LLM framework support (vLLM, Ollama, llama.cpp)
- Excellent driver ecosystem
- Broad model compatibility

### AMD ROCm (Improving)

- Better raw price/performance
- Linux-only for most features
-ROCm support improving but still behind CUDA

### Apple Silicon (MLX)

- Excellent for local inference on Mac
- Very efficient memory bandwidth
- Limited to Llama/Mistral with MLX optimization

---

## Contributing

Contributions welcome! Please read the contribution guidelines and submit PRs for:

- New benchmark results
- Additional GPU recommendations
- Corrections or updates to existing data

When adding benchmark data, please include:
- GPU model and VRAM
- Model and quantization level
- Framework and version
- Context length used
- Average tokens/sec over 100+ token generation

---

## Resources

- [GPU Comparison Tool](https://bestgpuforllm.com/compare/) - Interactive GPU comparison table
- [VRAM Calculator](https://bestgpuforllm.com/vram-calculator/) - Estimate VRAM requirements
- [TCO Calculator](https://bestgpuforllm.com/tco-calculator/) - Compare cloud vs local costs
- [LLM Buying Guide](https://bestgpuforllm.com/best-gpu-for-ollama/) - Getting started with Ollama

---

## License

MIT License - feel free to use and share.