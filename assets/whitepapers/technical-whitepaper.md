# CryptoRugMunch Technical Whitepaper

**Version**: 2.0
**Date**: February 2026
**Author**: CryptoRugMunch Development Team

---

## Abstract

CryptoRugMunch is a multi-chain crypto token risk analysis platform built on Python/FastAPI with 20+ Docker microservices. This whitepaper describes the architecture, detection methodology, AI integration, and API design of a production system that analyzes tokens across Solana, Ethereum, and Base for rug pull risk, honeypot traps, and deployer fraud.

---

## 1. Introduction

### 1.1 Problem Statement
Cryptocurrency scams cost users billions annually. Existing analysis tools are web-only, expensive, and require users to leave their trading workflow. The majority of crypto trading communication happens on Telegram, yet no comprehensive risk analysis tool operates natively within it.

### 1.2 Solution
CryptoRugMunch delivers instant, multi-chain token risk analysis through four interfaces:
1. **Telegram Bot** — Command-based and auto-detect scanning
2. **Browser Extension** — Risk badge injection on major DEX platforms
3. **Agent API** — x402-paywalled HTTP endpoints for machine consumption
4. **MCP Server** — Model Context Protocol integration for AI agent tooling

---

## 2. System Architecture

### 2.1 Technology Stack

| Layer | Technology |
|-------|-----------|
| Language | Python 3.12 |
| HTTP Framework | FastAPI |
| Bot SDK | python-telegram-bot |
| Database | PostgreSQL 16 + PgBouncer |
| Cache/Queue | Valkey 7 (Redis-compatible) |
| Orchestration | Docker Compose |
| Extension | React/TypeScript + Vite |
| Mini App | FastAPI + React |

### 2.2 Service Topology

The platform runs as 20+ Docker containers:

**Core Services**: bot, api, frontend, postgres, pgbouncer, valkey

**Background Workers**: alert-monitor, wallet-tracker, reputation-calculator, broadcast-sender, price-updater, blacklist-processor, case-study-broadcaster, rug-autopsy-monitor

**Marcus AI Workers**: marcus-mentions-stream, marcus-rug-quoter, marcus-weekly-thread, marcus-index-worker, marcus-reactive-worker

Each worker runs as an independent container with its own process, enabling horizontal scaling and fault isolation.

### 2.3 Data Flow

Token analysis follows a parallel-fetch, sequential-analyze pipeline:

1. **Address detection** — Regex matching for Solana (base58, 32–44 chars) and EVM (0x-prefixed, 40 hex chars) addresses
2. **Chain resolution** — Automatic chain detection from address format and DexScreener pair data
3. **Parallel data fetch** — Concurrent requests to DexScreener, Helius RPC, GoPlus Security, and TokenSniffer (timeout: 8s per source)
4. **Analysis pipeline** — Sequential execution of rug pattern matching, LP lock verification, holder analysis, bundle detection, contract security checks
5. **Risk scoring** — Weighted aggregation of all signals into a 0–100 risk score
6. **Caching** — Results cached in Valkey to reduce API credit consumption
7. **Persistence** — Scan history and snapshots stored in PostgreSQL for trend analysis

---

## 3. Detection Methodology

### 3.1 Rug Pattern Library

Seven distinct rug pattern signatures are matched against on-chain data:

The `RugPatternLibrary` module analyzes token characteristics against known exploit patterns including liquidity removal setups, mint authority retention, ownership manipulation, and supply concentration schemes.

### 3.2 LP Lock Verification

For Solana tokens, LP lock status is verified by:
1. Identifying the LP token address from the trading pair
2. Checking lock program accounts (e.g., Raydium lock vaults)
3. Verifying lock duration and unlock timestamps
4. Reporting lock status, duration, and percentage locked

### 3.3 Holder Concentration Analysis

The Gini coefficient is calculated across all token holders to measure wealth concentration. Values approaching 1.0 indicate extreme concentration (higher rug risk). Known DEX/CEX wallets (Pump.fun, Raydium, major exchanges) are excluded from the calculation to avoid false positives.

### 3.4 Bundle & Sniper Detection

Launch-time transaction analysis identifies:
- **Bundle buying** — Multiple wallets buying in the same block/slot via coordinated transactions
- **Sniper bots** — Wallets that buy within the first few transactions of a token launch
- **First buyer analysis** — Classification of early buyers by wallet age, funding source, and behavior patterns

