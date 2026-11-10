# Contributing to Swizzle AI

Welcome! We are excited to collaborate with the open-source community to build high-performance inference engines, hardware-roofline kernels, L7 edge routing, and real-time robotics world models.

## Developer Certificate of Origin (DCO)

All commits to Swizzle AI repositories must include a signed-off-by trailer verifying that the contributor has the right to submit the work under the Apache 2.0 license:

```bash
git commit -s -m "feat: your descriptive commit message"
```

## Pull Request Guidelines

1. **Focused PRs**: Each pull request should address a single feature, bugfix, or architectural optimization.
2. **Quality & Tests**: Include unit tests (pytest for Python, `go test` for Go, nvcc test harnesses for CUDA).
3. **Hardware Roofline**: Performance-sensitive PRs in `swizzle-kernels` or `swizzle` must include benchmark metrics (latency, arithmetic intensity, SRAM bank conflict rate).
4. **Code Style**: Format Go code with `gofmt -s`, Python code with `ruff` or `black`, and CUDA code with `clang-format`.

Thank you for contributing to the future of high-speed LLM inference!
