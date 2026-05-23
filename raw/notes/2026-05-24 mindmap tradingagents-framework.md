# Mind map: TradingAgents Framework (implementation view)

> **Source kind:** mind map (image) provided by user 2026-05-24.
> **About:** The open-source TradingAgents framework — an implementation
> view focused on agent composition, callable tools, orchestration, and
> service tiers. Cousin / extension of the
> [[2026-05-24 tauric-tradingagents-arxiv-2412.20138v7|Tauric academic paper]]
> but covers concrete deployment choices the paper does not (LangGraph,
> LLM Factory, vendor dispatcher, free/freemium/paid stacks).
> **Transcribed from image** — original lives in the conversation context.

## Root: TradingAgents Framework

### Agent Architecture
- **Analyst Team**
  - Market Analyst
  - Social/Sentiment Analyst
  - News Analyst
  - Fundamentals Analyst
- **Researcher Team**
  - Bull Researcher
  - Bear Researcher
  - Debate Loop
- **Management & Trading**
  - Research Manager
  - Trader
  - Portfolio Manager
- **Risk Management Team**
  - Aggressive Analyst
  - Conservative Analyst
  - Neutral Analyst

### Framework Skills & Tools
- **Callable Tools (`@tool`)**
  - Core Stock Data
  - Technical Indicators
  - Financial Statements
  - News & Insider Transactions
- **Core Capabilities**
  - Structured Output (Pydantic)
  - Persistent Decision Memory
  - Deferred Reflection Loop
  - Checkpoint Resume (SQLite)
  - 5-Tier Rating Parser

### System Orchestration
- LangGraph StateGraph
- Shared AgentState Blackboard
- LLM Factory (Quick vs. Deep Tiers)
- Vendor Dispatcher (yfinance / Alpha Vantage)

### Cost & Deployment
- **Service Tiers**
  - Free (yfinance, Local Files)
  - Freemium (Gemini, Alpha Vantage)
  - Paid (OpenAI, Anthropic, DeepSeek)
  - Self-hosted (Ollama)
- **Recommended Stacks**
  - Pure-free: Ollama + yfinance
  - Cheapest Hosted: Gemini + yfinance
  - Production: GPT-4 / Claude + Alpha Vantage

---

## Notes from the user

(none — bare mind map dropped in)

## My read on what's interesting

- This mind map is the **operational complement** to the Tauric paper.
  The paper says "agents debate in n rounds"; this mind map says
  "implemented via LangGraph StateGraph with a shared AgentState
  blackboard, Pydantic-typed handoffs, and SQLite checkpoints."
- The **Research Manager** and **Portfolio Manager** roles do not appear
  in the original 2024 Tauric paper (which has Researcher Team, Trader,
  Risk Management, Fund Manager). Either the implementation expanded the
  role taxonomy, or the mind map is summarizing a fork/extension.
  → Worth flagging as a divergence and verifying upstream.
- The **LLM Factory (Quick vs. Deep Tiers)** abstraction is essentially
  the paper's idea of "use gpt-4o-mini for retrieval, o1-preview for
  reasoning" turned into a runtime selector.
- The **5-Tier Rating Parser** is not in the paper either — probably
  output schema for the trader's final decision (Strong Buy / Buy / Hold
  / Sell / Strong Sell). Verify.
- **No mention of evaluation** — the paper backtests against B&H/MACD/
  KDJ+RSI/ZMR/SMA baselines on AAPL/GOOGL/AMZN. The mind map omits this,
  which makes the framework look more "ready" than the paper's data
  actually supports (3-month backtest with SR > 8 is implausibly high
  and the authors themselves flag this).
