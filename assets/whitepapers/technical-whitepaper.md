# CryptoRugMunch Technical Whitepaper

**Version**: 2.0
**Date**: February 2026
**Author**: CryptoRugMunch Development Team

---

## Abstract

CryptoRugMunch is a multi-chain crypto token risk analysis platform built on Python/FastAPI with 32 Docker microservices, 98 database tables, and 53 feature modules spanning 150,902 lines of Python across 366 files. This whitepaper describes the architecture, detection methodology, AI integration, and API design of a production system that analyzes tokens across Solana, Ethereum, and Base for rug pull risk, honeypot traps, and deployer fraud.

The platform delivers risk intelligence through four interfaces: a Telegram bot with natural language AI, a browser extension injecting risk badges on 8 DEX platforms, an x402-paywalled Agent API for autonomous AI agents, and a Model Context Protocol (MCP) server exposing 13 tools for AI agent tooling. At its core, a proprietary risk scoring algorithm combines liquidity analysis, holder concentration metrics, Gini coefficient calculations, pattern matching against 8 known rug signatures, and contract authority verification into a single 0–100 risk score.

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [System Architecture](#2-system-architecture)
3. [Risk Scoring Algorithm](#3-risk-scoring-algorithm)
4. [Detection Methodology](#4-detection-methodology)
5. [Marcus Aurelius — AI Intelligence Engine](#5-marcus-aurelius--ai-intelligence-engine)
6. [KOL Intelligence System](#6-kol-intelligence-system)
7. [Database Architecture](#7-database-architecture)
8. [Agent API & MCP Server](#8-agent-api--mcp-server)
9. [Browser Extension](#9-browser-extension)
10. [X/Twitter Integration](#10-xtwitter-integration)
11. [Infographic Generation](#11-infographic-generation)
12. [Reputation & Community Intelligence](#12-reputation--community-intelligence)
13. [Tier System & Access Control](#13-tier-system--access-control)
14. [Security Architecture](#14-security-architecture)
15. [Performance Engineering](#15-performance-engineering)
16. [Data Sources](#16-data-sources)
17. [Conclusion](#17-conclusion)
18. [Contact](#18-contact)

---

## 1. Introduction

### 1.1 Problem Statement

Cryptocurrency scams cost users billions annually. Existing analysis tools are web-only, expensive, and require users to leave their trading workflow. The majority of crypto trading communication happens on Telegram, yet no comprehensive risk analysis tool operates natively within it. Furthermore, the rise of AI agents executing autonomous trades creates a new attack surface — agents need machine-readable risk assessment before every transaction.

### 1.2 Solution

CryptoRugMunch delivers instant, multi-chain token risk analysis through four interfaces:

1. **Telegram Bot** — Command-based and auto-detect scanning with AI-powered natural language interaction
2. **Browser Extension** — Risk badge injection on 8 major DEX platforms via Shadow DOM isolation
3. **Agent API** — x402-paywalled HTTP endpoints for machine consumption (pay-per-request, no API keys required)
4. **MCP Server** — Model Context Protocol integration exposing 13 tools for Claude Desktop, Cursor, Windsurf, and other AI agent platforms

### 1.3 Scale

| Metric | Value |
|--------|-------|
| Python codebase | 150,902 lines across 366 files |
| TypeScript (extension) | 8,231 lines |
| Docker containers | 32 services |
| Database tables | 98 |
| Feature modules | 53 detection capabilities |
| Supported chains | Solana, Ethereum, Base (+Arbitrum, Polygon, Optimism, Avalanche) |
| Marcus AI service files | 17 |
| KOL intelligence files | 14 |
| Rug pattern signatures | 8 with severity/category classification |

---

## 2. System Architecture

### 2.1 Technology Stack

| Layer | Technology |
|-------|-----------|
| Language | Python 3.12 |
| HTTP Framework | FastAPI |
| Bot SDK | python-telegram-bot |
| Database | PostgreSQL 16 + PgBouncer (transaction pooling) |
| Cache/Queue | Valkey 7 (Redis-compatible, LRU eviction, AOF persistence) |
| Anti-Bot | FlareSolverr (headless browser for Cloudflare bypass) |
| Orchestration | Docker Compose (32 containers) |
| Extension | React/TypeScript + Vite (Manifest V3) |
| Mini App | FastAPI backend + React frontend |
| AI/LLM | Google Gemini + Anthropic Claude |
| Graph Database | Neo4j (Marcus relationship memory) |

### 2.2 Full Service Topology — 32 Docker Containers

The platform runs as 32 independently deployable Docker containers, each with its own health checks, restart policies, and resource limits:

```
┌─────────────────────────────────────────────────────────────────────┐
│                        CORE SERVICES (6)                            │
├─────────────────────────────────────────────────────────────────────┤
│  bot              │ Telegram bot — command handling, auto-detect    │
│  api              │ FastAPI backend — Mini App, Agent API, Marcus   │
│  frontend         │ React Mini App — served via Nginx              │
│  postgres         │ PostgreSQL 16 Alpine — primary data store      │
│  pgbouncer        │ Connection pooler — transaction mode, 100 max  │
│  valkey           │ Valkey 7 — cache, queues, rate limits (256MB)  │
├─────────────────────────────────────────────────────────────────────┤
│                    BACKGROUND WORKERS (10)                          │
├─────────────────────────────────────────────────────────────────────┤
│  alert-monitor          │ Real-time price & risk alert delivery     │
│  wallet-tracker         │ Portfolio wallet position monitoring      │
│  reputation-calculator  │ Community reputation score computation    │
│  broadcast-sender       │ Admin broadcast message delivery          │
│  price-updater          │ Periodic price refresh for tracked tokens │
│  blacklist-processor    │ Community blacklist vote processing       │
│  case-study-broadcaster │ Educational rug case study publishing     │
│  rug-autopsy-monitor    │ Automated post-rug forensic analysis     │
│  worker                 │ Async scan queue processor                │
│  infographic-worker     │ AI-generated visual analysis cards        │
├─────────────────────────────────────────────────────────────────────┤
│                    MARCUS AI SERVICES (5)                           │
├─────────────────────────────────────────────────────────────────────┤
│  marcus-mentions-stream  │ Real-time X @mention listener            │
│  marcus-rug-quoter       │ Rug event Stoic commentary generator    │
│  marcus-weekly-thread    │ Weekly analysis thread publisher         │
│  marcus-index-worker     │ Daily market risk index calculator       │
│  marcus-reactive-worker  │ Reactive X activity scanner             │
├─────────────────────────────────────────────────────────────────────┤
│                  INTELLIGENCE SERVICES (7)                          │
├─────────────────────────────────────────────────────────────────────┤
│  intelligence-digest     │ Daily intelligence digest generation     │
│  kol-activity-monitor    │ KOL wallet transaction monitoring       │
│  kol-seeder              │ KOL wallet discovery & seeding          │
│  kol-enricher            │ KOL Twitter/social data enrichment      │
│  marcus-jobs             │ Scheduled Marcus background tasks        │
│  marcus-tweet-announcer  │ Cross-posts tweets to Telegram          │
│  pumpfun-monitor         │ Pump.fun graduation detection           │
├─────────────────────────────────────────────────────────────────────┤
│                    UTILITY SERVICES (4)                             │
├─────────────────────────────────────────────────────────────────────┤
│  smart-alerts            │ Portfolio risk change monitoring         │
│  weekly-health-report    │ Weekly wallet health digest (Sundays)   │
│  agent-watch-checker     │ Agent API webhook delivery              │
│  flaresolverr            │ Anti-bot browser for Cloudflare bypass  │
└─────────────────────────────────────────────────────────────────────┘
```

### 2.3 Data Flow

Token analysis follows a parallel-fetch, sequential-analyze pipeline:

```
                          ┌──────────────┐
                          │  User Input  │
                          │ (CA / query) │
                          └──────┬───────┘
                                 │
                          ┌──────▼───────┐
                          │   Address    │
                          │  Detection   │
                          │ (regex/NLP)  │
                          └──────┬───────┘
                                 │
                          ┌──────▼───────┐
                          │    Chain     │
                          │  Resolution  │
                          └──────┬───────┘
                                 │
               ┌─────────────────┼─────────────────┐
               │                 │                  │
        ┌──────▼──────┐  ┌──────▼──────┐  ┌───────▼──────┐
        │ DexScreener │  │  Helius RPC │  │    GoPlus    │
        │  Pair Data  │  │  On-Chain   │  │   Security   │
        │  (8s max)   │  │  (8s max)   │  │   (8s max)   │
        └──────┬──────┘  └──────┬──────┘  └───────┬──────┘
               │                 │                  │
               └─────────────────┼──────────────────┘
                                 │
                          ┌──────▼───────┐
                          │  Analysis    │
                          │  Pipeline    │
                          │ (53 modules) │
                          └──────┬───────┘
                                 │
                          ┌──────▼───────┐
                          │ Risk Scoring │
                          │   (0-100)    │
                          └──────┬───────┘
                                 │
                    ┌────────────┼────────────┐
                    │            │             │
             ┌──────▼──────┐ ┌──▼───┐ ┌──────▼──────┐
             │ Valkey Cache│ │ DB   │ │  Response   │
             │  (TTL exp)  │ │Persist│ │ Generation  │
             └─────────────┘ └──────┘ └─────────────┘
```

1. **Address detection** — Regex matching for Solana (base58, 32–44 chars) and EVM (0x-prefixed, 40 hex chars) addresses
2. **Chain resolution** — Automatic chain detection from address format and DexScreener pair data
3. **Parallel data fetch** — Concurrent requests to DexScreener, Helius RPC, GoPlus Security, and TokenSniffer with 8-second timeout per source
4. **Analysis pipeline** — Sequential execution through 53 feature modules: rug pattern matching, LP lock verification, holder analysis, bundle detection, wallet clustering, contract security, and more
5. **Risk scoring** — Weighted aggregation of all signals into a 0–100 risk score (see Section 3)
6. **Caching** — Results cached in Valkey with TTL expiration to reduce API credit consumption
7. **Persistence** — Scan history and snapshots stored in PostgreSQL for trend analysis and intelligence learning

---

## 3. Risk Scoring Algorithm

The risk scoring engine is the core intellectual property of CryptoRugMunch. It produces a single 0–100 score where higher values indicate greater rug pull risk. The algorithm combines six weighted signal categories with adaptive thresholds for different chain and market cap profiles.

### 3.1 Score Components

```
Risk Score (0–100) =
    Liquidity Risk       (0–70 pts)   ← Absolute + MC ratio
  + Holder Concentration (0–25 pts)   ← Top 10 holder %
  + Single Holder Risk   (0–30 pts)   ← Largest individual wallet
  + Gini Coefficient     (0–20 pts)   ← Statistical inequality
  + Token Age            (0–12 pts)
  + Authority Risk       (0–26 pts)   ← Freeze (18) + Mint (8)
  + Selling Pressure     (0–12 pts)   ← Buy/sell ratio
  + Pattern Analysis     (0–30 pts)   ← Rug pattern matching
  ─────────────────────────────────
    Capped at 100
```

### 3.2 Liquidity Analysis (0–70 points)

Liquidity is the single most important rug risk indicator — without liquidity, holders cannot exit. The algorithm evaluates both absolute liquidity and the liquidity-to-market-cap ratio:

**Absolute Liquidity (0–40 points):**

| Liquidity (USD) | Risk Points | Assessment |
|-----------------|-------------|------------|
| < $5,000 | 40 | Extreme danger — instant rug risk |
| < $10,000 | 35 | Very high risk |
| < $25,000 | 28 | High risk |
| < $50,000 | 20 | Moderate risk |
| < $100,000 | 12 | Some risk |
| ≥ $100,000 | 0 | Adequate |

**Liquidity-to-Market-Cap Ratio (0–30 points):**

This catches sophisticated rugs where liquidity is drained slowly while market cap remains inflated:

| Liq/MC Ratio | Risk Points | Assessment |
|--------------|-------------|------------|
| < 2% | 30 | Extreme — fake market cap |
| < 5% | 20 | High slippage, manipulation risk |
| < 10% | 10 | Below average |
| ≥ 10% | 0 | Healthy |

**Large-Cap EVM Adjustment:**

For tokens with market cap ≥ $50M on EVM chains (Ethereum, Base, Arbitrum, Polygon, Optimism), the algorithm applies reduced liquidity ratio penalties. This accounts for the reality that established tokens have liquidity distributed across multiple DEXes and CEXes:

```python
if is_large_cap and is_evm_chain:
    # Reduced penalties for established EVM tokens
    if liquidity_ratio < 0.5:   # < 0.5% — still dangerous
        score += 15
    elif liquidity_ratio < 1:
        score += 8
    # 1%+ is acceptable for large-cap EVM
```

### 3.3 Holder Concentration (0–25 points)

Top 10 holder percentage measures how much of the token supply is controlled by the largest wallets:

| Top 10 Holders | Risk Points |
|----------------|-------------|
| > 80% | 25 |
| > 60% | 20 |
| > 40% | 12 |
| > 30% | 6 |
| ≤ 30% | 0 |

Known DEX/CEX wallets (Pump.fun, Raydium, Jupiter, major exchanges) are excluded from holder calculations to prevent false positives.

### 3.4 Single Holder Concentration (0–30 points)

A single wallet holding a disproportionate share is a major rug risk independent of the top-10 metric:

| Top Holder % | Risk Points |
|--------------|-------------|
| > 25% | 30 |
| > 15% | 22 |
| > 10% | 15 |
| > 5% | 8 |
| ≤ 5% | 0 |

### 3.5 Gini Coefficient (0–20 points)

The Gini coefficient provides a statistical measure of wealth inequality across all holders (0 = perfect equality, 1 = one wallet holds everything). The raw Gini risk score (0–25 from the module) is scaled to 0–20 points:

```python
if self.gini_analysis:
    gini_risk = self.gini_analysis.risk_points
    scaled_gini_risk = int(gini_risk * 0.8)
    score += scaled_gini_risk
```

### 3.6 Authority Flags

| Authority | Risk Points | Rationale |
|-----------|-------------|-----------|
| Freeze authority enabled | 18 | Team can freeze ANY wallet, preventing sells |
| Mint authority enabled | 8 | Team can create unlimited tokens, diluting holders |

### 3.7 Pattern Analysis Integration (0–30 points)

The rug pattern library (Section 4.1) runs independently and feeds up to 30 additional risk points based on matched patterns. This catches active rug pulls that the static metrics might miss:

```python
if include_pattern_analysis:
    pattern_analysis = self.analyze_rug_patterns()
    if pattern_analysis and pattern_analysis.total_risk_points > 0:
        pattern_risk = min(30, pattern_analysis.total_risk_points)
        score += pattern_risk
```

### 3.8 Rating Classification

| Score Range | Rating | Emoji |
|-------------|--------|-------|
| 0–14 | SAFE | ✅ |
| 15–29 | LOW RISK | 🟢 |
| 30–49 | MODERATE RISK | 🟡 |
| 50–69 | HIGH RISK | 🟠 |
| 70–100 | EXTREME DANGER | 🔴 |

### 3.9 Rating Elevation

The algorithm includes a safety mechanism that elevates ratings when critical risk factors exist but the numeric score is misleadingly low. If a token has freeze authority enabled (CRITICAL) or extreme liquidity drain, the rating is elevated to at minimum HIGH RISK regardless of the numeric score.

---

## 4. Detection Methodology

### 4.1 Rug Pattern Library

The `RugPatternLibrary` module implements 8 distinct pattern detectors, each classified by severity (`CRITICAL`, `HIGH`, `MEDIUM`, `LOW`) and category (`CONTRACT`, `LIQUIDITY`, `BEHAVIOR`, `SOCIAL`):

| # | Pattern | Severity | Category | Max Points | Detection |
|---|---------|----------|----------|------------|-----------|
| 1 | Freeze Authority | CRITICAL | CONTRACT | 25 | Token contract retains freeze authority — team can freeze any wallet |
| 2 | Mint Authority | HIGH/MEDIUM | CONTRACT | 15 | Token contract retains mint authority — unlimited supply creation |
| 3 | Liquidity Draining | CRITICAL | LIQUIDITY | 30 | Active liquidity removal detected — slow rug in progress |
| 4 | Extreme Concentration | CRITICAL | BEHAVIOR | 25 | Top 10 holders control >80% of supply |
| 5 | Brand New Token | MEDIUM | BEHAVIOR | 10 | Token less than 24 hours old — no track record |
| 6 | Heavy Selling Pressure | HIGH | BEHAVIOR | 15 | Buy/sell ratio < 0.3 — active dumping |
| 7 | Thin Liquidity Ratio | CRITICAL | LIQUIDITY | 30 | Liquidity < 2% of market cap — fake valuation |
| 8 | Price Collapse | CRITICAL | BEHAVIOR | 35 | Price crashed >60% in 24h — potential rug event |

Each pattern detector returns a `PatternMatch` dataclass containing the pattern ID, severity, risk points, user-facing warning, detailed explanation, and remediation advice. The library generates actionable recommendations based on the combination of detected patterns.

### 4.2 The 53 Feature Modules

Each file in the `features/` directory represents an independent detection capability:

**On-Chain Analysis:**

| Module | Capability |
|--------|------------|
| `holder_analysis.py` | Top holder distribution, whale tracking, concentration metrics |
| `holder_flow.py` | Holder growth/decline trends over time |
| `bundle_detection.py` | Multi-wallet coordinated buy detection in same block/slot |
| `first_buyers.py` | First N buyer classification and behavior analysis |
| `early_buyer_tracker.py` | Launch-time buyer tracking — insider dumping detection |
| `fresh_wallet_analyzer.py` | New wallet detection among holders (sybil indicator) |
| `fresh_wallets.py` | Fresh wallet percentage calculation and risk scoring |
| `dev_holdings_tracker.py` | Developer wallet position monitoring |
| `jito_mev.py` | Jito MEV bundle detection on Solana |
| `cex_funding.py` | CEX funding source identification for holder wallets |

**Behavioral Intelligence:**

| Module | Capability |
|--------|------------|
| `wallet_dna.py` | Behavioral fingerprinting — identifies same operator across wallets |
| `cluster_detector.py` | Graph-based wallet clustering — timing, funding, balance patterns |
| `wallet_classifier.py` | Wallet type classification (bot, sniper, team, organic) |
| `wallet_analyzer.py` | Deep wallet transaction history analysis |
| `social_osint.py` | Twitter recycling, domain age, Telegram legitimacy checks |

**Contract Security:**

| Module | Capability |
|--------|------------|
| `goplus_security.py` | GoPlus integration — honeypot, proxy, restrictions |
| `token_sniffer.py` | TokenSniffer independent scoring |
| `contract_security_orchestrator.py` | Multi-source contract audit aggregation |
| `dyn2_detector.py` | Dynamic contract behavior detection |

**Market & Trend:**

| Module | Capability |
|--------|------------|
| `risk_trajectory.py` | Risk score trend over multiple scans |
| `trend_analyzer.py` | Price/volume trend pattern recognition |
| `comparative_scoring.py` | Token-vs-token risk comparison |
| `analytics.py` | Scan analytics and usage metrics |
| `historical_tracker.py` | Historical price/liquidity snapshots |

**Community & Visual:**

| Module | Capability |
|--------|------------|
| `bubblemap_renderer.py` | Visual holder concentration maps |
| `bubblemaps_analysis.py` | Bubblemap data analysis |
| `chart_renderer.py` | Price chart generation |
| `scan_cards.py` | Visual scan result card generation |
| `win_cards.py` | Profit/loss celebration card generation |
| `wall_of_shame.py` | Known scammer showcase |
| `achievements.py` | User achievement tracking |

**KOL & Intelligence:**

| Module | Capability |
|--------|------------|
| `kol_labeling.py` | KOL wallet identification and labeling |
| `kol_monitor.py` | Real-time KOL position monitoring |
| `intelligence_hooks.py` | Auto-learning from scan outcomes |
| `intelligence_auto_approve.py` | Automated intelligence flag approval |
| `auto_flags.py` | Automated scam flagging based on pattern detection |
| `team_sell_alerts.py` | Team wallet sell detection and alerting |
| `whale_alerts.py` | Large transaction alerts |
| `whale_thresholds.py` | Dynamic whale threshold calculation |

### 4.3 Wallet DNA — Behavioral Fingerprinting

The `wallet_dna.py` module creates unique behavioral fingerprints for wallets that enable detection of coordinated activity **even when wallets have never interacted directly on-chain**. Traditional tools detect connections via direct transfers; Wallet DNA detects connections via behavioral similarity.

**DNA Feature Dimensions:**

```
WalletDNA Fingerprint Vector:
├── Timing Profile
│   ├── avg_hour_utc          — Average transaction hour (0-23)
│   ├── hour_entropy           — Spread across hours (0=predictable, 1=random)
│   ├── weekday_bias           — Weekend vs weekday ratio
│   ├── avg_tx_interval        — Average time between transactions
│   └── burst_ratio            — % of transactions in burst patterns (<5min)
├── Trading Style
│   ├── avg_hold_duration      — Average position hold time
│   ├── hold_duration_variance — Consistency of hold times
│   ├── buy_sell_ratio         — Ratio of buys to sells
│   ├── avg_position_size      — Average trade size (SOL)
│   ├── position_size_variance — Trade size consistency
│   ├── num_tokens_traded      — Token diversity
│   └── avg_entry_timing       — How early they enter (0=first, 1=late)
├── DEX Preferences
│   ├── primary_dex            — Most used DEX
│   ├── dex_diversity          — Number of DEXes used
│   ├── uses_aggregator        — Jupiter/1inch usage
│   └── dex_preference_vector  — Per-DEX usage distribution
├── Gas/Priority Patterns
│   ├── avg_priority_fee       — MEV indicator
│   ├── uses_jito              — Jito bundle usage
│   └── avg_compute_units      — Compute budget patterns
├── Token Selection
│   ├── avg_token_age_at_entry — Preference for new vs established tokens
│   ├── mcap_preference        — micro/small/mid/large cap preference
│   ├── prefers_memes          — Meme token affinity score
│   └── chain_diversity        — Multi-chain activity
├── Risk Profile
│   ├── rug_exposure_count     — Tokens that rugged after they held
│   ├── avg_exit_vs_ath        — How close to ATH they sell
│   ├── stop_loss_behavior     — Evidence of stop-loss usage
│   └── diamond_hands_score    — Hold-through-dip tendency
└── Network Behavior
    ├── funding_source_pattern — CEX, DEX, bridge, other wallet
    └── withdrawal_pattern     — Where profits go
```

The fingerprint vector is compared using cosine similarity to identify behaviorally similar wallets across the network.

### 4.4 Cluster Detection — Graph Analysis

The `cluster_detector.py` module identifies groups of wallets exhibiting coordinated behavior through four parallel detection methods:

1. **Timing Clusters** — Wallets buying within the same 60-second window (configurable)
2. **Funding Source Clusters** — Wallets funded from the same parent address
3. **Balance Pattern Clusters** — Wallets holding suspiciously similar balances (within 5% tolerance)
4. **Bundle Launch Detection** — Wallets created together that buy immediately at token launch

Each method runs concurrently and produces independent cluster results. A comprehensive risk score aggregates findings across all methods.

### 4.5 Early Buyer Tracking

The `early_buyer_tracker.py` module analyzes the first N buyers (default: 20) of a token to identify:

- **Insider dumping** — Early buyers who sold >80% within 24 hours
- **Diamond hands** — Early buyers still holding
- **Concentration risk** — Early buyer supply control
- **Dump timing patterns** — Coordinated exit timing

This is critical for distinguishing organic launches from coordinated pump-and-dump operations.

### 4.6 LP Lock Verification

For Solana tokens, LP lock status is verified by:
1. Identifying the LP token address from the trading pair
2. Checking lock program accounts (Raydium lock vaults, etc.)
3. Verifying lock duration and unlock timestamps
4. Reporting lock status, duration, and percentage locked

### 4.7 Contract Security

Multi-source contract analysis via:
- **GoPlus Security API** — Honeypot detection, mint authority, proxy contracts, trading restrictions
- **TokenSniffer** — Independent security scoring and vulnerability detection
- **Jito MEV** — MEV bundle detection for Solana transactions
- **Contract Security Orchestrator** — Aggregates multiple security sources into unified assessment

### 4.8 Deployer Intelligence

Cross-referencing deployer addresses against:
- Historical token deployments by the same address
- Known serial rugger database (community-maintained)
- Deployment frequency and token survival rates
- Connected wallet analysis via cluster detection

---

## 5. Marcus Aurelius — AI Intelligence Engine

Marcus Aurelius is CryptoRugMunch's LLM-powered Stoic crypto forensics analyst — a full intelligence system integrated across the entire platform. Deployed as 5 dedicated Docker containers backed by 17 service files, Marcus combines natural language understanding, multi-source signal aggregation, autonomous threat detection, and outcome learning into a unified AI engine.

### 5.1 Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                     Marcus Brain (LLM Core)                      │
│           Intent Classification · Stoic Persona                  │
│        Natural Language Understanding · Response Gen             │
├───────────────┬───────────────┬──────────────────────────────────┤
│   Knowledge   │  Intelligence │       Content Generation         │
│    System     │      Hub      │                                  │
│ ┌───────────┐ │ ┌───────────┐ │ ┌───────────┐ ┌──────────────┐  │
│ │Scam Lib   │ │ │X Sentiment│ │ │Rug Quoter │ │Weekly Thread │  │
│ │Forensic   │ │ │Polymarket │ │ │Formatter  │ │Publisher     │  │
│ │Manifest   │ │ │Brave Web  │ │ │Analysis   │ └──────────────┘  │
│ │Grounding  │ │ │Graph Mem  │ │ └───────────┘                   │
│ └───────────┘ │ │Market API │ │                                  │
│               │ └───────────┘ │                                  │
├───────────────┴───────────────┴──────────────────────────────────┤
│                   Proactive Intelligence                          │
│    Discovery Scanner · KOL Alpha Engine · Convergence Detector   │
│    Shill Detector · Outcome Tracker · Deployer Alerts            │
├──────────────────────────────────────────────────────────────────┤
│                   X/Twitter Integration                           │
│    Poster · Intel · Mentions Replier · Reactive Worker           │
│    Tweet Announcer · X Safety Layer                              │
├──────────────────────────────────────────────────────────────────┤
│                 Integration & API Layer                           │
│    Telegram Channel Routing · FastAPI Tools Router               │
│    Reputation System Hooks · Brain Prompt Builder                │
└──────────────────────────────────────────────────────────────────┘
```

### 5.2 Natural Language Brain

The core brain (`marcus_brain.py`, `marcus_natural_language.py`) processes user input through:

1. **Intent Classification** — Categorizes queries into 7 intent types:
   - `SCAN_TOKEN` — Contract address analysis request
   - `COMPARE_TOKENS` — Side-by-side token comparison
   - `CHECK_WALLET` — Wallet reputation/history lookup
   - `PRICE_CHECK` — Token price query
   - `RUG_QUESTION` — General scam/security question
   - `GENERAL_CRYPTO` — Broad crypto knowledge query
   - `X_SENTIMENT` — Social sentiment request

2. **Entity Extraction** — Detects contract addresses, token names, wallet addresses, and comparison targets from free-text input

3. **Stoic Persona Responses** — Risk-calibrated output:
   - High-risk verdicts → stern Stoic warnings
   - Medium-risk → measured counsel
   - Low-risk → philosophical encouragement

4. **Intelligence Hooks** — Every scan outcome feeds back into the learning pipeline via `marcus_intelligence.py`

5. **Blacklist Integration** — Cross-references every scanned token against community blacklist and known serial rugger database

6. **KOL Identification** — Identifies KOL wallets among top holders using the `kol_labeler` service

### 5.3 Knowledge System

Marcus maintains a structured knowledge base (`marcus_knowledge/`):

| Document | Purpose |
|----------|---------|
| `SCAM_PATTERN_LIBRARY.md` | Catalogued scam patterns with signatures, examples, detection heuristics |
| `FORENSIC_METHODOLOGY.md` | Step-by-step analysis methodology for token forensics |
| `TOOL_CAPABILITY_MANIFEST.md` | Descriptions of all available tools and capabilities |
| `grounding.py` | Runtime knowledge grounding — injects relevant knowledge into LLM context |

The enhanced system prompt (`marcus_brain_prompt.py`) injects the full knowledge library into every LLM interaction, ensuring grounded, consistent analysis with a risk assessment matrix standardizing threat level communication.

### 5.4 Intelligence Hub

`marcus_intelligence_hub.py` aggregates signals from 5 independent intelligence sources:

1. **X/Twitter Sentiment** — Real-time social signal analysis via X API v2 (`marcus_x_intel.py`). Searches for token mentions, KOL shills, hype patterns, and coordinated promotion campaigns.

2. **Polymarket Predictions** — Crypto-related prediction market data filtered by keyword matching (bitcoin, ethereum, crypto, memecoin, defi, etc.). Identifies high-confidence predictions (>70% or <30% probability) for market sentiment.

3. **Brave Search** — Web intelligence for token and project context. Searches for news, scam reports, team background. Automatically flags results containing warning keywords (scam, rug, hack, exploit, warning, fraud, ponzi).

4. **Graph Memory** — Neo4j-backed persistent relationship graph mapping connections between deployers, tokens, wallets, and events. Enables cross-token intelligence (e.g., "this deployer's last 3 tokens all rugged").

5. **Market Data** — On-chain metrics, volume, liquidity, and price feeds from DexScreener and other sources.

### 5.5 Proactive Intelligence

Marcus operates autonomously, hunting threats before users ask:

**Discovery Scanner** (`discovery_scanner.py`):
- Monitors pump.fun launches for new token deployments
- Detects volume spikes exceeding 500% in 24 hours
- Tracks KOL wallet buys and whale accumulation patterns
- Rate-limited to 3–4 discovery posts per day for signal quality

**KOL Alpha Engine** (`kol_alpha_engine.py`):
- Fresh Token Radar — KOL buys on tokens less than 1 hour old
- Smart Money Daily Digest — Aggregated KOL activity summary
- Exit Signals — Detects KOLs dumping tokens that users hold
- KOL Portfolio Tracker — Ongoing position monitoring

**Outcome Tracking** (`marcus_intelligence.py`):
- Tracks prediction accuracy over time
- Generates proactive deployer alerts for repeat offenders
- Maintains KOL scorecards based on historical accuracy

### 5.6 Marcus Index

A proprietary daily market risk score (`marcus_index.py`, `marcus_index_worker.py`) aggregating:
- Active rug frequency across monitored chains
- New token deployment velocity
- Holder concentration trends
- Community flag and report volume
- Historical pattern matching
- KOL activity anomalies

Published daily via X/Twitter and the `@RugMunchIntelligence` Telegram channel.

### 5.7 Marcus Service Files

The full Marcus system comprises 17 service files:

| File | Role |
|------|------|
| `marcus_brain.py` | Core brain — intent routing, blacklist checks, KOL identification |
| `marcus_natural_language.py` | NLP — intent classification, entity extraction |
| `marcus_brain_prompt.py` | System prompt builder with knowledge injection |
| `marcus_analysis.py` | Analysis output formatting with Stoic persona |
| `marcus_intelligence.py` | Outcome tracking and learning pipeline |
| `marcus_intelligence_hub.py` | Multi-source intelligence aggregation |
| `marcus_integration.py` | Telegram channel routing and reputation hooks |
| `marcus_index.py` | Daily market risk index calculation |
| `marcus_index_worker.py` | Index worker Docker service |
| `marcus_x_poster.py` | X/Twitter OAuth 1.0a posting |
| `marcus_x_intel.py` | X sentiment search and analysis |
| `marcus_mentions_replier.py` | @mention monitoring and reply |
| `marcus_reactive_worker.py` | Reactive X scanning (anti-bot hardened) |
| `marcus_weekly_thread.py` | Weekly analysis thread publisher |
| `marcus_rug_quoter.py` | Rug event commentary generator |
| `marcus_tweet_announcer.py` | Cross-posting tweets to Telegram |
| `marcus_tools_api.py` | FastAPI router for Marcus tools |

### 5.8 Multi-Service Deployment

Marcus runs as 5 dedicated Docker containers:

| Container | Process | Schedule |
|-----------|---------|----------|
| `marcus-mentions-stream` | Real-time X @mention listener | Continuous |
| `marcus-rug-quoter` | Rug event Stoic commentary | Every 600s check |
| `marcus-weekly-thread` | Weekly analysis thread | Mondays 14:00 UTC |
| `marcus-index-worker` | Daily market risk index | Daily 10:00 UTC |
| `marcus-reactive-worker` | Reactive X activity scanner | Continuous |

---

## 6. KOL Intelligence System

CryptoRugMunch operates a comprehensive Key Opinion Leader (KOL) intelligence pipeline spanning 14 files and covering the full lifecycle from wallet discovery to exit tracking.

### 6.1 Pipeline Overview

```
┌────────────┐   ┌────────────┐   ┌─────────────┐   ┌────────────┐
│  Discovery  │──▶│  Seeding   │──▶│  Enrichment │──▶│ Monitoring │
│  & Research │   │  & Import  │   │  (Twitter)  │   │ (On-Chain) │
└────────────┘   └────────────┘   └─────────────┘   └─────┬──────┘
                                                           │
                  ┌────────────────────────────────────────┘
                  ▼
┌────────────┐   ┌────────────┐   ┌─────────────┐   ┌────────────┐
│  Labeling  │◀──│ Convergence│──▶│    Shill    │──▶│    Alpha   │
│  & Wallet  │   │  Detection │   │  Detection  │   │   Engine   │
│   Mapping  │   └────────────┘   └─────────────┘   └────────────┘
└────────────┘
```

### 6.2 Component Files

| File | Stage | Function |
|------|-------|----------|
| `scripts/kol_discovery.py` | Discovery | Automated KOL wallet discovery |
| `scripts/kol_seed_list.py` | Seeding | Curated KOL wallet seed data |
| `scripts/seed_real_kols.py` | Seeding | Production KOL database seeding |
| `scripts/known_kol_wallets.py` | Seeding | Verified KOL wallet mapping |
| `services/kol_seeder.py` | Seeding | Docker service for continuous seeding (GMGN scraping via FlareSolverr) |
| `services/kol_twitter_enricher.py` | Enrichment | Twitter handle and follower data |
| `services/kol_enricher_service.py` | Enrichment | Docker service for KOL data enrichment |
| `features/kol_labeling.py` | Labeling | Wallet → KOL identity mapping |
| `features/kol_monitor.py` | Monitoring | Real-time position tracking |
| `services/kol_convergence_detector.py` | Detection | Multi-KOL buy pattern detection |
| `services/kol_shill_detector.py` | Detection | Coordinated promotion pattern matching |
| `services/kol_alpha_engine.py` | Intelligence | Alpha signal generation |
| `scripts/sync_kol_webhook.py` | Infrastructure | Helius webhook sync for KOL wallets |
| `scripts/test_kol_discovery.py` | Testing | KOL system test suite |

### 6.3 Convergence Detection

The convergence detector (`kol_convergence_detector.py`) monitors for multiple KOLs buying the same token within a time window. Three alert thresholds:

| KOLs | Window | Level | Emoji |
|------|--------|-------|-------|
| 2 | 6 hours | EARLY SIGNAL | 🟡 |
| 3 | 12 hours | CONVERGENCE DETECTED | 🟠 |
| 5+ | 24 hours | COORDINATED PUMP ALERT | 🔴 |

The detector processes events from Helius webhooks, maintains state in Valkey for fast lookups, and filters common tokens (SOL, USDC, USDT, mSOL, JUP, BONK, etc.) to reduce noise.

### 6.4 KOL Database Schema

Five dedicated tables support the KOL intelligence system:

- `kol_wallets` — Wallet addresses, labels, Twitter handles, chains
- `kol_transactions` — Historical transaction records with amounts and types
- `kol_portfolio` — Current position snapshots
- `kol_performance` — Win/loss tracking and accuracy metrics
- `kol_alerts` — Generated alert history

---

## 7. Database Architecture

### 7.1 Overview

CryptoRugMunch uses PostgreSQL 16 as its primary data store with PgBouncer for connection pooling (transaction mode, 100 max connections, 20 default pool size). The schema spans 98 tables organized into functional domains.

### 7.2 Table Domains

**Scan & Analysis (12 tables):**
`scan_log`, `scan_cache`, `scan_analytics`, `scan_cards`, `user_scans`, `token_history`, `token_blacklist`, `buy_events`, `sell_events`, `buy_tracker_config`, `sell_tracker_config`, `fresh_wallet_analysis`

**User & Access (10 tables):**
`user_profiles`, `user_preferences`, `user_settings`, `user_achievements`, `user_reputation`, `user_education_progress`, `user_daily_usage`, `user_tiers`, `user_follows`, `linked_x_accounts`

**Portfolio & Tracking (6 tables):**
`user_portfolio`, `portfolio_snapshots`, `price_alerts`, `alert_rules`, `alert_triggers`, `tracked_wallets`

**Wallet Intelligence (8 tables):**
`wallet_activity`, `wallet_position_cache`, `wallet_reputation_cache`, `wallet_reputation_votes`, `wallet_clusters`, `whale_watch_list`, `whale_holders_snapshot`, `whale_alerts_log`

**Community & Reputation (6 tables):**
`reputation_events`, `blacklist_flags`, `blacklist_votes`, `blacklist_appeals`, `blacklist_appeal_votes`, `bot_stats`

**KOL System (5 tables):**
`kol_wallets`, `kol_transactions`, `kol_portfolio`, `kol_performance`, `kol_alerts`

**Marcus AI (7 tables):**
`marcus_users`, `marcus_usage_log`, `marcus_wallets`, `marcus_payments`, `marcus_referrals`, `marcus_group_licenses`, `cex_addresses`

**Education (5 tables):**
`education_lessons`, `education_quizzes`, `education_quiz_questions`, `education_glossary`, `education_schedule`

**API & Infrastructure (8 tables):**
`api_keys`, `developer_api_keys`, `api_rate_limits`, `rate_limits`, `rate_limit_violations`, `cache_entries`, `cache_statistics`, `migrations`

**Broadcasting & Content (5 tables):**
`broadcasts`, `broadcast_deliveries`, `win_cards`, `win_card_shares`, `win_card_notifications`

**Additional (26 tables):**
`dev_holdings_tracker`, `cex_funding_analysis`, `league_history`, `streak_history`, `tier_events`, plus PostgreSQL migration-generated tables for extended features.

### 7.3 Dual-Write Architecture

The system supports a dual-write mode (`DATABASE_DUAL_WRITE=true`) that writes to both SQLite and PostgreSQL simultaneously, enabling zero-downtime migration between backends. Backend selection is controlled via `DATABASE_BACKEND` environment variable.

---

## 8. Agent API & MCP Server

### 8.1 x402 Payment Protocol

The Agent API uses the x402 HTTP payment protocol for per-request billing. No API keys, no subscriptions — each request includes cryptographic payment verification via Coinbase's facilitator. Supports both EVM (Base) and Solana payment rails.

### 8.2 API Endpoints

| Method | Path | Description | Cost |
|--------|------|-------------|------|
| POST | `/api/agent/v1/check-risk` | Single token risk analysis | $0.005 |
| POST | `/api/agent/v1/check-risk` (premium) | Deep analysis with full breakdown | $0.025 |
| POST | `/api/agent/v1/check-batch` | Batch analysis (up to 20 tokens) | $0.10 |
| GET | `/api/agent/v1/deployer/{addr}` | Deployer history and classification | $0.02 |
| GET | `/api/agent/v1/token-intel/{addr}` | Full token report (price, volume, holders) | $0.02 |
| GET | `/api/agent/v1/holder-deepdive/{chain}/{addr}` | Deep holder analysis with clustering | $0.03 |
| GET | `/api/agent/v1/social-osint/{chain}/{addr}` | Social legitimacy analysis | $0.015 |
| GET | `/api/agent/v1/kol-shills/{addr}` | KOL shill pattern detection | $0.02 |
| GET | `/api/agent/v1/coordinated-buys` | KOL convergence alerts | $0.01 |
| GET | `/api/agent/v1/blacklist/{chain}/{addr}` | Community blacklist check | $0.005 |
| GET | `/api/agent/v1/scammer-check/{addr}` | Known scammer wallet check | $0.005 |
| GET | `/api/agent/v1/market-risk` | Marcus Index daily score | $0.005 |
| GET | `/api/agent/v1/serial-ruggers` | Known serial rugger list | $0.005 |
| GET | `/api/agent/v1/health` | Service health check | Free |

**Response Schema** (check-risk):

```json
{
  "token_address": "full_address",
  "chain": "solana",
  "risk_score": 72,
  "risk_level": "critical",
  "token_name": "Example Token",
  "token_symbol": "EX",
  "price_usd": 0.00042,
  "liquidity_usd": 3200,
  "market_cap": 420000,
  "holder_count": 156,
  "top_10_holder_percent": 78.4,
  "honeypot_risk": false,
  "freeze_authority": true,
  "mint_authority": false,
  "risk_factors": [
    "Freeze authority enabled",
    "Liquidity below $5,000",
    "Top 10 holders control 78.4%"
  ],
  "recommendation": "AVOID"
}
```

### 8.3 MCP Server — 13 AI Agent Tools

The MCP server (`agent_api/mcp_server.py`) implements the Model Context Protocol for seamless integration with Claude Desktop, Cursor, Windsurf, and any MCP-compatible AI client:

| # | Tool | Description | Cost |
|---|------|-------------|------|
| 1 | `check_token_risk` | Standard risk check (0-100 score + recommendation) | $0.01 |
| 2 | `check_token_risk_premium` | Deep analysis with full category breakdown | $0.025 |
| 3 | `check_batch_risk` | Portfolio screening (up to 20 tokens) | $0.10 |
| 4 | `check_deployer_history` | Deployer classification (legitimate_builder/suspicious/serial_rugger) | $0.02 |
| 5 | `get_token_intelligence` | Full report: price, volume, MC, holders, LP, authorities | $0.02 |
| 6 | `get_holder_deepdive` | Sniper detection, Jito bundles, fresh wallet clustering | $0.03 |
| 7 | `get_social_osint` | Twitter recycling, domain age, scam infrastructure cross-ref | $0.015 |
| 8 | `get_kol_shills` | KOL shill pattern detection: buy timing vs shill timing | $0.02 |
| 9 | `get_coordinated_buys` | Multi-KOL convergence on same token (configurable lookback) | $0.01 |
| 10 | `check_blacklist` | Community blacklist lookup | $0.005 |
| 11 | `check_scammer_wallet` | Known scammer/serial rugger check | $0.005 |
| 12 | `get_market_risk_index` | Marcus Index daily market risk score | $0.005 |
| 13 | `get_serial_ruggers` | Serial rug deployer watchlist | $0.005 |

**Claude Desktop Configuration:**

```json
{
  "mcpServers": {
    "rug-munch": {
      "command": "python3",
      "args": ["/path/to/mcp_server.py"],
      "env": {
        "RUG_MUNCH_API_BASE": "https://api.cryptorugmunch.com/api/agent/v1"
      }
    }
  }
}
```

### 8.4 Stablecoin Whitelist

The API includes a hardcoded stablecoin whitelist that returns pre-set low risk scores for known safe tokens (USDC, USDT, WSOL, stSOL, mSOL, JUP, BONK), preventing unnecessary API calls and ensuring consistent results.

---

## 9. Browser Extension

### 9.1 Architecture

The browser extension is built with React/TypeScript (8,231 lines) using Manifest V3 for Chrome, with WebExtension compatibility for Firefox and Safari (via Xcode conversion).

### 9.2 Shadow DOM Isolation

All injected UI components use Shadow DOM encapsulation to prevent conflicts with host page styles. The risk badge, scan overlay, and Marcus chat panel each mount inside their own shadow root, ensuring visual consistency across all supported platforms.

### 9.3 Platform Support — 8 DEX Integrations

| Platform | Integration Type |
|----------|-----------------|
| DexScreener | Risk badge injection on token pair pages |
| Pump.fun | Risk badge on token detail pages |
| Jupiter | Risk overlay on swap interface |
| Raydium | Risk badge on pool/swap pages |
| BullX | Risk badge injection |
| GMGN | Risk badge injection |
| Birdeye | Risk overlay on token pages |
| Photon | Risk badge injection |

### 9.4 Features

- **Risk badge injection** — Visual risk indicator (✅/🟡/🟠/🔴) overlaid directly on DEX token pages
- **Shadow DOM isolation** — Injected UI never conflicts with host page styling
- **Popup quick scan** — Token analysis without leaving the current page
- **Side panel Marcus chat** — Conversational AI analysis in a browser side panel (Chrome Side Panel API)
- **Phantom deeplink** — One-click Solana wallet connection for portfolio integration
- **Auto-scan** — Automatic analysis on page load (feature flag controlled)

---

## 10. X/Twitter Integration

### 10.1 Service Architecture

Five specialized Docker services handle the X/Twitter presence:

| Service | Function |
|---------|----------|
| `marcus_x_poster.py` | OAuth 1.0a authenticated posting of high-risk token alerts |
| `marcus_x_intel.py` | X API v2 search for sentiment, KOL mentions, hype signals |
| `marcus_mentions_replier.py` | Monitors and replies to @CryptoRugMunch mentions |
| `marcus_reactive_worker.py` | Reactive scanning triggered by X activity (anti-bot hardened) |
| `marcus_tweet_announcer.py` | Cross-posts tweets to Telegram community |

### 10.2 X Safety Layer

The `x_safety/` module provides comprehensive guardrails for public X engagement:

**Reply Validator** (`reply_validator.py`):
Ensures all public replies meet quality and safety standards. Validates against Roman Law principles:
- **Veritas** (Truth) — Only state what can be verified
- **Prudentia** (Prudence) — Consider consequences before speaking
- **Gravitas** (Dignity) — Maintain composure under all circumstances

Blocks replies containing trading advice, price predictions, unsourced claims, or aggressive/defensive tone.

**Thread Context Tracker** (`thread_context.py`):
Maintains awareness of which threads Marcus owns, what each thread is about, and reply chain context. Enables intelligent decisions about on-topic vs off-topic replies and when to exercise editorial control.

**CA Redirect Handler** (`ca_redirect.py`):
Detects when users drop contract addresses in reply to Marcus's analysis threads. If the CA is off-topic (different token than the thread's subject), generates a polite redirect to the proper mention flow. Prevents thread derailment and freeloading.

**Paste Service** (`paste_service.py`):
Handles long-form content that exceeds X's character limits via controlled, auditable paste creation with content sanitization.

**Anti-Bot Hardening**:
The reactive worker resists bot manipulation and coordinated trigger attempts. Rate limiting, content validation, and behavioral analysis prevent adversarial actors from weaponizing Marcus's X presence.

---

## 11. Infographic Generation

### 11.1 Visual Analysis Cards

CryptoRugMunch generates AI-powered visual analysis cards for scan results, win celebrations, and market intelligence. The infographic system runs as a dedicated Docker container (`infographic-worker`).

### 11.2 Architecture

| Component | Role |
|-----------|------|
| `services/infographics/worker_unified.py` | Unified queue worker processing all infographic types |
| `services/infographics/v4_generator.py` | Latest generation image generator |
| `services/infographics/prompt_engine.py` | AI prompt engineering for visual layouts |
| `features/scan_cards.py` | Scan result card templates |
| `features/win_cards.py` | Profit/loss celebration cards |
| `features/chart_renderer.py` | Price chart rendering |
| `features/bubblemap_renderer.py` | Holder concentration visualization |

The worker consumes jobs from a Valkey queue, generates images using Gemini for layout prompts and template rendering, and delivers them back to the requesting service (Telegram bot, API, or X poster).

---

## 12. Reputation & Community Intelligence

### 12.1 Reputation System

Users earn reputation points through:
- Accurate scam flags (verified by community votes)
- Successful vote appeals
- Quiz completion and educational progress
- Consistent scanning activity

### 12.2 Community Flagging

- `/flag` — Submit a scam flag with evidence
- `/vote` — Vote on pending flags
- `/appeal` — Challenge a flag decision
- `/voteappeal` — Community review of appeals

### 12.3 League System

Competitive ranking based on scanning activity, flag accuracy, and reputation scores. Visible via `/league` and `/myrank` with shareable rank cards. League history is tracked across seasons.

### 12.4 Education System

Seven interactive rug pattern lessons with quizzes:
- `education_lessons` — Structured lesson content
- `education_quizzes` — Quiz definitions
- `education_quiz_questions` — Question bank
- `education_glossary` — Crypto security terminology
- `education_schedule` — Automated lesson delivery scheduling

---

## 13. Tier System & Access Control

### 13.1 Tier Hierarchy

Seven tiers, strictly monotonic (each tier ≥ all limits of tiers below):

| Tier | Rank | CRM Hold | Stars/mo | SOL/mo | USD/mo |
|------|------|----------|----------|--------|--------|
| 🆓 Free | 0 | — | — | — | — |
| 🥉 Holder | 1 | 100K | 500 ⭐ | 0.05 | $10 |
| ⭐ Scout | 2 | 250K | 750 ⭐ | 0.08 | $15 |
| 🐋 Whale | 3 | 1M | 2,000 ⭐ | 0.22 | $40 |
| ⭐⭐ Analyst | 4 | 2.5M | 3,500 ⭐ | 0.38 | $70 |
| ⭐⭐⭐ Syndicate | 5 | 10M | 5,000 ⭐ | 0.55 | $100 |
| 💎 OG | 6 | 50M | — | — | Invite only |

### 13.2 Access Resolution

Each tier is accessible via three independent paths:
1. **$CRM token holdings** — Hold-to-access, perpetual (checked on-chain)
2. **Telegram Stars** — Monthly or annual subscription (2 months free on annual)
3. **SOL / USDC on-chain payment** — Monthly, used primarily by extension

The highest tier from any source wins. Admins and VIPs map to OG automatically.

### 13.3 Tier Limits

| Feature | Free | Holder | Scout | Whale | Analyst | Syndicate | OG |
|---------|------|--------|-------|-------|---------|-----------|-----|
| Scans/day | 3 | 15 | 30 | ∞ | ∞ | ∞ | ∞ |
| Marcus queries/day | 0 | 3 | 10 | 25 | 50 | ∞ | ∞ |
| Cooldown (sec) | 60 | 30 | 10 | 10 | 0 | 0 | 0 |
| History days | 3 | 7 | 30 | 90 | 90 | ∞ | ∞ |
| Portfolio positions | 3 | 5 | 10 | 30 | 30 | ∞ | ∞ |
| Tracked wallets | 0 | 1 | 2 | 10 | 10 | 50 | ∞ |
| Price alerts | 1 | 3 | 5 | 15 | 15 | ∞ | ∞ |
| Comparison scans | 0 | 0 | 3 | 5 | ∞ | ∞ | ∞ |
| Deep analysis | — | — | Basic | Basic | Full | Full+API | All+Beta |
| API access | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ |
| Priority support | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ | ✓ |
| Beta features | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ | ✓ |

---

## 14. Security Architecture

### 14.1 Rate Limiting

Multi-layer rate limiting implemented via Valkey:

- **Per-user scan limits** — Enforced per tier (3/day free → unlimited for Whale+)
- **Per-user cooldowns** — 60 seconds (free) → 0 seconds (Analyst+)
- **Per-API rate limits** — Agent API free tier: 50/hour; keyed: 1,000/hour
- **Per-feature limits** — Votes (10/hour), flags (5/day), alerts (5/hour), win cards (10/day)
- **Violation tracking** — `rate_limit_violations` table for abuse detection

### 14.2 Connection Pooling

PgBouncer sits between all services and PostgreSQL:
- Transaction pooling mode (connections returned to pool after each transaction)
- 100 max client connections
- 20 default pool size
- Prevents connection exhaustion from 32 concurrent containers

### 14.3 Anti-Bot Infrastructure

- **FlareSolverr** — Dedicated Docker container running a headless browser for bypassing Cloudflare protection on data sources (GMGN, etc.)
- **Configurable delays** — GMGN scraping uses 8-second delays between requests
- **Marcus reactive worker** — Anti-bot hardened against coordinated trigger attempts on X

### 14.4 Input Sanitization

- Address validation via regex before any API call (Solana base58, EVM hex)
- Token address normalization — Solana case-sensitive, EVM lowercased
- Known DEX/CEX wallet filtering in holder analysis
- Stablecoin whitelist bypass for known safe tokens

### 14.5 Cache Security

- Valkey configured with `allkeys-lru` eviction policy at 256MB cap
- AOF persistence for crash recovery
- Scan results cached per-token with TTL expiration
- Separate cache namespaces for scan data, rate limits, and queue jobs

### 14.6 Secret Management

Docker secrets for all sensitive credentials:
- API keys (Birdeye, Helius, Etherscan, Solscan, Brave)
- X/Twitter OAuth credentials (consumer key/secret, access token/secret, bearer token)
- Mini App URL
- Never exposed in environment variables or container logs

### 14.7 X Safety Layer

Complete content safety system for public X engagement (see Section 10.2):
- Reply validation against Roman Law principles
- Thread context awareness
- CA redirect handling
- Content sanitization before paste creation
- Post validation before every X publish

---

## 15. Performance Engineering

### 15.1 Parallel Data Fetching

All external data sources are fetched concurrently using Python's `asyncio`:

```python
# Concurrent fetch with per-source timeout
results = await asyncio.gather(
    fetch_dexscreener(address),     # 8s timeout
    fetch_helius(address),          # 8s timeout
    fetch_goplus(address),          # 8s timeout
    fetch_token_sniffer(address),   # 8s timeout
    return_exceptions=True
)
```

Individual source failures are handled gracefully — a scan completes with partial data rather than failing entirely.

### 15.2 Caching Architecture

| Cache Layer | Backend | TTL | Purpose |
|-------------|---------|-----|---------|
| Scan results | Valkey | Configurable | Reduce API credits on repeat scans |
| Holder data | In-memory | 1 hour | Reduce Helius RPC calls |
| KOL wallet cache | In-memory | Session | Avoid repeated DB lookups |
| Transaction history | In-memory | 1 hour | Reduce Helius RPC calls |
| Funding source | In-memory | 1 hour | Cluster detection optimization |
| API key lookups | Valkey | 5 min | Reduce DB round-trips |

### 15.3 Background Worker Architecture

All long-running or periodic tasks run as independent Docker containers, preventing the main bot and API from blocking on:
- Price updates
- Alert delivery
- Reputation calculation
- Intelligence digest generation
- KOL monitoring
- Infographic rendering

Each worker has its own health check, restart policy (`unless-stopped`), and can be independently scaled or disabled via Docker Compose profiles.

### 15.4 Queue Processing

The async scan queue (`services/queue/scan_processor.py`) runs as a dedicated worker container, consuming scan jobs from Valkey and processing them independently of the bot's message handling loop. This ensures scan latency doesn't impact bot responsiveness.

### 15.5 Database Performance

- PostgreSQL with PgBouncer transaction pooling
- Indexed queries on frequently accessed columns (token_address, user_id, timestamp)
- Normalized address storage (EVM lowercase, Solana original case) for consistent lookups
- Custom JSON encoder for datetime serialization

---

## 16. Data Sources

| Source | Data Provided | Integration |
|--------|--------------|-------------|
| Helius RPC | Solana on-chain data, token metadata, transaction history, webhooks | Direct API + webhooks |
| DexScreener | Token pair data, pricing, liquidity, volume across all chains | REST API |
| GoPlus Security | Contract risk — honeypot, mint authority, proxy, restrictions | REST API |
| TokenSniffer | Independent contract security scoring | REST API |
| Solscan | Supplementary Solana token and account data | REST API |
| Jito | MEV bundle detection on Solana | REST API |
| Pump.fun | New Solana token launch data, graduation events | WebSocket + REST |
| X/Twitter API v2 | Social signal monitoring, mention tracking, posting | OAuth 1.0a + Bearer |
| Polymarket | Crypto prediction market sentiment | REST API |
| Brave Search | Web intelligence for token/project research | REST API |
| GMGN | KOL wallet discovery and seeding | FlareSolverr scraping |
| Birdeye | Token analytics and market data | REST API |
| Etherscan/Basescan | EVM contract verification, deployer data | REST API |
| Neo4j | Relationship graph for deployers, tokens, wallets | Bolt protocol |

---

## 17. Conclusion

CryptoRugMunch is a production-grade, multi-chain token intelligence platform with deep analysis capabilities, AI-powered automation, and multiple distribution channels. The architecture prioritizes:

- **Comprehensive detection** — 53 feature modules covering on-chain analysis, behavioral fingerprinting, contract security, social OSINT, and KOL intelligence
- **Adaptive scoring** — A risk algorithm that adjusts for chain characteristics, market cap, and evolving rug techniques
- **Autonomous intelligence** — Marcus Aurelius hunts threats proactively across Telegram and X/Twitter, learning from every scan outcome
- **Machine-readable risk** — Agent API and MCP server enable AI agents to check risk before every transaction
- **Fault isolation** — 32 independent Docker containers with individual health checks, restart policies, and horizontal scaling capability
- **Data depth** — 98 database tables capturing scan history, wallet intelligence, KOL activity, reputation metrics, and Marcus's learning history

The system continues to expand with new detection modules, additional chain support, and deeper AI integration.

---

## Contact

- **Telegram**: [@newInstanceOfObject](https://t.me/newInstanceOfObject)
- **X/Twitter**: [@CryptoRugMunch](https://x.com/CryptoRugMunch)
- **Email**: dev.crm.paradox703@passinbox.com
