# Swizzle AI

<div align="center">

### Inference that remembers what it already read.

**Sub-40ms cached TTFT · Zero shared-memory bank conflicts · 10× cheaper prefix billing**

[![Live Platform](https://img.shields.io/badge/Live_Platform-swizzle--ten.vercel.app-c9ff3b?style=for-the-badge&logo=vercel&logoColor=black)](https://swizzle-ten.vercel.app)
[![Student Robotics Playground](https://img.shields.io/badge/Robotics_%26_World_Models-Student_Playground_(80.5_Hz)-00E676?style=for-the-badge)](https://swizzle-ten.vercel.app/#student-playground)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg?style=for-the-badge)](LICENSE)

---

</div>

## 🌐 The Swizzle Open-Source Ecosystem

Swizzle AI is a modular, high-performance inference ecosystem engineered specifically for autonomous coding agents, heavy reasoning LLMs, and real-time robotics world models.

```text
                                  ┌──────────────────────────┐
                                  │   Client Applications    │
                                  │ (Cursor, Claude, Robots) │
                                  └─────────────┬────────────┘
                                                │
                                                ▼
                                  ┌──────────────────────────┐
                                  │     swizzle-gateway      │
                                  │ (Go L7 Reverse Proxy)    │
                                  │ • Dual Wire (OpenAI/Anth)│
                                  │ • AST-Diff Prefix Ledger │
                                  └─────────────┬────────────┘
                                                │
                     ┌──────────────────────────┴──────────────────────────┐
                     ▼                                                     ▼
       ┌───────────────────────────┐                         ┌───────────────────────────┐
       │      swizzle-router       │                         │          swizzle          │
       │ (Semantic Router & Vector)│                         │ (Core Engine & Scheduler) │
       │ • Matryoshka Embeddings   │                         │ • Continuous Batching     │
       │ • Warm Cache Dispatch     │                         │ • Paged KV Block Manager  │
       └───────────────────────────┘                         └─────────────┬─────────────┘
                                                                           │
                                                                           ▼
                                                             ┌───────────────────────────┐
                                                             │      swizzle-kernels      │
                                                             │ (Hardware Fused Kernels)  │
                                                             │ • XOR Attention (0 Banks) │
                                                             │ • Speculative Verify Tile │
                                                             │ • TPU Pallas VMEM Kernel  │
                                                             └───────────────────────────┘
```

---

## 📦 Core Repositories

| Repository | Description | Stack | Status |
| :--- | :--- | :--- | :--- |
| **[`swizzle`](https://github.com/Swizzle-AI/swizzle)** | Core continuous batching inference engine, AST-diff virtual paging, speculative decoding, and prefill-decode disaggregation. | Python, C++, PyTorch | **Main Engine** |
| **[`swizzle-gateway`](https://github.com/Swizzle-AI/swizzle-gateway)** | Ultra-low latency (<1ms) L7 reverse proxy supporting both OpenAI (`/v1/chat/completions`) and Anthropic (`/v1/messages`) wire protocols. | Go 1.22+ | **Active** |
| **[`swizzle-kernels`](https://github.com/Swizzle-AI/swizzle-kernels)** | Hardware-roofline fused mega-kernels: XOR shared-memory bank conflict elimination, speculative verification, and TPU v5e Pallas VMEM attention. | CUDA C++, Triton, JAX/Pallas | **High Performance** |
| **[`swizzle-router`](https://github.com/Swizzle-AI/swizzle-router)** | Semantic intent router, domain-adapted Matryoshka embedding pipelines, and prefix-affinity multi-cluster load balancing. | Python, PyTorch | **Active** |
| **[`swizzle-python-sdk`](https://github.com/Swizzle-AI/swizzle-python-sdk)** | Official Python client library (`pip install swizzle-ai`) with automatic speculative stream unpacking and robotics telemetry. | Python | **v0.3.0** |
| **[`swizzle-robotics`](https://github.com/Swizzle-AI/swizzle-robotics)** | Real-time robotics world models, 80.5 Hz visual servoing, 50Hz quintic spline smoothing, and Student Robotics Playground. | Python, React, WebRTC | **Production** |

---

## ⚡ The 3 Core Pillars

1. **`Swizzle-Draft` (Speculative Decoding)**: In-memory Prompt-Trie N-gram lookahead operating at the edge paired with parallel forward verification on the worker ($98.7	ext{ tok/s}$, $2.76	imes$ speedup).
2. **`Swizzle-Tree` (AST-Diff Virtual Paging)**: Syntactic semantic block decomposition packs unchanged AST functions into a contiguous warm prefix, achieving **$89.6\%$ KV cache reuse** (vs $48\%$ linear).
3. **`Swizzle-PD` (Prefill-Decode Disaggregation)**: Dedicated H100 prefill compute decoupled from A100/MI300X decode nodes over $100	ext{ GB/s}$ RoCEv2/InfiniBand RDMA ($99.9\%$ ITL jitter drop).

---

## 🚀 Getting Started

* **Explore the Live Platform**: [https://swizzle-ten.vercel.app](https://swizzle-ten.vercel.app)
* **Student Robotics Playground**: [https://swizzle-ten.vercel.app/#student-playground](https://swizzle-ten.vercel.app/#student-playground)
* **Install Python SDK**:
  ```bash
  pip install swizzle-ai
  ```

---

<div align="center">

**Swizzle AI is open-source under the Apache 2.0 License.**

</div>