### 3.5 Contract Security

Multi-source contract analysis via:
- **GoPlus Security API** — Honeypot detection, mint authority, proxy contracts, trading restrictions
- **TokenSniffer** — Independent security scoring and vulnerability detection
- **Jito MEV** — MEV bundle detection for Solana transactions

### 3.6 Deployer Intelligence

Cross-referencing deployer addresses against:
- Historical token deployments by the same address
- Known serial rugger database (community-maintained)
- Deployment frequency and token survival rates
- Connected wallet analysis

### 3.7 KOL Tracking

Multi-stage influencer intelligence pipeline:
- **Identification** — Wallet labeling and KOL association
- **Monitoring** — Position tracking and entry/exit detection
- **Shill detection** — Pattern matching for coordinated promotion
- **Convergence alerts** — Multiple KOLs buying the same token
- **Exit tracking** — KOL sell detection with timing analysis

---

## 4. Marcus Aurelius — AI Intelligence Engine

Marcus Aurelius is CryptoRugMunch's LLM-powered Stoic crypto forensics analyst — a full intelligence system integrated across the entire platform. He combines natural language understanding, multi-source signal aggregation, autonomous threat detection, and outcome learning into a unified AI engine.

### 4.1 Architecture Overview

Marcus is composed of a core AI brain, a knowledge grounding system, an intelligence hub, and multiple specialized workers deployed as independent Docker services.

```
┌─────────────────────────────────────────────────────────┐
│                   Marcus Brain (LLM)                     │
│         Intent Classification · Stoic Persona            │
│      Natural Language Understanding · Response Gen       │
├──────────────┬──────────────┬───────────────────────────┤
│  Knowledge   │ Intelligence │     Content Generation    │
│   System     │     Hub      │                           │
│ ┌──────────┐ │ ┌──────────┐ │ ┌───────────┐ ┌────────┐ │
│ │Scam Lib  │ │ │X Sentiment│ │ │Rug Quoter │ │Weekly  │ │
│ │Forensic  │ │ │Polymarket│ │ │Formatter  │ │Thread  │ │
│ │Manifest  │ │ │Brave Web │ │ │Analysis   │ │        │ │
│ │Grounding │ │ │Graph Mem │ │ └───────────┘ └────────┘ │
│ └──────────┘ │ │Market API│ │                           │
│              │ └──────────┘ │                           │
├──────────────┴──────────────┴───────────────────────────┤
│              Proactive Intelligence                       │
│  Discovery Scanner · KOL Alpha Engine · Convergence Det  │
│  Shill Detector · Outcome Tracker · Deployer Alerts      │
├─────────────────────────────────────────────────────────┤
│                 X/Twitter Integration                     │
│  Poster · Intel · Mentions Replier · Reactive Worker     │
│  Tweet Announcer · X Safety Layer                        │
├─────────────────────────────────────────────────────────┤
│               Integration & API Layer                    │
│  Telegram Channel Routing · FastAPI Tools Router         │
│  Reputation System Hooks · Brain Prompt Builder          │
└─────────────────────────────────────────────────────────┘
```

### 4.2 Natural Language Brain

The core brain (`marcus_brain.py`, `marcus_natural_language.py`) processes user input through:

1. **Intent Classification** — Categorizes queries into: `SCAN_TOKEN`, `COMPARE_TOKENS`, `CHECK_WALLET`, `PRICE_CHECK`, `RUG_QUESTION`, `GENERAL_CRYPTO`, `X_SENTIMENT`
2. **Entity Extraction** — Detects contract addresses, token names, wallet addresses, and comparison targets from free-text input
3. **Stoic Persona Responses** — Risk-calibrated output: high-risk verdicts receive stern Stoic warnings, medium-risk gets measured counsel, low-risk receives philosophical encouragement
4. **Intelligence Hooks** — Every scan outcome feeds back into the learning pipeline via `marcus_intelligence.py`

The enhanced system prompt (`marcus_brain_prompt.py`) injects the full knowledge library into every LLM interaction for grounded, consistent analysis.

### 4.3 Knowledge System

Marcus maintains a structured knowledge base in `marcus_knowledge/`:

