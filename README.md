# Awesome LLM Infrastructure [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Curated production-grade tools for running LLMs at scale — runtimes, clients, observability, safety, agents, and finance.

Built and maintained by [@Mattbusel](https://github.com/Mattbusel).

This list focuses on **production reliability**: tools that handle failure gracefully, expose structured observability, and have been validated under real workloads. Each entry earns its place — no vaporware, no abandoned experiments.

## Contents

- [Async Runtimes & Orchestration](#async-runtimes--orchestration)
- [LLM Clients & SDKs](#llm-clients--sdks)
- [Streaming & Token Processing](#streaming--token-processing)
- [Retry, Circuit Breakers & Resilience](#retry-circuit-breakers--resilience)
- [Observability & Tracing](#observability--tracing)
- [Safety & Hallucination Detection](#safety--hallucination-detection)
- [Agent Memory & State](#agent-memory--state)
- [Benchmarking & Evaluation](#benchmarking--evaluation)
- [Cost & Budget Management](#cost--budget-management)
- [C++ Single-Header Libraries](#c-single-header-libraries)
- [Quantitative Finance + LLMs](#quantitative-finance--llms)
- [WebAssembly & Edge](#webassembly--edge)
- [Learning Resources](#learning-resources)

---

## ⚙️ Async Runtimes & Orchestration

End-to-end request pipelines with backpressure, deduplication, circuit breaking, and structured concurrency.

- [**tokio-prompt-orchestrator**](https://github.com/Mattbusel/tokio-prompt-orchestrator) ⭐ — Aerospace-grade async LLM orchestration pipeline built on Tokio. Features lock-free SPSC streaming, circuit breakers, retry with exponential backoff, RAG integration, and a 1.5:1 test-to-production ratio enforced by CI. `Rust` `tokio` `production`
- [**HelixRouter**](https://github.com/Mattbusel/HelixRouter) ⭐ — Intelligent request router for multi-provider LLM deployments. Routes based on latency, cost, and model capability with automatic failover. `Rust` `routing` `multi-provider`
- [**langchain-rust**](https://github.com/Abraxas-365/langchain-rust) — Full LangChain implementation in Rust. Chains, agents, memory, and tool use with async-first design. `Rust` `agents` `chains`
- [**rig**](https://github.com/0xPlaygrounds/rig) — Ergonomic Rust framework for building LLM-powered agents and pipelines. Clean API surface, provider-agnostic, production-tested. `Rust` `agents` `ergonomic`
- [**async-openai**](https://github.com/64bit/async-openai) — Idiomatic async Rust bindings for the OpenAI API. Streaming, function calling, embeddings, and fine-tuning all supported. `Rust` `openai` `async`
- [**litechain**](https://github.com/rogeriochaves/litechain) — Minimal composable pipeline framework for LLMs. Focuses on streaming-first composition with typed outputs. `Python` `streaming` `composable`

---

## 🔌 LLM Clients & SDKs

Provider SDKs and abstraction layers for building model-agnostic applications.

- [**tokio-llm**](https://github.com/Mattbusel/tokio-llm) ⭐ — Purpose-built async LLM client for Tokio environments. Unified interface across OpenAI, Anthropic, and Mistral with structured error types, retry hooks, and token counting. `Rust` `multi-provider` `typed`
- [**llm-cpp**](https://github.com/Mattbusel/llm-cpp) ⭐ — 26 production-ready C++ single-header libraries for LLM infrastructure. Zero external dependencies, MSVC/GCC/Clang compatible, AVX2/AVX-512 optimized hot paths. `C++` `single-header` `simd`
- [**async-openai**](https://github.com/64bit/async-openai) — The reference Rust implementation of the OpenAI API. Battle-tested in production, well-maintained, full feature coverage. `Rust` `openai`
- [**anthropic-sdk-python**](https://github.com/anthropics/anthropic-sdk-python) — Official Python SDK for the Anthropic Claude API. Sync and async modes, streaming, tool use, and vision. `Python` `anthropic` `official`
- [**openai-node**](https://github.com/openai/openai-node) — Official Node.js/TypeScript SDK for OpenAI. Full API coverage including Assistants, streaming, and structured outputs. `TypeScript` `openai` `official`
- [**mistral.rs**](https://github.com/EricLBuehler/mistral.rs) — Blazing-fast local inference engine for Mistral, Llama, Phi, and Gemma. ISQ quantization, PagedAttention, speculative decoding. `Rust` `inference` `local`
- [**ollama**](https://github.com/ollama/ollama) — Run large language models locally with a simple REST API. Model management, custom modelfiles, and OpenAI-compatible endpoints. `Go` `local` `api`

---

## 🌊 Streaming & Token Processing

Low-latency token streaming, SPSC pipelines, and incremental decode.

- [**Every-Other-Token**](https://github.com/Mattbusel/Every-Other-Token) ⭐ — Research implementation and production toolkit for token-level streaming compression. Validates the every-other-token hypothesis for bandwidth reduction without semantic loss. 23 stars. `Python` `research` `compression`
- [**llm-stream**](https://github.com/Mattbusel/llm-cpp) ⭐ — C++ streaming pipeline component from the llm-cpp suite. Lock-free SPSC ring buffer with OHLCV tick ingestion and Lorentz-transform coordinate normalization for financial token streams. `C++` `spsc` `lock-free`
- [**llm.c**](https://github.com/karpathy/llm.c) — Andrej Karpathy's minimal C/CUDA implementation of GPT-2 training and inference. Single file, fully commented, indispensable for understanding the mechanics. `C` `cuda` `educational`
- [**candle**](https://github.com/huggingface/candle) — HuggingFace's minimalist ML framework in Rust. CUDA support, WASM builds, no Python runtime required, used in production at HF. `Rust` `inference` `cuda`
- [**vllm**](https://github.com/vllm-project/vllm) — High-throughput LLM serving engine with PagedAttention. Continuous batching, tensor parallelism, OpenAI-compatible API. The production standard for GPU inference. `Python` `cuda` `serving`
- [**text-generation-inference**](https://github.com/huggingface/text-generation-inference) — HuggingFace's production inference server. Flash Attention 2, speculative decoding, Safetensors loading, Prometheus metrics. `Rust` `Python` `serving`

---

## 🔁 Retry, Circuit Breakers & Resilience

Production-grade failure handling: retry policies, backpressure, and fault isolation.

- [**llm-retry**](https://github.com/Mattbusel/llm-retry) ⭐ — C++ library for LLM-specific retry logic. Exponential backoff with jitter, per-provider error classification, and circuit breaker integration. Header-only, zero dependencies. `C++` `resilience` `header-only`
- [**tokio-prompt-orchestrator**](https://github.com/Mattbusel/tokio-prompt-orchestrator) ⭐ — The orchestrator's retry module implements tiered backoff: immediate retry → linear backoff → exponential with full jitter. Circuit breaker opens after configurable failure threshold with half-open probe. `Rust` `circuit-breaker` `backoff`
- [**again**](https://github.com/softprops/again) — Simple, composable async retry for Rust. Configurable strategies (fixed, exponential, linear), condition filters, and async-compatible. `Rust` `retry` `async`
- [**governor**](https://github.com/antifuchs/governor) — Principled rate limiting for Rust using the GCRA algorithm. Keyed limiters, burst allowances, and async compatibility. The correct choice for per-tenant rate limiting. `Rust` `rate-limiting` `gcra`
- [**resilience4j**](https://github.com/resilience4j/resilience4j) — The Java reference implementation for the circuit breaker pattern. Retry, bulkhead, timeout, and rate limiter decorators with rich metrics. `Java` `circuit-breaker` `battle-tested`
- [**pybreaker**](https://github.com/danielfm/pybreaker) — Python circuit breaker implementation. Thread-safe, Redis-backed state option, listener hooks for observability integration. `Python` `circuit-breaker`

---

## 📊 Observability & Tracing

Structured logs, distributed traces, and metrics for LLM workloads.

- [**llm-log**](https://github.com/Mattbusel/llm-cpp) ⭐ — Structured logging component from the llm-cpp suite. JSON-line output, severity levels, correlation IDs for request tracing. Header-only C++. `C++` `logging` `structured`
- [**llm-trace**](https://github.com/Mattbusel/llm-cpp) ⭐ — Distributed tracing header from the llm-cpp suite. OpenTelemetry-compatible span creation, propagation headers, and sampling policy hooks. `C++` `tracing` `opentelemetry`
- [**langfuse**](https://github.com/langfuse/langfuse) — Open-source LLM observability platform. Prompt management, evaluation pipelines, cost tracking, and session replay. Self-hostable. `TypeScript` `observability` `self-hosted`
- [**helicone**](https://github.com/Helicone/helicone) — LLM observability proxy. Drop-in between your app and any OpenAI-compatible endpoint. Latency, cost, and error dashboards out of the box. `TypeScript` `proxy` `metrics`
- [**opentelemetry-rust**](https://github.com/open-telemetry/opentelemetry-rust) — Official Rust SDK for OpenTelemetry. Traces, metrics, and logs with W3C context propagation. The foundation for vendor-neutral observability. `Rust` `opentelemetry` `standard`
- [**tracing**](https://github.com/tokio-rs/tracing) — The Tokio ecosystem's structured async-aware tracing framework. Span context, async instrumentation, and pluggable subscriber backends. `Rust` `async` `spans`
- [**phoenix**](https://github.com/Arize-ai/phoenix) — Arize's open-source AI observability tool. LLM traces, embedding drift, retrieval quality, and evaluation in a single UI. `Python` `observability` `evals`

---

## 🛡️ Safety & Hallucination Detection

Guard rails, content filtering, and factuality verification.

- [**LLM-Hallucination-Detection-Script**](https://github.com/Mattbusel/LLM-Hallucination-Detection-Script) ⭐ — Detection pipeline for LLM hallucinations using consistency sampling, self-checking, and NLI-based factuality scoring. 14 stars. `Python` `hallucination` `factuality`
- [**llm_affector**](https://github.com/Mattbusel/llm_affector) ⭐ — Sentiment and affect analysis layer for LLM outputs. Flags emotionally charged or manipulative responses before delivery. `Python` `sentiment` `safety`
- [**llm-guard**](https://github.com/Mattbusel/llm-cpp) ⭐ — C++ guard rail component from the llm-cpp suite. Input sanitization, PII detection patterns, and output schema validation. Zero-overhead on the hot path. `C++` `guardrails` `pii`
- [**guardrails-ai**](https://github.com/guardrails-ai/guardrails) — Python framework for adding input/output validation to LLMs. 60+ built-in validators: PII, toxicity, JSON schema, regex, and custom. `Python` `validation` `production`
- [**nemo-guardrails**](https://github.com/NVIDIA/NeMo-Guardrails) — NVIDIA's programmable guardrail system. Colang language for declarative safety policies. Jailbreak resistance, topical rails, and fact checking. `Python` `nvidia` `declarative`
- [**llm-guard**](https://github.com/protectai/llm-guard) — ProtectAI's security toolkit for LLM applications. Prompt injection detection, token limit enforcement, and sensitive data scanning. `Python` `security` `injection`
- [**garak**](https://github.com/NVIDIA/garak) — LLM vulnerability scanner. Tests models for prompt injection, jailbreaks, hallucination, toxicity, and data leakage. Think `nmap` for LLMs. `Python` `security` `red-teaming`

---

## 🧠 Agent Memory & State

Vector stores, episodic memory, and persistent agent context management.

- [**tokio-agent-memory**](https://github.com/Mattbusel/tokio-agent-memory) ⭐ — Async memory layer for Tokio-based agents. Short-term working memory with LRU eviction, long-term episodic store, and retrieval-augmented recall. `Rust` `memory` `async`
- [**mem-graph**](https://github.com/Mattbusel/mem-graph) ⭐ — Graph-structured agent memory. Entities, relations, and temporal context with graph traversal for associative recall. `Rust` `graph` `knowledge`
- [**lancedb**](https://github.com/lancedb/lancedb) — Serverless vector database built on the Lance columnar format. Embedded (no server), S3-compatible, multimodal, and ANN search via IVF-PQ. `Rust` `Python` `vector-db`
- [**chroma**](https://github.com/chroma-core/chroma) — Open-source embedding database. Simple Python API, persistent storage, metadata filtering, and multi-modal support. The fastest way to add memory to an agent. `Python` `vector-db` `embeddings`
- [**qdrant**](https://github.com/qdrant/qdrant) — Production vector search engine. Rust core, distributed deployments, payload filtering, named vectors, and quantization. OpenAPI + gRPC. `Rust` `vector-db` `distributed`
- [**mem0**](https://github.com/mem0ai/mem0) — Intelligent memory layer for AI assistants. Automatically extracts, stores, and retrieves user preferences and context across sessions. `Python` `memory` `personalization`
- [**zep**](https://github.com/getzep/zep) — Long-term memory for LLM apps. Automatic summarization, temporal knowledge graph, and semantic search over conversation history. `Go` `memory` `summarization`

---

## 📏 Benchmarking & Evaluation

Throughput testing, quality metrics, and systematic model evaluation.

- [**llm-bench**](https://github.com/Mattbusel/llm-bench) ⭐ — Comprehensive LLM infrastructure benchmarking suite. Measures throughput, P50/P99 latency, token rate, circuit breaker overhead, and streaming pipeline performance. `Rust` `benchmarking` `metrics`
- [**llm-eval**](https://github.com/Mattbusel/llm-cpp) ⭐ — C++ evaluation harness from the llm-cpp suite. Deterministic test vectors, regression detection, and golden-file comparison. Header-only. `C++` `evaluation` `regression`
- [**Token-Visualizer**](https://github.com/Mattbusel/Token-Visualizer) ⭐ — Interactive tokenization visualizer. Inspects BPE merge sequences, attention patterns, and token boundary artifacts across tokenizer versions. 8 stars. `Python` `visualization` `tokenization`
- [**evals**](https://github.com/openai/evals) — OpenAI's evaluation framework. 1000+ built-in eval sets, custom eval authoring, and CI integration for tracking model regressions. `Python` `evaluation` `openai`
- [**ragas**](https://github.com/explodinggradients/ragas) — RAG pipeline evaluation. Faithfulness, answer relevancy, context precision, and context recall metrics. Works with any RAG framework. `Python` `rag` `evaluation`
- [**promptfoo**](https://github.com/promptfoo/promptfoo) — CLI and library for prompt testing and red-teaming. A/B prompt comparison, automated regression tests, and provider-agnostic. `TypeScript` `prompts` `testing`
- [**lm-evaluation-harness**](https://github.com/EleutherAI/lm-evaluation-harness) — EleutherAI's standard benchmark suite. MMLU, HellaSwag, TruthfulQA, GSM8K, and 200+ tasks. The academic standard for model comparison. `Python` `benchmarks` `academic`

---

## 💰 Cost & Budget Management

Token accounting, spend tracking, and budget enforcement.

- [**llm-budget**](https://github.com/Mattbusel/llm-budget) ⭐ — Real-time budget management for LLM applications. Per-tenant spend limits, token quotas, alert thresholds, and automatic request shedding when budgets are exceeded. `Rust` `budget` `multi-tenant`
- [**llm-cost**](https://github.com/Mattbusel/llm-cpp) ⭐ — C++ cost estimation header from the llm-cpp suite. Per-model pricing tables, token counting, and cost projection for batch workloads. `C++` `cost` `accounting`
- [**tokencost**](https://github.com/AgentOps-AI/tokencost) — Python library with up-to-date pricing for 400+ LLM models. Automatic token counting and cost estimation for any provider. `Python` `pricing` `token-counting`
- [**litellm**](https://github.com/BerriAI/litellm) — Universal LLM proxy with built-in cost tracking. 100+ providers under a single OpenAI-compatible interface. Budget limits, usage logs, and model fallbacks. `Python` `proxy` `multi-provider`
- [**langfuse**](https://github.com/langfuse/langfuse) — Also includes detailed cost attribution per trace, user, and experiment. See [Observability](#observability--tracing). `TypeScript` `cost` `tracing`

---

## 🔩 C++ Single-Header Libraries

The complete [**llm-cpp**](https://github.com/Mattbusel/llm-cpp) ⭐ suite — 26 production-ready headers for embedding LLM infrastructure into any C++ application. No external dependencies. MSVC, GCC, and Clang compatible. AVX2/AVX-512 hot paths where applicable.

| Header | Purpose |
|--------|---------|
| [`llm-client.hpp`](https://github.com/Mattbusel/llm-cpp) | HTTP client with connection pooling and TLS |
| [`llm-stream.hpp`](https://github.com/Mattbusel/llm-cpp) | Lock-free SPSC streaming pipeline |
| [`llm-retry.hpp`](https://github.com/Mattbusel/llm-cpp) | Exponential backoff with jitter |
| [`llm-circuit.hpp`](https://github.com/Mattbusel/llm-cpp) | Circuit breaker with half-open probe |
| [`llm-budget.hpp`](https://github.com/Mattbusel/llm-cpp) | Token quota and spend enforcement |
| [`llm-cost.hpp`](https://github.com/Mattbusel/llm-cpp) | Per-model pricing and cost projection |
| [`llm-guard.hpp`](https://github.com/Mattbusel/llm-cpp) | Input/output sanitization and PII detection |
| [`llm-log.hpp`](https://github.com/Mattbusel/llm-cpp) | Structured JSON-line logging |
| [`llm-trace.hpp`](https://github.com/Mattbusel/llm-cpp) | OpenTelemetry-compatible span tracing |
| [`llm-eval.hpp`](https://github.com/Mattbusel/llm-cpp) | Evaluation harness and golden-file comparison |
| [`llm-embed.hpp`](https://github.com/Mattbusel/llm-cpp) | Embedding generation and similarity search |
| [`llm-cache.hpp`](https://github.com/Mattbusel/llm-cpp) | Semantic response caching with TTL |
| [`llm-pool.hpp`](https://github.com/Mattbusel/llm-cpp) | Worker pool for concurrent inference |
| [`llm-queue.hpp`](https://github.com/Mattbusel/llm-cpp) | Priority request queue with backpressure |
| [`llm-router.hpp`](https://github.com/Mattbusel/llm-cpp) | Multi-provider request routing |
| [`llm-ratelimit.hpp`](https://github.com/Mattbusel/llm-cpp) | Token bucket and GCRA rate limiting |
| [`llm-tokenize.hpp`](https://github.com/Mattbusel/llm-cpp) | BPE tokenizer with vocabulary management |
| [`llm-prompt.hpp`](https://github.com/Mattbusel/llm-cpp) | Prompt template engine |
| [`llm-schema.hpp`](https://github.com/Mattbusel/llm-cpp) | JSON schema validation for structured output |
| [`llm-rag.hpp`](https://github.com/Mattbusel/llm-cpp) | Retrieval-augmented generation pipeline |
| [`llm-agent.hpp`](https://github.com/Mattbusel/llm-cpp) | Minimal tool-use agent loop |
| [`llm-memory.hpp`](https://github.com/Mattbusel/llm-cpp) | In-process episodic memory store |
| [`llm-simd.hpp`](https://github.com/Mattbusel/llm-cpp) | AVX2/AVX-512 SIMD kernels for embedding ops |
| [`llm-wasm.hpp`](https://github.com/Mattbusel/llm-cpp) | WebAssembly export adapters |
| [`llm-finance.hpp`](https://github.com/Mattbusel/llm-cpp) | Quant finance primitives (beta, gamma, OHLCV) |
| [`llm-bench.hpp`](https://github.com/Mattbusel/llm-cpp) | Micro-benchmark harness |

---

## 📈 Quantitative Finance + LLMs

Applying language models to market data, trading strategies, and financial modeling.

- [**Special-Relativity-in-Financial-Modeling**](https://github.com/Mattbusel/Special-Relativity-in-Financial-Modeling) ⭐ — Applies special relativity's spacetime geometry to financial modeling. Maps price momentum to relativistic beta (v/c), uses Lorentz transforms for reference-frame-invariant signal extraction. Q1 VR=1.27x, Bartlett p=6e-16. `Python` `C++` `research` `quant`
- [**FinRL_DeepSeek_Crypto_Trading**](https://github.com/Mattbusel/FinRL_DeepSeek_Crypto_Trading) ⭐ — Reinforcement learning crypto trading agent powered by DeepSeek LLM for market sentiment. Combines FinRL's DRL backbone with LLM-generated signals. `Python` `rl` `crypto` `deepseek`
- [**Reddit-Options-Trader**](https://github.com/Mattbusel/Reddit-Options-Trader) ⭐ — Options trading system driven by Reddit sentiment analysis via LLM classification. Parses WSB, rates tickers, and constructs option spreads around sentiment extremes. `Python` `options` `sentiment` `reddit`
- [**LLMTokenStreamQuantEngine**](https://github.com/Mattbusel/LLMTokenStreamQuantEngine) ⭐ — Quantitative engine that treats LLM token streams as market microstructure data. Applies order book analytics, tick-by-tick momentum, and HFT-style signal extraction to token generation sequences. `Python` `C++` `hft` `microstructure`
- [**FinRL**](https://github.com/AI4Finance-Foundation/FinRL) — The reference deep reinforcement learning framework for quantitative finance. Backtesting, paper trading, live trading, and 50+ market environments. `Python` `rl` `backtesting`
- [**qlib**](https://github.com/microsoft/qlib) — Microsoft Research's AI-oriented quantitative investment platform. Alpha mining, portfolio optimization, online learning, and a full data pipeline. `Python` `microsoft` `research`
- [**vectorbt**](https://github.com/polakowo/vectorbt) — Vectorized backtesting engine. NumPy/Pandas-native, supports parameter grid search over millions of strategy variants in seconds. `Python` `backtesting` `vectorized`

---

## 🌐 WebAssembly & Edge

Running LLM components in the browser, at the edge, and in sandboxed environments.

- [**llm-wasm**](https://github.com/Mattbusel/llm-wasm) ⭐ — WebAssembly build of core LLM client infrastructure. Runs tokenization, prompt templating, and response parsing fully in-browser without a server round-trip. `Rust` `wasm` `browser`
- [**wasm-agent**](https://github.com/Mattbusel/wasm-agent) ⭐ — Lightweight agent runtime compiled to WASM. Tool-use loop, memory retrieval, and streaming output — deployable to Cloudflare Workers, Fastly Compute, and Deno Deploy. `Rust` `wasm` `edge`
- [**llama.cpp**](https://github.com/ggerganov/llama.cpp) — The canonical C/C++ LLM inference library. GGUF format, WASM/SIMD/Metal/CUDA backends, and the foundation for most local inference tooling. `C++` `wasm` `gguf` `inference`
- [**wasm-bindgen**](https://github.com/rustwasm/wasm-bindgen) — Rust/WebAssembly interoperability toolkit. The standard for compiling Rust to WASM with JavaScript bindings. Essential for browser-side LLM components. `Rust` `wasm` `bindings`
- [**web-llm**](https://github.com/mlc-ai/web-llm) — In-browser LLM inference via WebGPU. Full Llama, Mistral, and Phi models running natively in Chrome/Edge with no server. `TypeScript` `webgpu` `browser`
- [**wasi-nn**](https://github.com/WebAssembly/wasi-nn) — WASI Neural Network proposal. Standard interface for ML inference from WASM modules. The foundation for portable edge inference. `WebAssembly` `standard` `wasi`

---

## 📚 Learning Resources

Foundational and practical resources for building serious LLM infrastructure.

- [**Neural Networks: Zero to Hero**](https://karpathy.ai/zero-to-hero.html) — Andrej Karpathy's complete video series. Builds nanoGPT from scratch: backprop, attention, tokenization, scaling. The best technical introduction that exists.
- [**Lilian Weng's Blog**](https://lilianweng.github.io) — Lilian Weng (OpenAI) writes the definitive technical deep-dives: attention mechanisms, RLHF, agents, diffusion, tool use. Dense, rigorous, essential.
- [**Tokio Tutorial**](https://tokio.rs/tokio/tutorial) — The official async Rust tutorial. Task scheduling, channels, select!, timeouts, and I/O. Required reading before writing any async LLM infrastructure in Rust.
- [**The Illustrated Transformer**](https://jalammar.github.io/illustrated-transformer/) — Jay Alammar's visual walkthrough of transformer architecture. The clearest explanation of attention, residual streams, and the full forward pass.
- [**Latency Numbers Every LLM Engineer Should Know**](https://github.com/sirupsen/latency) — Updated version of the classic "latency numbers every programmer should know", extended with GPU memory bandwidth, PCIe throughput, and inter-datacenter latency.
- [**Building LLM Applications for Production**](https://huyenchip.com/2023/04/11/llm-engineering.html) — Chip Huyen's practical guide to production LLM systems: evaluation, cost, latency, and the hard lessons from shipping real products.
- [**LLM Patterns**](https://eugeneyan.com/writing/llm-patterns/) — Eugene Yan's catalog of recurring patterns in production LLM systems: evals, RAG, caching, guardrails, and versioning. Pragmatic and well-sourced.

---

## Contributing

Contributions welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first.

- Each entry must be actively maintained (last commit within 18 months)
- Entries must be production-relevant, not toy examples
- Descriptions must be factual — no marketing language
- Keep the ⭐ marker exclusively for repos by [@Mattbusel](https://github.com/Mattbusel)

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, [Matthew Busel](https://github.com/Mattbusel) has waived all copyright and related rights to this work.
