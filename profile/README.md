<div align="center">

<img src="https://raw.githubusercontent.com/Swizzle-AI/.github/main/assets/swizzle_org_banner.jpg" alt="Swizzle AI Architectural Banner" width="100%" />

<br />

<img src="https://raw.githubusercontent.com/Swizzle-AI/swizzle-runtime/main/assets/swizzle_avatar.svg" alt="Swizzle AI Logo" width="72" />

# Swizzle AI

### *Inference that remembers what it already read.*

**Sub-40ms cached TTFT · Zero shared-memory bank conflicts · Verifiable Ed25519 receipts**

[![Swizzle Runtime v0.1.0](https://img.shields.io/badge/Swizzle_Runtime-v0.1.0_(Rust_%2B_CUDA)-c9ff3b?style=for-the-badge&logo=rust&logoColor=black)](https://github.com/Swizzle-AI/swizzle-runtime)
[![Technical Report PDF](https://img.shields.io/badge/Technical_Report-28--Page_PDF_(SWZ--TR--2026--01)-c9ff3b?style=for-the-badge&logo=adobeacrobatreader&logoColor=black)](https://github.com/Swizzle-AI/swizzle-runtime/blob/main/docs/Swizzle_Runtime_Technical_Report.pdf)
[![Live Platform](https://img.shields.io/badge/Live_Platform-swizzle--ten.vercel.app-06120d?style=for-the-badge&logo=vercel&logoColor=c9ff3b)](https://swizzle-ten.vercel.app)
[![Student Robotics Playground](https://img.shields.io/badge/Robotics_Playground-80.5_Hz-00E676?style=for-the-badge)](https://swizzle-ten.vercel.app/#student-playground)
[![Twitter Follow](https://img.shields.io/badge/@Swizzler112-1DA1F2?style=for-the-badge&logo=x&logoColor=white)](https://x.com/Swizzler112)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg?style=for-the-badge)](https://github.com/Swizzle-AI/swizzle-runtime/blob/main/LICENSE)

</div>

---

## 🌐 Ecosystem Architecture

Swizzle AI is an open-source inference stack built for **local edge GPUs, autonomous coding agents, and real-time robotics world models**.

```mermaid
flowchart TB
    subgraph Clients["Client Applications & Agents"]
        C1["Coding Agents (Continue, Aider, Cursor, Claude)"]
        C2["Robotics & World Models (80.5 Hz Control Loop)"]
        C3["OpenAI / Ollama / Anthropic SDKs"]
    end

    subgraph Edge["Control Plane & Semantic Routing"]
        GW["swizzle-gateway (Go L7 Proxy)<br/>Dual Wire (OpenAI + Anthropic) · AST-Diff Prefix Ledger"]
        RT_R["swizzle-router (Semantic Router)<br/>Matryoshka Embeddings · Warm Cache Dispatch"]
    end

    subgraph Execution["Inference Engines & Hardware Kernels"]
        SRT["swizzle-runtime (swizzle-rt)<br/>Pure Rust · RAD-1 Speculative · Warm Start · Ed25519 Receipts"]
        SWZ["swizzle (Control Plane & Scheduler)<br/>Continuous Batching · Paged KV · PD Disaggregation"]
        KRN["swizzle-kernels<br/>XOR SMEM Tiling (0 Bank Conflicts) · CUDA / Vulkan / AVX2 / Pallas"]
    end

    C1 --> GW
    C2 --> GW
    C3 --> GW
    GW --> RT_R
    GW --> SWZ
    RT_R --> SRT
    SWZ --> SRT
    SRT --> KRN
    SWZ --> KRN

    style Clients fill:#0b1c14,stroke:#335243,color:#f0fdf4
    style Edge fill:#0b1c14,stroke:#4c7863,color:#f0fdf4
    style Execution fill:#06120d,stroke:#c9ff3b,color:#f0fdf4
    style SRT fill:#102a1d,stroke:#c9ff3b,color:#c9ff3b
```

---

## 📦 Core Repositories

| Repository | Description | Stack | Status |
| :--- | :--- | :--- | :--- |
| **[`swizzle-runtime`](https://github.com/Swizzle-AI/swizzle-runtime)** | Pure-Rust GGUF local inference engine (`swizzle-rt`) with AVX2, CUDA (`sm_75`–`sm_120`), Vulkan, RAD-1 speculative decoding, and Ed25519 receipts. | Rust, CUDA, Vulkan | **v0.1.0 Live** |
| **[`swizzle`](https://github.com/Swizzle-AI/swizzle)** | Core continuous batching engine, AST-diff virtual paging (`Swizzle-Tree`), speculative decoding, and prefill-decode disaggregation. | Python, C++, PyTorch | **Main Engine** |
| **[`swizzle-gateway`](https://github.com/Swizzle-AI/swizzle-gateway)** | Sub-millisecond L7 reverse proxy supporting OpenAI (`/v1/chat/completions`) and Anthropic (`/v1/messages`) wire protocols. | Go 1.22+ | **Active** |
| **[`swizzle-kernels`](https://github.com/Swizzle-AI/swizzle-kernels)** | Hardware-roofline fused mega-kernels: XOR shared-memory bank conflict elimination, speculative verification, and TPU Pallas VMEM attention. | CUDA C++, Triton, JAX | **High Performance** |
| **[`swizzle-router`](https://github.com/Swizzle-AI/swizzle-router)** | Semantic intent router, Matryoshka embedding pipelines, and prefix-affinity multi-cluster load balancing. | Python, PyTorch | **Active** |
| **[`swizzle-python-sdk`](https://github.com/Swizzle-AI/swizzle-python-sdk)** | Official Python client library (`pip install swizzle-ai`) with speculative stream unpacking and robotics telemetry. | Python | **v0.3.0** |
| **[`swizzle-robotics`](https://github.com/Swizzle-AI/swizzle-robotics)** | Real-time robotics world models, 80.5 Hz visual servoing, 50 Hz quintic spline smoothing, and Student Robotics Playground. | Python, React, WebRTC | **Production** |

---

## 📊 Verified Local Inference Benchmarks (`swizzle-rt v0.1.0`)

📄 **[Read the Full 28-Page Technical Report (`SWZ-TR-2026-01`, PDF)](https://github.com/Swizzle-AI/swizzle-runtime/blob/main/docs/Swizzle_Runtime_Technical_Report.pdf)** — First-principles derivations, coding decisions across all 10 Rust crates, XOR-swizzled Tensor-Core GEMM proofs (`gemm_swizzle(r, b) = b ^ ((r & 7) << 4)`), Cauchy-Schwarz + IEEE-754 `Shortlist` vocabulary screening bounds, `RAD-1` ensemble speculative decoding, and head-to-head hardware telemetry.

<p align="center">
  <img src="https://raw.githubusercontent.com/Swizzle-AI/swizzle-runtime/main/assets/swizzle_benchmark_comparison.png" alt="Swizzle Runtime vs llama.cpp Benchmark Comparison" width="100%" />
</p>

---

## ⚡ Quick Start

* **One-Command Install (`swizzle-rt` Linux x86_64 CUDA 12.8)**:
  ```sh
  curl -fsSL https://raw.githubusercontent.com/Swizzle-AI/swizzle-runtime/main/install.sh | sh
  ```
* **Run via Docker (GHCR)**:
  ```sh
  docker run --rm -p 8080:8080 -v "$PWD/models:/models:ro" ghcr.io/swizzle-ai/swizzle-runtime:latest /models/model.gguf
  ```
* **Python SDK & Live Platform**: `pip install swizzle-ai` · [swizzle-ten.vercel.app](https://swizzle-ten.vercel.app)

---

<div align="center">

**Swizzle AI is open-source under the Apache 2.0 License.**

</div>
