# Tessera

**Programmable LLM gateway.** A thin substrate proxy in your AI request path. Auto-route, exact + semantic cache, prompt compression, batch arbitrage, cross-provider failover, per-stack quality canary — under a single drop-in SDK. Cost optimization is the wedge. Substrate is the endgame.

**Free 60M tokens/month. Paid tiers are a flat monthly subscription by token volume — Starter $199, Growth $999, Scale $3,999, Enterprise custom. Keep 100% of measured savings.**

→ [tesseraai.io](https://tesseraai.io) · [tesseraai.io/dev](https://tesseraai.io/dev) · [ledger.tesseraai.io](https://ledger.tesseraai.io)

---

## Open-source SDK

| Package | What it is | Install |
|---|---|---|
| [**`tessera-sdk`**](https://github.com/tessera-llm/tessera-sdk) | Vanilla provider SDK patcher — wraps `openai`, `anthropic`, `mistralai`, `groq`, `cohere` clients. Start here. | `pip install tessera-llm-proxy` · `npm install @tessera-llm/tessera-sdk` |

## Framework integrations

Drop-in adapters for the AI frameworks you already use:

| Framework | Package | Install |
|---|---|---|
| **LangChain** (Python + Node) | [`tessera-langchain`](https://github.com/tessera-llm/tessera-langchain) | `pip install tessera-langchain` · `npm install @tessera-llm/langchain` |
| **Vercel AI SDK** (Node) | [`tessera-vercel-ai`](https://github.com/tessera-llm/tessera-vercel-ai) | `npm install @tessera-llm/vercel-ai` |
| **LlamaIndex** (Python) | [`tessera-llamaindex`](https://github.com/tessera-llm/tessera-llamaindex) | `pip install tessera-llamaindex` |
| **Mastra** (Node) | [`@tessera-llm/mastra`](https://www.npmjs.com/package/@tessera-llm/mastra) | `npm install @tessera-llm/mastra` |
| **Pydantic AI** (Python) | [`tessera-pydantic-ai`](https://pypi.org/project/tessera-pydantic-ai/) | `pip install tessera-pydantic-ai` |
| **CrewAI** (Python) | [`tessera-crewai`](https://pypi.org/project/tessera-crewai/) | `pip install tessera-crewai` |
| **AutoGen 0.4+** (Python) | [`tessera-autogen`](https://pypi.org/project/tessera-autogen/) | `pip install tessera-autogen` |

All seven integrations route through the same proxy at `api.tesseraai.io` with a single `tk_…` key. Mix and match safely — they don't conflict.

---

## How it works in one line

```python
import tessera
tessera.activate(api_key="tk_...")

# Your existing OpenAI / Anthropic / Mistral / Groq / Cohere code
# runs unchanged. Every request now flows through Tessera.
```

That's it. No re-architecture. No new framework to learn. No code changes beyond `activate()`. Save measurements stream to your dashboard at [`ledger.tesseraai.io`](https://ledger.tesseraai.io).

---

## What runs inside the proxy

11 production mechanics, each gated by a per-workload quality canary that auto-disables on regression:

- **M1 auto-route** — cheaper-equivalent model swap when quality preservation holds
- **M2 exact cache** — request hash → cached response
- **M3 prompt compress** — lossless whitespace + structural compression
- **M5 semantic cache** — embedding-similarity lookup with cosine ≥ 0.95 default
- **M6 prompt cache** — Anthropic / OpenAI / Google native provider-side cache markers
- **M7 context pruning** — conversation history + RAG chunk trim past 12 turns or 32K chars
- **M8 structured output** — `response_format=json_schema` injection
- **M9 output-length predictor** — max_tokens ceiling from p90 historical truncation rate
- **M10 batch arbitrage** — async-tolerant workloads routed onto provider batch APIs
- **M11 cross-provider failover** — opt-in OpenRouter fallback on 5xx / connection error
- **C8 probe & prefill** — foundation; per-ADR wire-in deferred

Per-stack quality canary auto-rollback fires per (workload, mechanic-stack) tuple — a regression on `m1+m7` doesn't gate `m1+m3`. SLA floor 0.95 default; configurable per workload.

---

## Pricing

- **Free Sandbox** — 60M tokens/month, hard cap at quota, $0 fee, full mechanic stack active (route · cache · compress · batch). Solo devs + side projects covered entirely.
- **Paid tiers** — flat monthly subscription by gross tokens submitted: Starter $199 (≤1B), Growth $999 (≤5B), Scale $3,999 (≤20B), Enterprise custom (20B+). Full mechanic stack active, unlimited workloads + API keys, auto-rollback + 10% credit on quality regression. You keep 100% of measured savings.

No card up front. No trial expiry. No per-token markup, no cut of your savings — you keep 100% of what we save you.

---

## Resources

- [tesseraai.io](https://tesseraai.io) — landing + product page
- [tesseraai.io/dev](https://tesseraai.io/dev) — developer entry (Free Sandbox signup, install instructions, runnable examples)
- [ledger.tesseraai.io](https://ledger.tesseraai.io) — operator + sponsor dashboard
- [tesseraai.io/blog](https://tesseraai.io/blog) — substrate-architecture deep-dives + cost case studies
- [tesseraai.io/how-it-works](https://tesseraai.io/how-it-works) — per-mechanic deep-dive trust track
- [tesseraai.io/security](https://tesseraai.io/security) — security posture, audit trail, SOC 2 progress

---

Tessera is operated by Fintechagency OÜ, Tallinn, Estonia (registry 16638667).
