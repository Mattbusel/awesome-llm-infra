# Awesome LLM Infrastructure

> A curated list of tools for running LLMs in production: runtimes and orchestration, clients, streaming, resilience, observability, safety, memory, evaluation, cost control, C++ libraries, finance and edge.

Maintained by [@Mattbusel](https://github.com/Mattbusel). Projects by the maintainer are marked with ⭐ so you can tell them apart from the wider ecosystem. Links were checked in September 2026; archived or long-inactive projects were removed.

## Contents

- [Async Runtimes & Orchestration](#async-runtimes--orchestration)
- [LLM Clients & SDKs](#llm-clients--sdks)
- [Inference & Streaming](#inference--streaming)
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

## Async Runtimes & Orchestration

Request pipelines with backpressure, deduplication, circuit breaking and structured concurrency.

- ⭐ [**tokio-prompt-orchestrator**](https://github.com/Mattbusel/tokio-prompt-orchestrator) - Five-stage Tokio pipeline for serving LLM requests with dedup, circuit breakers, retries, rate limits and a dead-letter queue; REST, SSE, MCP and a TUI. `Rust`
- ⭐ [**agent-runtime**](https://github.com/Mattbusel/agent-runtime) - Agent runtime crate: ReAct and plan-execute loops, memory, knowledge graph, circuit breakers, Anthropic and OpenAI providers, multi-agent bus. `Rust`
- ⭐ [**HelixRouter**](https://github.com/Mattbusel/HelixRouter-adaptive-async-compute-router-) - Adaptive Tokio job router that picks inline, spawn, CPU pool, batch or drop per job from cost, latency budget and live pressure. `Rust`
- [**rig**](https://github.com/0xPlaygrounds/rig) - Rust framework for LLM-powered agents and pipelines with a provider-agnostic API. `Rust`
- [**langchain-rust**](https://github.com/Abraxas-365/langchain-rust) - LangChain concepts in Rust: chains, agents, memory and tools, async-first. `Rust`

---

## LLM Clients & SDKs

Provider SDKs and abstraction layers for model-agnostic applications.

- ⭐ [**tokio-llm**](https://github.com/Mattbusel/tokio-llm) - Async OpenAI and Anthropic client with retry, circuit breaker, USD budget cap, SSE streaming and typed errors. `Rust`
- [**async-openai**](https://github.com/64bit/async-openai) - Async Rust bindings for the OpenAI API: streaming, function calling, embeddings. `Rust`
- [**anthropic-sdk-python**](https://github.com/anthropics/anthropic-sdk-python) - Official Python SDK for the Anthropic API: sync and async, streaming, tool use, vision. `Python`
- [**openai-node**](https://github.com/openai/openai-node) - Official Node.js/TypeScript SDK for OpenAI. `TypeScript`
- [**litellm**](https://github.com/BerriAI/litellm) - One OpenAI-compatible interface and proxy for 100+ providers, with fallbacks and cost tracking. `Python`

---

## Inference & Streaming

Local and server-side inference engines, and token-level stream tooling.

- ⭐ [**Every-Other-Token**](https://github.com/Mattbusel/Every-Other-Token) - Intercepts an LLM token stream live: per-token confidence and perplexity, on-the-fly token mutation, provider and A/B comparison, replay and heatmap export. `Rust`
- ⭐ [**llm-stream**](https://github.com/Mattbusel/llm-stream) - Single-header C++17 client for streaming OpenAI and Anthropic responses token by token over SSE. `C++`
- [**vllm**](https://github.com/vllm-project/vllm) - High-throughput serving engine with PagedAttention, continuous batching and an OpenAI-compatible API. `Python`
- [**llama.cpp**](https://github.com/ggml-org/llama.cpp) - C/C++ inference for GGUF models with CPU, Metal, CUDA and other backends. `C++`
- [**ollama**](https://github.com/ollama/ollama) - Run models locally behind a simple REST API with model management. `Go`
- [**mistral.rs**](https://github.com/EricLBuehler/mistral.rs) - Local inference engine in Rust with quantization, PagedAttention and speculative decoding. `Rust`
- [**candle**](https://github.com/huggingface/candle) - Minimalist ML framework in Rust from Hugging Face, with CUDA and WASM builds. `Rust`
- [**llm.c**](https://github.com/karpathy/llm.c) - Minimal C/CUDA GPT-2 training and inference; useful for learning the mechanics. `C`

---

## Retry, Circuit Breakers & Resilience

Retry policies, rate limiting, backpressure and fault isolation.

- ⭐ [**llm-retry**](https://github.com/Mattbusel/llm-retry) - Single-header C++17 backoff with jitter, retryable HTTP code handling, provider failover and a circuit breaker. `C++`
- [**governor**](https://github.com/boinkor-net/governor) - GCRA rate limiting for Rust with keyed limiters and async support. `Rust`
- [**resilience4j**](https://github.com/resilience4j/resilience4j) - Circuit breaker, retry, bulkhead, timeout and rate limiter decorators with metrics. `Java`
- [**pybreaker**](https://github.com/danielfm/pybreaker) - Circuit breaker for Python with optional Redis-backed state and listeners. `Python`

---

## Observability & Tracing

Structured logs, traces and metrics for LLM workloads.

- ⭐ [**llm-trace**](https://github.com/Mattbusel/llm-trace) - Single-header C++17 RAII spans with model, token and cost attributes and OTLP-style JSON export. `C++`
- ⭐ [**llm-log**](https://github.com/Mattbusel/llm-log) - Single-header C++17 JSONL logger for LLM calls: model, tokens, cost and latency per call. `C++`
- [**langfuse**](https://github.com/langfuse/langfuse) - Open-source LLM observability: traces, prompt management, evaluations and cost tracking; self-hostable. `TypeScript`
- [**helicone**](https://github.com/Helicone/helicone) - Observability proxy in front of OpenAI-compatible endpoints with latency, cost and error dashboards. `TypeScript`
- [**phoenix**](https://github.com/Arize-ai/phoenix) - Arize's open-source tool for LLM traces, retrieval quality and evaluations. `Python`
- [**opentelemetry-rust**](https://github.com/open-telemetry/opentelemetry-rust) - Official OpenTelemetry SDK for Rust: traces, metrics and logs. `Rust`
- [**tracing**](https://github.com/tokio-rs/tracing) - Structured, async-aware tracing for the Tokio ecosystem. `Rust`

---

## Safety & Hallucination Detection

Guardrails, content filtering and factuality checks.

- ⭐ [**LLM-Hallucination-Detection-Script**](https://github.com/Mattbusel/LLM-Hallucination-Detection-Script) - Renders per-token confidence from logprobs as colored terminal, HTML or Markdown output and flags low-confidence spans. `Rust`
- ⭐ [**llm_affector**](https://github.com/Mattbusel/llm_affector) - LLM-as-judge library: hallucination detection for text and critique of Rust code, with typed results (prototype). `Rust`
- ⭐ [**llm-guard (C++)**](https://github.com/Mattbusel/llm-guard) - Single-header C++17 offline PII scrubbing (emails, phones, SSNs, cards, API keys) and prompt-injection scoring. `C++`
- [**guardrails**](https://github.com/guardrails-ai/guardrails) - Input and output validation for LLMs with a library of validators. `Python`
- [**NeMo Guardrails**](https://github.com/NVIDIA-NeMo/Guardrails) - NVIDIA's programmable guardrails with the Colang policy language. `Python`
- [**garak**](https://github.com/NVIDIA/garak) - LLM vulnerability scanner for prompt injection, jailbreaks, leakage and more. `Python`

---

## Agent Memory & State

Vector stores, episodic memory and persistent agent context.

- ⭐ [**tokio-agent-memory**](https://github.com/Mattbusel/tokio-agent-memory) - Episodic events with causal links, semantic fact graph, prioritized working memory, decay, fuzzy retrieval and a multi-agent bus. `Rust`
- ⭐ [**tokio-memory**](https://github.com/Mattbusel/tokio-memory) - Trait-based episodic and semantic stores, query builder, Ebbinghaus decay and consolidation. `Rust`
- ⭐ [**mem-graph**](https://github.com/Mattbusel/mem-graph) - Embeddable in-memory knowledge graph with typed relationships, traversal, shortest path and JSON snapshots. `Rust`
- ⭐ [**llm-sync**](https://github.com/Mattbusel/llm-sync) - CRDTs and vector clocks for sharing state between agents without a coordinator. `Rust`
- [**qdrant**](https://github.com/qdrant/qdrant) - Vector search engine with payload filtering, quantization and distributed mode. `Rust`
- [**lancedb**](https://github.com/lancedb/lancedb) - Embedded, serverless vector database on the Lance columnar format. `Rust` `Python`
- [**chroma**](https://github.com/chroma-core/chroma) - Open-source embedding database with a simple API and metadata filtering. `Rust` `Python`
- [**mem0**](https://github.com/mem0ai/mem0) - Memory layer that extracts and recalls user facts across sessions. `Python`
- [**zep**](https://github.com/getzep/zep) - Long-term memory for LLM apps with a temporal knowledge graph. `Python`

---

## Benchmarking & Evaluation

Latency testing, quality metrics and systematic evaluation.

- ⭐ [**llm-bench**](https://github.com/Mattbusel/llm-bench) - CLI that runs your prompts against OpenAI and Anthropic models and compares p50/p99 latency, tokens per second and cost. `Rust`
- ⭐ [**llm-eval**](https://github.com/Mattbusel/llm-eval) - Single-header C++17 consistency and latency evaluation: run a prompt N times, compare models or system prompts. `C++`
- ⭐ [**llm-ab**](https://github.com/Mattbusel/llm-ab) - Single-header C++17 A/B testing of prompts and models with Welch's t-test and effect size. `C++`
- ⭐ [**Token-Visualizer**](https://github.com/Mattbusel/Token-Visualizer) - Python script showing how tiktoken or Hugging Face tokenizers split a prompt, with token-cost ranking. `Python`
- [**promptfoo**](https://github.com/promptfoo/promptfoo) - CLI and library for prompt testing, regression checks and red-teaming. `TypeScript`
- [**ragas**](https://github.com/vibrantlabsai/ragas) - Evaluation metrics for RAG pipelines: faithfulness, relevancy, context precision and recall. `Python`
- [**lm-evaluation-harness**](https://github.com/EleutherAI/lm-evaluation-harness) - EleutherAI's standard benchmark suite (MMLU, HellaSwag, GSM8K and hundreds more). `Python`
- [**evals**](https://github.com/openai/evals) - OpenAI's framework and registry for model evaluations. `Python`

---

## Cost & Budget Management

Token accounting, spend tracking and budget enforcement.

- ⭐ [**llm-budget**](https://github.com/Mattbusel/llm-budget) - Hard USD caps per agent and per fleet, kill switches and automatic model downgrade as budgets run low. `Rust`
- ⭐ [**llm-cost-dashboard**](https://github.com/Mattbusel/llm-cost-dashboard) - Terminal dashboard for LLM spend from a JSON request log, with 83 priced models and monthly projections. `Rust`
- ⭐ [**llm-cost**](https://github.com/Mattbusel/llm-cost) - Single-header C++17 offline token counter and cost estimator with a budget guard. `C++`
- [**tokencost**](https://github.com/AgentOps-AI/tokencost) - Token counting and price estimates for hundreds of models. `Python`
- [**litellm**](https://github.com/BerriAI/litellm) - Also tracks spend per key, user and team with budget limits. See [LLM Clients](#llm-clients--sdks). `Python`
- [**langfuse**](https://github.com/langfuse/langfuse) - Also attributes cost per trace, user and experiment. See [Observability](#observability--tracing). `TypeScript`

---

## C++ Single-Header Libraries

⭐ [**llm-cpp**](https://github.com/Mattbusel/llm-cpp) indexes 26 single-header C++17 libraries, each in its own repository. Copy one `.hpp`; network libraries need only libcurl.

| Library | Purpose |
|---|---|
| [llm-stream](https://github.com/Mattbusel/llm-stream) | Stream OpenAI and Anthropic responses token by token over SSE |
| [llm-chat](https://github.com/Mattbusel/llm-chat) | Multi-turn conversation manager with token-budget trimming |
| [llm-agent](https://github.com/Mattbusel/llm-agent) | Tool-calling agent loop for OpenAI-compatible APIs |
| [llm-vision](https://github.com/Mattbusel/llm-vision) | Send images to OpenAI or Anthropic vision models |
| [llm-audio](https://github.com/Mattbusel/llm-audio) | Whisper transcription and text-to-speech |
| [llm-embed](https://github.com/Mattbusel/llm-embed) | Embeddings, cosine similarity and a file-backed vector store |
| [llm-rag](https://github.com/Mattbusel/llm-rag) | Chunk, embed, index, retrieve and answer |
| [llm-rank](https://github.com/Mattbusel/llm-rank) | BM25, LLM and hybrid reranking |
| [llm-parse](https://github.com/Mattbusel/llm-parse) | Clean HTML/Markdown and chunk documents |
| [llm-compress](https://github.com/Mattbusel/llm-compress) | Fit conversations into a token budget |
| [llm-template](https://github.com/Mattbusel/llm-template) | Mustache-style prompt templates with a token budget |
| [llm-format](https://github.com/Mattbusel/llm-format) | Schema-validated JSON output with automatic retries |
| [llm-json](https://github.com/Mattbusel/llm-json) | JSON parser and builder for LLM code |
| [llm-router](https://github.com/Mattbusel/llm-router) | Pick a model by prompt complexity, cost and latency |
| [llm-retry](https://github.com/Mattbusel/llm-retry) | Backoff, failover and circuit breaker |
| [llm-pool](https://github.com/Mattbusel/llm-pool) | Worker pool with request and token rate budgets |
| [llm-batch](https://github.com/Mattbusel/llm-batch) | Resumable JSONL batch runner with rate limiting |
| [llm-cache](https://github.com/Mattbusel/llm-cache) | LRU response cache with TTL |
| [llm-cost](https://github.com/Mattbusel/llm-cost) | Token counting, cost estimates and a budget guard |
| [llm-guard](https://github.com/Mattbusel/llm-guard) | PII scrubbing and prompt-injection scoring |
| [llm-log](https://github.com/Mattbusel/llm-log) | JSONL logging of calls with cost and latency |
| [llm-trace](https://github.com/Mattbusel/llm-trace) | RAII tracing spans with OTLP-style export |
| [llm-eval](https://github.com/Mattbusel/llm-eval) | Consistency and latency evaluation |
| [llm-ab](https://github.com/Mattbusel/llm-ab) | Prompt and model A/B tests with statistics |
| [llm-mock](https://github.com/Mattbusel/llm-mock) | Scripted mock LLM for unit tests |
| [llm-finetune](https://github.com/Mattbusel/llm-finetune) | OpenAI fine-tuning jobs and training files |

---

## Quantitative Finance + LLMs

Language models and market data.

- ⭐ [**LLMTokenStreamQuantEngine**](https://github.com/Mattbusel/LLMTokenStreamQuantEngine) - C++20 research engine that maps a live LLM token stream to sentiment weights and emits risk-gated trade signals to FIX 4.2, REST or mock adapters. `C++`
- ⭐ [**Reddit-Options-Trader**](https://github.com/Mattbusel/Reddit-Options-Trader-ROT-) - Research pipeline that turns trending Reddit discussions into structured market events and options trade ideas. `Python`
- ⭐ [**FinRL_DeepSeek_Crypto_Trading**](https://github.com/Mattbusel/FinRL_DeepSeek_Crypto_Trading) - FinRL Contest 2025 Task 1 entry: a reinforcement-learning crypto trading agent using LLM-derived market signals. `Python`
- ⭐ [**Special-Relativity-in-Financial-Modeling**](https://github.com/Mattbusel/Special-Relativity-in-Financial-Modeling) - C++20 research code applying special-relativistic geometry (Lorentz factors, spacetime intervals, geodesic deviation) to OHLCV data. `C++`
- [**FinRL**](https://github.com/AI4Finance-Foundation/FinRL) - Deep reinforcement learning framework for quantitative finance. `Python`
- [**qlib**](https://github.com/microsoft/qlib) - Microsoft's AI-oriented quantitative investment platform. `Python`
- [**vectorbt**](https://github.com/polakowo/vectorbt) - Vectorized backtesting on NumPy and pandas for large parameter sweeps. `Python`

---

## WebAssembly & Edge

LLM components in the browser, at the edge and in sandboxes.

- ⭐ [**llm-wasm**](https://github.com/Mattbusel/llm-wasm) - Pure-Rust logic around an LLM call that builds for `wasm32`: TTL cache, retry policy, guards, routing, cost ledger, templates, JSON extraction. `Rust`
- ⭐ [**wasm-agent**](https://github.com/Mattbusel/wasm-agent) - Synchronous ReAct loop with tool registry and token-limited history; no async runtime, builds for `wasm32`. `Rust`
- [**web-llm**](https://github.com/mlc-ai/web-llm) - In-browser LLM inference on WebGPU. `TypeScript`
- [**wasm-bindgen**](https://github.com/wasm-bindgen/wasm-bindgen) - Rust and JavaScript interop for WebAssembly. `Rust`

---

## Learning Resources

- [**Neural Networks: Zero to Hero**](https://karpathy.ai/zero-to-hero.html) - Andrej Karpathy's video series that builds a GPT from scratch.
- [**Lilian Weng's blog**](https://lilianweng.github.io) - Deep technical write-ups on attention, RLHF, agents and more.
- [**Tokio tutorial**](https://tokio.rs/tokio/tutorial) - The official async Rust tutorial; background for any Tokio-based LLM service.
- [**The Illustrated Transformer**](https://jalammar.github.io/illustrated-transformer/) - Jay Alammar's visual walkthrough of the transformer.
- [**Building LLM applications for production**](https://huyenchip.com/2023/04/11/llm-engineering.html) - Chip Huyen on evaluation, cost and latency in real LLM products.
- [**Patterns for building LLM-based systems**](https://eugeneyan.com/writing/llm-patterns/) - Eugene Yan's catalogue of evals, RAG, caching, guardrails and more.

---

## Contributing

Suggestions are welcome as issues or pull requests. An entry should be:

- actively maintained (a commit within the last 18 months, not archived),
- useful for running LLMs in production rather than a toy example,
- described factually, without marketing language.