| Document | Purpose |
|----------|---------|
| `SCAM_PATTERN_LIBRARY.md` | Catalogued scam patterns with signatures, examples, and detection heuristics |
| `FORENSIC_METHODOLOGY.md` | Step-by-step analysis methodology for token forensics |
| `TOOL_CAPABILITY_MANIFEST.md` | Descriptions of all available tools and their capabilities |
| `grounding.py` | Runtime knowledge grounding — injects relevant knowledge into LLM context |

The knowledge system includes a risk assessment matrix with severity levels that standardizes how Marcus evaluates and communicates threat levels.

### 4.4 Intelligence Hub

`marcus_intelligence_hub.py` aggregates signals from multiple independent sources:

- **X/Twitter Sentiment** — Real-time social signal analysis via `marcus_x_intel.py`
- **Polymarket Predictions** — Prediction market data for crypto sentiment
- **Brave Search** — Web intelligence for token and project context
- **Graph Memory** — Persistent relationship graph for deployers, tokens, and wallets
- **Market Data** — On-chain metrics, volume, liquidity, and price feeds

The hub produces a unified intelligence assessment that informs both Marcus's responses and the Marcus Index.

### 4.5 Proactive Intelligence

Marcus doesn't wait for users to ask — he hunts autonomously:

**Discovery Scanner** (`discovery_scanner.py`)
- Monitors pump.fun launches for new token deployments
- Detects volume spikes exceeding 500% in 24 hours
- Tracks KOL wallet buys and whale accumulation patterns
- Rate-limited to 3–4 discovery posts per day to maintain signal quality

**KOL Alpha Engine** (`kol_alpha_engine.py`)
- Fresh Token Radar — KOL buys on tokens less than 1 hour old
- Smart Money Daily Digest — aggregated KOL activity summary
- Exit Signals — detects KOLs dumping tokens that users hold
- KOL Portfolio Tracker — ongoing position monitoring

**Convergence & Shill Detection**
- `kol_convergence_detector.py` — Alerts when multiple KOLs converge on the same token
- `kol_shill_detector.py` — Pattern matching for coordinated, inorganic promotion

**Outcome Tracking** (`marcus_intelligence.py`)
- Tracks whether predictions were accurate over time
- Generates proactive deployer alerts for repeat offenders
- Maintains KOL scorecards based on historical accuracy

### 4.6 Marcus Index

A proprietary daily market risk score (`marcus_index.py`, `marcus_index_worker.py`) aggregating:
- Active rug frequency across monitored chains
- New token deployment velocity
- Holder concentration trends
- Community flag and report volume
- Historical pattern matching
- KOL activity anomalies

### 4.7 X/Twitter Integration

Five specialized services handle the X/Twitter presence:

| Service | Function |
|---------|----------|
| `marcus_x_poster.py` | Posts high-risk token alerts (OAuth 1.0a, X Safety validation) |
| `marcus_x_intel.py` | Searches X for sentiment, KOL mentions, hype, coordinated shill warnings |
| `marcus_mentions_replier.py` | Monitors and replies to @CryptoRugMunch mentions |
| `marcus_reactive_worker.py` | Reactive scanning based on X activity (anti-bot hardened) |
| `marcus_tweet_announcer.py` | Platform announcements |

### 4.8 Safety & Quality Layer

The `x_safety/` module provides a complete safety layer:
- **Reply validation** — Ensures responses meet quality and safety standards before posting
- **CA redirect** — Routes contract address mentions to proper scan flow
- **Thread context** — Maintains conversation context across X thread replies
- **Paste service** — Handles long-form content gracefully
- **Anti-bot hardening** — The reactive worker resists bot manipulation and coordinated trigger attempts
- **Post validation** — Every X post is validated before publishing

### 4.9 Integration Points

- `marcus_integration.py` — Routes scan results to the public @RugMunchIntelligence Telegram channel and feeds the reputation system
- `marcus_tools_api.py` — FastAPI router exposing Marcus tools (X search, web search, graph memory) for internal and external consumption
- `marcus_analysis.py` — Formats full and quick analysis output with Marcus persona styling

### 4.10 Multi-Service Deployment

Marcus runs as 5 dedicated Docker containers, each independently scalable:

| Container | Process |
|-----------|---------|
| `marcus-mentions-stream` | Real-time X mention listener |
| `marcus-rug-quoter` | Rug event commentary generator |
| `marcus-weekly-thread` | Weekly analysis thread publisher |
| `marcus-index-worker` | Daily market risk index calculator |
| `marcus-reactive-worker` | Reactive X activity scanner |

---

## 5. Agent API

### 5.1 x402 Payment Protocol

The Agent API uses the x402 HTTP payment protocol for per-request billing. No API keys, no subscriptions — each request includes payment verification.

### 5.2 Endpoints

| Method | Path | Description | Cost |
|--------|------|-------------|------|
| POST | `/api/agent/v1/check-risk` | Single token risk analysis | $0.01 |
| POST | `/api/agent/v1/check-risk` (premium) | Deep analysis with full breakdown | $0.025 |
| POST | `/api/agent/v1/check-batch` | Batch analysis (up to 20 tokens) | $0.10 |
| GET | `/api/agent/v1/deployer/{addr}` | Deployer history and classification | $0.02 |
| GET | `/api/agent/v1/market-risk` | Marcus Index score | $0.005 |
| GET | `/api/agent/v1/serial-ruggers` | Known serial rugger list | $0.02 |
| GET | `/api/agent/v1/health` | Service health check | Free |

### 5.3 MCP Server

A full Model Context Protocol server (`mcp_server.py`) exposes 13 tools for AI agent integration:

- `check_token_risk` — Standard risk check
- `check_token_risk_premium` — Deep analysis
- `check_batch_risk` — Portfolio screening
- `check_deployer_history` — Deployer intelligence
- Plus 9 additional tools covering holder analysis, KOL detection, market intelligence, and more

Compatible with Claude Desktop, Cursor, Windsurf, and any MCP-compatible client.

---

## 6. Browser Extension

### 6.1 Platform Support
Chrome (Manifest V3), Firefox (WebExtension), Safari (via Xcode conversion).

### 6.2 Features
- **Risk badge injection** — Overlays on DexScreener, Pump.fun, Jupiter, Raydium, BullX, GMGN, Birdeye, Photon
- **Shadow DOM isolation** — Injected UI components don't conflict with host page styles
- **Popup quick scan** — Token analysis without leaving the current page
- **Side panel Marcus chat** — Conversational AI analysis in a browser side panel
- **Phantom deeplink** — One-click wallet integration for Solana
- **Auto-scan** — Automatic analysis on page load (feature flag controlled)

---

## 7. Reputation & Community Intelligence

### 7.1 Reputation System
Users earn reputation points through:
- Accurate scam flags (verified by community votes)
- Successful vote appeals
- Quiz completion and educational progress
- Consistent scanning activity

### 7.2 Community Flagging
- `/flag` — Submit a scam flag with evidence
- `/vote` — Vote on pending flags
- `/appeal` — Challenge a flag decision
- `/voteappeal` — Community review of appeals

### 7.3 League System
Competitive ranking based on scanning activity, flag accuracy, and reputation scores. Visible via `/league` and `/myrank` with shareable rank cards.

---

## 8. Data Sources

| Source | Data Provided |
|--------|--------------|
| Helius RPC | Solana on-chain data, token metadata, transaction history, webhooks |
| DexScreener | Token pair data, pricing, liquidity, volume across all supported chains |
| GoPlus Security | Contract risk analysis — honeypot, mint authority, proxy, restrictions |
| TokenSniffer | Independent contract security scoring |
| Solscan | Supplementary Solana token and account data |
| Jito | MEV bundle detection on Solana |
| Pump.fun | New Solana token launch data |
| X/Twitter API | Social signal monitoring, Marcus posting |

---

## 9. Security Considerations

- **API key management** — Runtime key configuration via bot admin commands (`/setkey`, `/apikeys`)
- **Rate limiting** — Per-user and per-API rate limiting via Valkey
- **Connection pooling** — PgBouncer prevents database connection exhaustion
- **Input sanitization** — Address validation before any API call
- **Cache isolation** — Scan results cached per-token with TTL expiration
- **Known wallet filtering** — DEX/CEX wallets excluded from holder analysis to prevent false positives

---

## 10. Conclusion

CryptoRugMunch is a production-grade, multi-chain token intelligence platform with deep analysis capabilities, AI-powered automation, and multiple distribution channels. The architecture prioritizes parallel data fetching, fault-isolated microservices, and extensible feature modules to maintain analysis speed and reliability as coverage expands.

---

## Contact

- **Telegram**: [@newInstanceOfObject](https://t.me/newInstanceOfObject)
- **X/Twitter**: [@CryptoRugMunch](https://x.com/CryptoRugMunch)
- **Email**: dev.crm.paradox703@passinbox.com
