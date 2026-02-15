# CryptoRugMunch Product Whitepaper

**Version**: 2.0
**Date**: February 2026
**Author**: CryptoRugMunch Development Team

---

## Abstract

CryptoRugMunch is a multi-channel crypto intelligence platform delivering token risk analysis, portfolio management, community-driven scam detection, and AI-powered market intelligence. The platform operates across four distribution channels — a Telegram bot, a browser extension for 8 DEX platforms, an Agent API with x402 payment, and an MCP server for AI tool integration. This whitepaper describes the complete product design, feature set, technical architecture, and user experience in detail.

---

## Table of Contents

1. [Product Philosophy](#1-product-philosophy)
2. [Platform Overview](#2-platform-overview)
3. [Telegram Bot — Complete Reference](#3-telegram-bot--complete-reference)
4. [The Scan Experience — What You Actually Get](#4-the-scan-experience--what-you-actually-get)
5. [Portfolio & Position Management](#5-portfolio--position-management)
6. [Marcus Aurelius — AI Intelligence Engine](#6-marcus-aurelius--ai-intelligence-engine)
7. [KOL Intelligence System](#7-kol-intelligence-system)
8. [Community Intelligence Network](#8-community-intelligence-network)
9. [Browser Extension](#9-browser-extension)
10. [Telegram Mini App](#10-telegram-mini-app)
11. [Infographic & Visual Card System](#11-infographic--visual-card-system)
12. ["You Dodged This" — Outcome Alerts](#12-you-dodged-this--outcome-alerts)
13. [Agent API & MCP Server](#13-agent-api--mcp-server)
14. [Tier System & Pricing](#14-tier-system--pricing)
15. [User Journeys](#15-user-journeys)
16. [Distribution Strategy](#16-distribution-strategy)
17. [Conclusion](#17-conclusion)
18. [Contact](#contact)

---

## 1. Product Philosophy

### Receipt-First Intelligence

Every claim is backed by on-chain data. CryptoRugMunch doesn't predict — it surfaces evidence and quantifies risk. When the platform says a token is dangerous, it shows you exactly why: the deployer's history, the holder concentration, the LP lock status, the contract permissions. Users learn to evaluate risk themselves because every scan is an education.

### Meet Users Where They Are

- **Telegram** for traders who live in group chats
- **Browser extension** for DEX users who need risk signals before they click "Buy"
- **Agent API** for developers building trading bots and dApps
- **MCP server** for AI tools like Claude Desktop and Cursor
- **X/Twitter** for the broader crypto community through Marcus's autonomous posts

### Community as Infrastructure

Every scan, flag, vote, and appeal feeds back into the intelligence network. A user in Tokyo flags a suspicious token. A user in London votes to confirm. A user in New York sees the warning in their next scan. The product improves with every interaction — this isn't a database you query, it's a living intelligence network you participate in.

### Stoic Philosophy as UX

Marcus Aurelius isn't a gimmick. The Stoic persona creates memorable, educational interactions that help users internalize risk assessment. A number on a screen is forgettable. *"Even emperors can be deceived — but not by patterns this obvious"* sticks with you. The philosophical framing turns risk data into wisdom.

---

## 2. Platform Overview

CryptoRugMunch is built as a distributed intelligence platform with four user-facing channels and a shared analysis backend:

```
┌──────────────────────────────────────────────────────────────┐
│                    Analysis Engine                            │
│  Risk Scoring · Contract Security · Holder Analysis          │
│  Deployer History · Bundle Detection · Rug Patterns          │
│  KOL Intelligence · Social OSINT · Community Flags           │
└──────────────┬───────────────┬──────────────┬───────────────┘
               │               │              │
    ┌──────────┴──┐   ┌───────┴────┐  ┌──────┴──────┐
    │ Telegram Bot│   │  Browser   │  │  Agent API  │
    │  + Mini App │   │ Extension  │  │ + MCP Server│
    └─────────────┘   └────────────┘  └─────────────┘
```

**Multi-chain support**: Solana (primary), Ethereum, Base, Arbitrum, Polygon, Optimism, Avalanche, and Zora.

**Backend stack**: Python (FastAPI + python-telegram-bot), PostgreSQL, Redis/Valkey, with integrations to DexScreener, Birdeye, GoPlus, TokenSniffer, Helius, and Jito.

---

## 3. Telegram Bot — Complete Reference

The bot (`@cryptorugmuncher`) provides 60+ commands organized into functional groups. Users interact through explicit commands, natural language conversation with Marcus, or simply pasting a contract address for instant analysis.

### 3.1 Scanning & Analysis

| Command | Description |
|---------|-------------|
| `/scan <address>` | Full multi-chain token risk analysis with risk score, holder breakdown, LP status, contract security, deployer history, and rug pattern matching |
| `/compare <addr1> <addr2>` | Side-by-side risk comparison of two tokens |
| `/comparewallets <w1> <w2>` | Cross-chain wallet comparison |
| `/checkwallet <address>` | Wallet reputation and activity analysis |
| `/reputation <address>` | Deep wallet reputation scoring |
| `/holders <address>` | Detailed holder distribution analysis |
| `/bubblemap <address>` | Visual bubble map of holder relationships |
| `/kolmap <address>` | Map KOL holders in a token |
| `/kolnetwork <address>` | Visualize KOL relationship networks |
| `/firstbuyers <address>` | Analyze first 100 buyers for insider/bundle signals (alias: `/fb`) |
| Auto-scan | Paste any contract address — no command needed. Detects Solana (base58) and EVM (0x) addresses automatically |

<!-- Screenshot: Scan result showing risk score, holder chart, and Marcus verdict -->

### 3.2 Portfolio & Tracking

| Command | Description |
|---------|-------------|
| `/portfolio` | View all tracked positions with live P&L calculations |
| `/addposition <token>` | Add a position to your portfolio |
| `/removeposition <token>` | Remove a tracked position |
| `/trackwallet <address>` | Monitor a wallet's activity with alerts |
| `/trackedwallets` | List all wallets you're monitoring |
| `/watch <address>` | Add a token to your watchlist with priority level |
| `/unwatch <address>` | Remove a token from your watchlist |
| `/watchlist` | View your full watchlist with current prices |
| `/tag <token> <label>` | Tag a watched token with a custom label |
| `/watch_config` | Configure watchlist notification preferences |

### 3.3 Price Alerts

| Command | Description |
|---------|-------------|
| `/createalert <token> <condition>` | Create a custom price or risk alert |
| `/alerts` | Alert management overview |
| `/listalerts` | View all active alerts (alias: `/myalerts`) |
| `/deletealert <id>` | Delete a specific alert |
| `/alerthistory` | View triggered alert history |
| `/alerttest` | Test alert delivery |

### 3.4 Community Intelligence

| Command | Description |
|---------|-------------|
| `/flag <address>` | Report a suspicious token with evidence |
| `/vote` | Vote on pending community flags |
| `/flags` | View active flags and their status |
| `/appeal` | Challenge a flag decision with counter-evidence |
| `/voteappeal` | Participate in community appeal reviews |
| `/votewallet` | Vote on wallet reputation |

### 3.5 Reputation & Competition

| Command | Description |
|---------|-------------|
| `/myreputation` | View your reputation score, tier, and history |
| `/leaderboard` | Global reputation rankings |
| `/league` | View current league standings and your division |
| `/myrank` | Your current league rank and progress |
| `/sharerank` | Generate and share a rank card image |
| `/tiers` | View all reputation tiers and requirements |

### 3.6 Education

| Command | Description |
|---------|-------------|
| `/lesson` | Today's rug pattern lesson (alias: `/learn`) |
| `/lessons` | Browse all available lessons (7 structured modules) |
| `/quiz` | Interactive knowledge test on scam detection |
| `/myprogress` | Track educational progress and quiz scores |

### 3.7 Marcus AI

| Command | Description |
|---------|-------------|
| `/marcus_start` | Register for Marcus AI access (aliases: `/mstart`, `/marcusstart`) |
| `/marcus_status` | Check your tier, queries remaining, and account info (aliases: `/mstatus`, `/marcusstatus`) |
| `/marcus_verify <wallet>` | Verify $CRM token holdings for tier access (aliases: `/mverify`, `/marcusverify`) |
| `/marcus_upgrade` | Upgrade tier via Telegram Stars payment (aliases: `/mupgrade`, `/marcusupgrade`) |
| `/marcus_referral` | Get your personal referral link (aliases: `/mreferral`, `/marcusreferral`) |
| `/marcus_stats` | View your Marcus usage statistics (aliases: `/mstats`, `/marcusstats`) |
| Natural language | Just talk to Marcus — ask about any token, paste addresses, or ask crypto questions |

### 3.8 Sell & Activity Tracking

| Command | Description |
|---------|-------------|
| `/tracksells <address>` | Get alerts when a wallet sells a specific token |
| `/untracksells` | Stop tracking sell activity |
| `/listsells` | View active sell tracking subscriptions |
| `/watchme` | Enable personal activity monitoring |
| `/unwatchme` | Disable personal monitoring |
| `/watchstatus` | Check monitoring status |

### 3.9 Social & Sharing

| Command | Description |
|---------|-------------|
| `/wincard <address>` | Generate a win card for a successful rug dodge |
| `/wincards` | View your win card collection |
| `/shareresults` | Share scan results as a formatted image |
| `/linkx` | Link your X/Twitter account |
| `/unlinkx` | Unlink your X/Twitter account |

### 3.10 Token & Utility

| Command | Description |
|---------|-------------|
| `/start` | Welcome message and quick-start guide |
| `/help` | Full command reference |
| `/guide` | Platform usage guide |
| `/tier` | Check your current subscription tier |
| `/verify` | Verify $CRM token holdings |
| `/upgrade` | Upgrade your tier |
| `/myid` | Display your Telegram user ID |
| `/deletemydata` | Request deletion of all personal data (GDPR) |

### 3.11 Admin & KOL Management

| Command | Access | Description |
|---------|--------|-------------|
| `/addkol` | Admin | Add a KOL to the tracking system |
| `/removekol` | Admin | Remove a tracked KOL |
| `/listkols` | Admin | List all tracked KOLs |
| `/searchkol` | Admin | Search KOL database |
| `/kolstats` | Admin | View KOL intelligence statistics |
| `/intelstats` | Admin | Intelligence system statistics |
| `/intelpending` | Admin | Review pending intelligence discoveries |
| `/intelapprove` | Admin | Approve a discovery for posting |
| `/intelreject` | Admin | Reject a discovery |
| `/schedule` | Admin | Schedule broadcast messages |
| `/broadcasts` | Admin | Manage scheduled broadcasts |
| `/announce` | Admin | Send announcements |
| `/config` | Admin | View/modify bot configuration |
| `/stats` | Admin | Platform analytics (alias: `/analytics`) |
| `/cachestats` | Admin | Cache performance metrics |
| `/apikeys` | Admin | Manage API keys |
| `/setkey` | Admin | Set an API key |
| `/testkey` | Admin | Test an API key |
| `/getkeys` | Admin | Retrieve API keys |
| `/testbuy` | Admin | Test buy announcement rendering |

### 3.12 Quick Triggers

In addition to commands, users can type keywords in chat for instant responses:

- **`CA`** — Display $CRM contract addresses
- **`PRICE`** — Live $CRM price across chains
- **`BUY`** — How to buy $CRM with DEX links
- **`LINKS`** — Official links and resources

---

## 4. The Scan Experience — What You Actually Get

A CryptoRugMunch scan isn't a simple "safe/unsafe" label. It's a comprehensive forensic report that examines a token from every angle. Here's what a full scan returns:

### 4.1 Risk Score (0–100)

The headline number. Aggregated from all analysis dimensions using weighted scoring:

| Score Range | Rating | Meaning |
|-------------|--------|---------|
| 0–25 | 🟢 Low Risk | Unusually clean. Proceed with normal caution |
| 26–45 | 🟡 Moderate | Some flags. Research before buying |
| 46–65 | 🟠 Elevated | Multiple warning signs. High caution required |
| 66–85 | 🔴 High Risk | Strong rug indicators. Avoid unless you understand the risks |
| 86–100 | ⛔ Critical | Known scam patterns or confirmed rug. Do not buy |

### 4.2 Contract Security Analysis

Aggregated from three independent sources running in parallel for speed:

**GoPlus Security (Primary)**
- Honeypot detection — can you actually sell after buying?
- Buy/sell tax analysis — hidden taxes that drain your position
- Ownership status — can the owner change balances, take back ownership, or self-destruct the contract?
- Proxy detection — upgradeable contracts that can change behavior post-launch
- Open source verification — is the contract code published and verifiable?
- Hidden owner detection — obfuscated ownership structures

**TokenSniffer Audit**
- Audit score (0–100, higher = safer)
- Letter grade (A through F)
- Similar scam pattern matching — has this contract code been seen in known scams?
- Specific flag enumeration

**Jito MEV Analysis (Solana)**
- Bundle detection — coordinated launch transactions
- Tip analysis — MEV tips paid, indicating sophisticated bot activity
- Bundle count and total tips in SOL

The orchestrator runs all three checks in parallel and aggregates into a single `contract_risk_score`.

### 4.3 Holder Distribution Analysis

- **Top holder concentration** — what percentage do the top 10/20/50 holders control?
- **Holder count** — total unique holders
- **Fresh wallet detection** — newly created wallets holding large positions (insider signal)
- **Cluster detection** — groups of wallets that transact together (coordinated holdings)
- **Whale thresholds** — identification of whale-sized positions
- **CEX funding analysis** — wallets funded from centralized exchanges vs. other sources
- **Dev holdings tracking** — deployer and team wallet positions over time

<!-- Screenshot: Holder distribution pie chart with whale markers -->

### 4.4 Liquidity & LP Analysis

- **Total liquidity** in USD across all pools
- **LP lock status** — is liquidity locked? For how long? Which locker?
- **LP burn verification** — burned LP tokens (permanent lock)
- **Liquidity depth** — how much slippage would a large sell cause?
- **Pool distribution** — liquidity across Raydium, Meteora, Orca, etc.

### 4.5 Deployer History

One of the most powerful signals. The scan cross-references the deployer wallet against the entire database:

- **Total tokens deployed** by this wallet
- **Rug count** — how many of those tokens rugged?
- **Classification**: `legitimate_builder`, `suspicious`, or `serial_rugger`
- **Deployer scorecard** — win/loss record with outcome details
- **Related wallets** — connected deployer addresses through funding patterns

A deployer who has rugged 3 of 5 previous tokens is a 60% rug rate. That context alone can save you.

### 4.6 Bundle & First Buyer Detection

The `/firstbuyers` command (or automatic analysis during scans) examines the first 100 buyers:

- **Buy clustering** — how many bought within the first second, 5 seconds, 30 seconds?
- **Hold distribution** — diamond hands vs. partial sellers vs. dumpers
- **Insider signals** — wallets with suspiciously perfect timing
- **Average initial buy size** — are first buyers committing large or small amounts?
- **Fresh wallet ratio** — what percentage of first buyers used brand new wallets?
- **Funding source analysis** — where did the buy money come from?

Heavy clustering in the first few seconds strongly suggests coordinated launches (bundles), where the deployer or insiders front-run legitimate buyers.

### 4.7 Rug Pattern Library

A systematic pattern detection engine checks every scan against known rug techniques:

**Pattern Categories:**
- **Contract patterns** — honeypot mechanisms, hidden mint functions, blacklist capabilities
- **Liquidity patterns** — unlocked LP, thin liquidity, liquidity removal preparation
- **Behavior patterns** — team dumping, wash trading, artificial volume
- **Social patterns** — recycled Twitter accounts, fake Telegram groups, coordinated shilling

Each pattern has a severity level (Critical, High, Medium, Low) and contributes specific risk points to the overall score. The library includes remediation suggestions — what the project could do to address each concern.

### 4.8 Social OSINT

Beyond on-chain data, the scan checks social legitimacy:

- **Twitter account analysis** — account age, follower quality, recycled handles
- **Domain age** — when was the project website registered?
- **Telegram group analysis** — bot-filled groups, fake member counts
- **Cross-reference with scam infrastructure** — shared hosting, recycled domains, connected social accounts
- **KOL shill detection** — are influencers being paid to promote this token?

### 4.9 Marcus Verdict

Every scan concludes with Marcus Aurelius's risk-calibrated Stoic verdict:

- **High risk**: *"⛔ Memento mori. This token smiles at your portfolio. Walk away."*
- **Medium risk**: *"🟠 Begin each day telling yourself: Today I will meet with interference. This token has plenty."*
- **Low risk**: *"🟢 Unusually clean. Trust, but verify. Even emperors can be deceived."*

The verdict isn't just flavor — it synthesizes the full analysis into a memorable, actionable recommendation.

### 4.10 Community Intelligence Overlay

If the token has been flagged, voted on, or discussed by the CryptoRugMunch community, that context appears in the scan:

- Active flags with evidence
- Community vote results
- Blacklist status
- Related tokens from the same deployer that were previously flagged

---

## 5. Portfolio & Position Management

CryptoRugMunch isn't just a scanner — it's a portfolio management tool that tracks your positions, calculates P&L, and monitors risk continuously.

### 5.1 Position Tracking

`/addposition <token>` tracks a token in your portfolio. The system records:
- Entry price and timestamp
- Current price (live via DexScreener/Birdeye)
- Position size
- Unrealized P&L (absolute and percentage)
- Risk score at time of entry vs. current risk score

`/portfolio` displays all positions in a clean dashboard with live pricing. Positions are color-coded by P&L performance and risk status.

### 5.2 P&L Calculator

The built-in P&L calculator (`features/pnl_calculator.py`) tracks:
- Buy/sell transactions per position
- Cost basis calculation (FIFO)
- Realized vs. unrealized gains
- Total portfolio value over time
- Win rate (% of positions closed in profit)

### 5.3 Wallet Monitoring

`/trackwallet <address>` sets up real-time monitoring of any wallet address. When the tracked wallet makes transactions, you receive alerts:
- Buy/sell notifications with amounts
- New token acquisitions
- Large transfers
- Interaction with known scam contracts

Tier limits control how many wallets you can track simultaneously (0 for free users, up to unlimited for OG tier).

### 5.4 Watchlists with Priority

The watchlist system (`/watch`, `/watchlist`, `/tag`) lets you monitor tokens without tracking a full position:
- Priority levels for notification urgency
- Custom tags for organization (e.g., "researching", "waiting for dip", "team tracking")
- Configurable notification preferences via `/watch_config`
- Risk score change alerts — get notified if a watched token's risk score changes significantly

### 5.5 Price Alerts

The alert system supports multiple condition types:
- Price above/below threshold
- Percentage change (up or down)
- Risk score change
- Volume spike
- Holder count change

Alerts trigger as Telegram DMs with full context about what changed and why.

---

## 6. Marcus Aurelius — AI Intelligence Engine

Marcus Aurelius is the AI brain of CryptoRugMunch — a full LLM-powered Stoic crypto forensics analyst who operates across every platform channel. He is not a chatbot with canned responses. He is an intelligence engine that aggregates data from 6+ sources, learns from outcomes, and generates proactive alpha.

### 6.1 Persona & Philosophy

Marcus's persona is deliberately chosen. The Stoic philosopher-emperor framework creates several advantages:

- **Risk calibration** — Stoic responses naturally scale with danger. High-risk tokens receive stern warnings. Low-risk tokens get measured encouragement.
- **Memorability** — *"The obstacle may be the way, but this obstacle is just a rug"* is more memorable than "Risk Score: 78".
- **Education** — The philosophical framing teaches users to think about risk, not just react to numbers.
- **Trust building** — A character who consistently counsels caution builds more trust than a faceless API.

### 6.2 Natural Language Processing

Marcus understands natural conversation through an intent classification system with 10 intent types:

| Intent | Example | Response |
|--------|---------|----------|
| `SCAN_TOKEN` | "Is this token safe? [address]" | Full scan with Stoic verdict |
| `COMPARE_TOKENS` | "Which is better, X or Y?" | Side-by-side comparison |
| `CHECK_WALLET` | "Check this wallet" | Wallet reputation analysis |
| `PRICE_CHECK` | "What's the price of $TOKEN?" | Live price data |
| `RUG_QUESTION` | "Is this a rug?" | Risk assessment with evidence |
| `X_SENTIMENT` | "What are people saying about $TOKEN?" | X/Twitter sentiment analysis |
| `GENERAL_CRYPTO` | "What's happening in the market?" | Marcus Index + market context |
| `GREETING` | "GM" | "AVE, traveler. What token troubles your soul today?" |
| `HELP` | "What can you do?" | Capability overview |
| `UNKNOWN` | Anything else | "Drop a contract address and I shall reveal its secrets." |

The parser extracts Solana addresses (base58), EVM addresses (0x), and $TICKER symbols automatically from natural text. Users never need to learn command syntax.

### 6.3 Multi-Source Intelligence Aggregation

What makes Marcus powerful is that he doesn't just check one data source. Every analysis pulls from:

1. **On-chain data** — Token contracts, holder distributions, LP locks, deployer history, transaction patterns via Helius, DexScreener, Birdeye
2. **Contract security** — GoPlus, TokenSniffer, and Jito MEV analysis running in parallel
3. **X/Twitter sentiment** — Real-time social signal monitoring, hype detection, shill pattern identification
4. **Polymarket** — Prediction market data for crypto sentiment and event probability
5. **Web search** — Broader context about projects, teams, and associated entities
6. **Graph memory** — Persistent relationship tracking across deployers, tokens, wallets, and KOLs
7. **Community intelligence** — Flags, votes, reputation data, and blacklist status from CryptoRugMunch users
8. **KOL activity** — What tracked influencers are buying, selling, and shilling

This multi-source approach means Marcus understands context that no single API could provide.

### 6.4 Marcus Index — Daily Market Risk Score

A daily market-wide risk metric (0–100) that gives users an at-a-glance read on overall conditions:

**Inputs:**
- Rug frequency (how many rugs detected in the last 24h)
- Deployment velocity (abnormal spikes in new token launches)
- Holder concentration trends (are markets getting more concentrated?)
- Community report volume (spike in flags = something's happening)
- KOL activity anomalies (unusual buying/selling patterns)

**Output:** A single score with interpretation:
- **0–30**: Low risk environment. Normal market conditions.
- **31–60**: Elevated caution. Above-average rug activity.
- **61–100**: High alert. Significant rug wave in progress.

Available via `/scan` context, Agent API (`GET /market-risk`), and Marcus's daily X posts.

### 6.5 Outcome Learning

Marcus doesn't just analyze — he tracks whether his assessments were correct:

- **Deployer scorecards** — Win/loss records for every deployer. "This deployer has rugged 3 of 5 tokens" is data, not prediction.
- **KOL accuracy tracking** — Which influencers' picks actually perform? Which are consistently wrong?
- **Pattern confidence scores** — Over time, the system learns which rug patterns are most predictive.
- **Auto-calibration** — Risk scoring weights adjust based on historical accuracy of each signal.

### 6.6 Cross-Platform Presence

Marcus operates across every CryptoRugMunch channel:

- **Telegram** — Full conversational interface through the bot. Natural language or commands.
- **X/Twitter** ([@CryptoRugMunch](https://x.com/CryptoRugMunch)) — Autonomous posts, mention replies, weekly market threads, rug commentary, discovery posts. Marcus has his own voice on X.
- **Browser extension** — Side panel chat for real-time analysis while browsing DEX platforms.
- **Agent API** — Programmatic access to Marcus intelligence for bots and dApps.
- **MCP server** — Tool calling interface for AI assistants.

### 6.7 Proactive Discovery

Marcus doesn't wait for users to ask. The Discovery Scanner service continuously hunts for interesting tokens:

**Discovery sources:**
- New launches on pump.fun, Raydium, Meteora
- Unusual volume spikes (>500% in 24h)
- KOL wallet buys from tracked wallets
- Whale accumulation patterns

**Filters:**
- Minimum liquidity: $10,000
- Minimum market cap: $50,000
- Maximum risk score: 65 (don't promote high-risk tokens)
- Rate limit: 3–4 discoveries per day (signal quality over quantity)

Discoveries are posted to X with scan summaries and sent to admin channels for review. The intelligence auto-approve system can escalate findings autonomously based on confidence thresholds.

---

## 7. KOL Intelligence System

The KOL (Key Opinion Leader) Intelligence System is one of CryptoRugMunch's most sophisticated features. Spread across 14 code modules, it provides a full pipeline from identifying influencers to generating actionable trading signals.

### 7.1 Architecture

```
KOL Seeding → Wallet Labeling → Activity Monitoring → Signal Generation
     │              │                    │                     │
  Manual +      Link wallets       On-chain tx           Fresh Token Radar
  Auto-seed     to identities      monitoring            Exit Signals
                                                         Convergence Alerts
                                                         Shill Detection
                                                         Daily Digest
```

### 7.2 KOL Database & Labeling

The system maintains a database of tracked crypto influencers with:
- **Identity**: Name, X/Twitter handle, follower count
- **Wallets**: One or more associated wallet addresses (verified through on-chain analysis and labeling)
- **Classification**: Trader, analyst, degen, whale, fund, etc.
- **Accuracy score**: Historical accuracy of their picks
- **Activity status**: Active/inactive with last activity timestamp

KOLs can be added manually via `/addkol` or discovered through on-chain pattern recognition. The labeling system (`features/kol_labeling.py`) identifies KOL wallets among top holders during scans and maintains the wallet-to-identity mapping.

### 7.3 Activity Monitoring

The KOL Monitor (`features/kol_monitor.py`) continuously tracks on-chain activity of all labeled KOL wallets:

- Buy/sell transactions with amounts and timing
- New token acquisitions (especially < 2 hours old)
- Large position changes
- Cross-token activity patterns

### 7.4 Signal Generation — KOL Alpha Engine

The Alpha Engine (`services/kol_alpha_engine.py`) transforms raw KOL activity into actionable signals:

**Fresh Token Radar** ⚡
When a tracked KOL buys a token less than 2 hours old with market cap under $5M:
- Alert includes KOL identity, buy amount, token details, and DexScreener/BullX links
- Urgency levels: 🔴 (3+ KOLs), 🟠 (2 KOLs), ⚡ (1 KOL)
- Deduplication prevents spam (1-hour cooldown per token)
- Cycle: every 2 minutes

**Exit Signals** 🚪
When KOLs start selling tokens you might hold:
- Cross-references KOL sells against admin/user positions
- Alerts include KOL identity, sell size, remaining position
- Early warning system for potential dumps

**Smart Money Daily Digest** 📊
Daily summary of overnight KOL activity:
- What did tracked KOLs buy/sell in the last 24 hours?
- Net flow analysis (accumulating vs. distributing)
- Top tokens by KOL interest
- Delivered at 08:00 UTC daily

**Convergence Alerts** 🎯
When multiple KOLs pile into the same token within a short window:
- Detects 2+ KOLs buying the same token within hours
- Stronger signal than individual buys
- Often precedes significant price movement

### 7.5 Shill Detection

Marcus detects coordinated, inorganic promotion patterns:
- Multiple accounts promoting the same token in a short window
- Similar messaging or copy-paste patterns
- Buy timing vs. shill timing analysis (did the KOL buy before or after shilling?)
- Shill warnings appear in scan results and X posts

This is exposed through the MCP tool `get_kol_shills` and the Agent API endpoint.

### 7.6 KOL Commands

- `/addkol` — Add a KOL with identity and wallet information
- `/removekol` — Remove a tracked KOL
- `/listkols` — List all tracked KOLs with stats
- `/searchkol` — Search the KOL database
- `/kolstats` — View aggregate KOL intelligence statistics
- `/kolmap <token>` — Map KOL holders in a specific token
- `/kolnetwork <token>` — Visualize KOL relationship networks

---

## 8. Community Intelligence Network

CryptoRugMunch treats its user base as a distributed intelligence network. Every user interaction generates signal that makes the platform smarter.

### 8.1 Flag → Vote → Appeal → VoteAppeal Pipeline

**Flagging** (`/flag`)
Any user can flag a suspicious token with evidence. Flags include:
- Token address and chain
- Reason category (rug pull, honeypot, scam, etc.)
- Evidence description
- Supporting links or screenshots

**Voting** (`/vote`)
Community members vote on pending flags:
- Upvote (agree it's suspicious) or downvote (disagree)
- Minimum vote threshold before a flag is confirmed
- Voting accuracy affects your reputation score
- Confirmed flags add warnings to all future scans of that token

**Appeals** (`/appeal`)
Flag subjects (or any user) can challenge a flag decision:
- Counter-evidence submission
- Re-opens the review process

**Appeal Voting** (`/voteappeal`)
Community reviews appeals with the same voting mechanism:
- If the appeal succeeds, the flag is removed
- If rejected, the flag stands with increased confidence
- Appeal outcomes affect the original flagger's reputation

### 8.2 Reputation System

Every user has a reputation score that reflects their contribution quality:

**Earning reputation:**
- Accurate scam flags (validated by community votes)
- Educational quiz completion
- Consistent platform usage
- Accurate wallet votes
- Winning league competitions

**Losing reputation:**
- False flags (voted down by community)
- Inaccurate wallet votes
- Abuse reports

**Reputation tiers** progress automatically based on points:
- Tiers are borrowed from Roman military hierarchy
- Higher tiers unlock community privileges (flag weight, vote influence)
- Visible on leaderboards and rank cards

### 8.3 Wall of Shame

Confirmed rug tokens and their deployers are permanently displayed on the Wall of Shame (`features/wall_of_shame.py`). This creates:
- A public record of scammers
- Cross-reference material for future scans
- Deterrent effect for would-be scammers

### 8.4 League System

The competitive league system (`services/league_manager.py`) adds gamification to platform usage:

**Structure:**
- Weekly leagues with promotion/demotion
- Top 20% promotes to the next tier
- Bottom 20% demotes
- Minimum 1 scan per week to be eligible
- Scaling: single global league below 25 users, tier-specific leagues above

**Scoring:**
- Scanning activity
- Flag accuracy
- Reputation growth
- Educational progress

**Social proof:**
- `/sharerank` generates shareable rank card images
- League standings visible via `/league` and `/leaderboard`

### 8.5 Achievements & Gamification

The achievement system (`features/achievements.py`) rewards milestone behaviors:

**Achievement categories:**
- **Scanning**: First Scan (🔍), Scanner Novice (10 scans, 📊), Scanner Expert (50, 🎯), Scanner Master (100, 👑)
- **Education**: Knowledge Seeker (first lesson, 📚), Scholar (all lessons, 🎓), Quiz Ace (100% score, 💯)
- **Alerts**: Alert Creator (first alert)
- **Community**: Flag contributions, voting participation
- **Portfolio**: Position tracking milestones

Achievement tiers: Bronze → Silver → Gold → Platinum. Each achievement triggers an AI-generated achievement card (see Section 11).

### 8.6 Education System

Seven structured lessons covering:
1. What is a rug pull? Types and mechanics
2. Reading smart contracts for red flags
3. Liquidity analysis and LP locks
4. Holder distribution analysis
5. Social engineering and shill detection
6. Using CryptoRugMunch effectively
7. Advanced: deployer analysis and pattern recognition

Each lesson is followed by an interactive quiz. Progress is tracked via `/myprogress`.

---

## 9. Browser Extension

### 9.1 Overview

The CryptoRugMunch browser extension (8,200+ lines TypeScript) brings risk intelligence directly into DEX trading interfaces. Instead of switching to Telegram to scan a token, users see risk signals injected into the pages they're already using.

### 9.2 Supported Platforms

Risk badge injection is implemented for 8 DEX platforms, each with platform-specific content scripts:

| Platform | File | What's Injected |
|----------|------|-----------------|
| DexScreener | `dexscreener.tsx` | Risk badge on token pages |
| Pump.fun | `pumpfun.tsx` | Risk badge on new launches |
| Jupiter | `jupiter.tsx` | Risk badge in swap interface |
| Raydium | `raydium.tsx` | Risk badge on pool pages |
| BullX | `bullx.tsx` | Risk badge in terminal |
| GMGN | `gmgn.tsx` | Risk badge on token cards |
| Birdeye | `birdeye.tsx` | Risk badge on analytics pages |
| Photon | `photon.tsx` | Risk badge in trading view |

### 9.3 Shadow DOM Injection

Risk badges are rendered inside Shadow DOM containers. This is critical for reliability:
- **Style isolation** — Extension styles don't conflict with host page CSS
- **DOM protection** — Host page JavaScript can't interfere with badge rendering
- **Consistent appearance** — Badges look identical across all 8 platforms regardless of host page theme

### 9.4 Popup Quick Scan

Click the extension icon for an instant token scan:
- Paste any contract address
- View risk score and key findings
- Quick link to full scan in Telegram

### 9.5 Side Panel — Marcus Chat

A persistent side panel provides a full Marcus AI chat interface:
- Conversational analysis while browsing
- Token context auto-detected from the current page
- Persistent chat history within the session

### 9.6 Phantom Deeplink Integration

The extension includes Phantom wallet integration (`walletBridge.ts`):
- Deeplink generation for Phantom mobile wallet
- Wallet connection for $CRM balance verification
- Tier verification without leaving the extension

### 9.7 Feature Flags

- **`EXT_AUTO_SCAN`** — Automatically analyze tokens when navigating to a token page. Hands-free risk assessment.
- **`EXT_RISK_OVERLAY`** — Toggle risk badge injection on/off per platform.

### 9.8 Browser Support

- **Chrome** — Manifest V3, primary platform
- **Firefox** — WebExtension API compatible build
- **Safari** — iOS and macOS via Xcode conversion

---

## 10. Telegram Mini App

### 10.1 Architecture

The Mini App is a Telegram Web App (React frontend + FastAPI backend) providing features that work better in a full UI than in chat messages. The backend consists of 28 Python modules handling authentication, payments, social features, and wallet intelligence.

### 10.2 Authentication

- Telegram WebApp `initData` verification (HMAC-SHA256)
- User identity tied to Telegram account
- Session management with tier-aware middleware
- Security middleware with rate limiting and access guards

### 10.3 Payment Management

`ext_payments.py` handles subscription management:
- Telegram Stars checkout flow
- Monthly and annual subscription options
- Tier upgrade/downgrade management
- Payment history and receipts
- Refund processing (within 14-day window)

### 10.4 Referral System

`ext_referral_api.py` provides:
- Unique referral link generation
- Referral tracking with attribution
- Referral rewards and bonus queries
- Referral leaderboard

### 10.5 Reputation Dashboard

`ext_reputation_api.py` exposes:
- Full reputation score history
- Achievement display
- League standing and progress
- Contribution history (flags, votes, scans)

### 10.6 Wallet Intelligence

Multiple wallet-focused APIs:
- **`wallet_intel_api.py`** — Wallet analysis and intelligence queries
- **`wallet_sync_api.py`** — Wallet synchronization and balance tracking
- **`wallet_verification.py`** — $CRM holdings verification
- **`ext_wallet_api.py`** — Wallet management endpoints
- **`phantom_api.py`** — Phantom wallet deeplink integration

### 10.7 Social Features

`ext_social_api.py` provides:
- Shareable profiles and rank cards
- Social feed of community activity
- Win card sharing
- Achievement announcements

### 10.8 Marcus Chat API

`ext_chat_api.py` and `marcus_api.py`:
- WebSocket-based chat with Marcus
- Conversation history
- Usage tracking and quota management

### 10.9 "You Dodged This" Dashboard

`ext_dodged_api.py`:
- View all tokens you scanned that later rugged
- Estimated money saved
- Dodged rug statistics and timeline

### 10.10 Agent Watch & Analytics

- **`ext_agent_api.py`** — External agent access endpoints
- **`ext_agent_watch.py`** — Agent position watching
- **`ext_agent_analytics.py`** — Agent usage analytics

---

## 11. Infographic & Visual Card System

CryptoRugMunch generates AI-powered visual cards for key moments. These aren't generic templates — they're dynamically generated images with scan data, risk scores, and Stoic commentary baked in.

### 11.1 Card Types

**Scan Cards** (`features/scan_cards.py`)
Generated after every scan with:
- Risk score with color-coded background (green → red gradient)
- Token name, symbol, and chain
- Key risk metrics (contract security, holder concentration, LP status)
- Marcus verdict
- QR code linking to the full scan
- Cyberpunk-themed design (dark backgrounds, cyan/neon accents)

**Win Cards** (`features/win_cards.py`)
Celebration cards when a user successfully dodges a rug:
- "YOU DODGED THIS" headline
- The scan date vs. the rug date
- Estimated loss avoided
- Risk score at time of scan
- Shareable on social media

**Shame Cards**
For the Wall of Shame — documenting confirmed rug deployers:
- Deployer address and rug count
- Tokens rugged with dates
- Total estimated losses
- "SERIAL RUGGER" classification

**Alert Cards**
Visual alerts for significant events:
- KOL convergence on a token
- Major risk score changes
- Discovery posts

**Achievement Cards**
Triggered by the achievement system:
- Achievement name and description
- Tier badge (bronze/silver/gold/platinum)
- User's achievement collection progress

### 11.2 Generation Pipeline

Cards are generated through a request queue:
1. Scan/event triggers a card request
2. Request is pushed to a Redis queue (`marcus:infographic:requests`)
3. The card generator processes requests asynchronously
4. Generated images are stored and served to users
5. Rate limiting prevents abuse (tier-dependent daily limits)

### 11.3 V4 Generator

The latest card generator uses prompt engineering for AI-generated visual elements combined with Pillow-based data overlay. The design system includes:
- Consistent color palette (dark backgrounds with cyan, neon pink, and teal accents)
- Risk-adaptive coloring (green → yellow → orange → red → critical pink)
- Formatted numbers (K/M/B abbreviations, appropriate decimal precision)
- QR codes for quick links

---

## 12. "You Dodged This" — Outcome Alerts

### 12.1 Concept

When a token that a user previously scanned is confirmed as rugged, they receive a personalized DM celebrating that they dodged it. This is one of the most powerful engagement loops in the platform.

### 12.2 How It Works

**Detection Pipeline:**
1. The autopsy monitor continuously watches for rug events (price drops >90%, liquidity removal, etc.)
2. When a rug is confirmed, a `rug_autopsy` record is created with severity, price drop percentage, peak price, current price, estimated total losses, and affected holder count
3. The "You Dodged This" service (`services/you_dodged_this.py`) is triggered

**User Matching:**
4. The service queries `scan_log` for all users who scanned this token BEFORE the rug
5. Only includes users who received a risk score ≥ 40 (they got a meaningful warning)
6. Deduplicates by user (one alert per user per rug)

**Alert Delivery:**
7. Each matching user receives a personalized DM containing:
   - Token name and symbol
   - Their scan date and the risk score they received
   - The rug date and severity
   - Price drop percentage (e.g., "99.7% crash")
   - Estimated loss they would have suffered
   - Number of holders affected
   - A Marcus Stoic celebration quote

### 12.3 Feature Gating

The feature uses a staged rollout system:
- **OFF** → Feature disabled
- **INTERNAL** → Admin-only testing
- **BETA** → Selected users
- **GA** → All users

Controlled by the `YOU_DODGED_THIS` feature flag.

### 12.4 Why This Matters

This feature closes the feedback loop. Most risk tools are fire-and-forget — you scan, you see a number, you move on. You never know if the scan was right. "You Dodged This" proves the value of scanning and creates:
- **Viral moments** — Users share dodged-rug screenshots on social media
- **Habit reinforcement** — Every dodge reinforces the scanning behavior
- **Trust building** — The platform proves it's right with receipts
- **Win card generation** — Dodged rugs trigger shareable win cards

---

## 13. Agent API & MCP Server

### 13.1 Agent API — x402 Payment Protocol

The Agent API provides programmatic access to CryptoRugMunch's intelligence for developers, trading bots, and dApp integrations.

**Design philosophy:** No API keys. No subscriptions. No registration. Each request carries x402 payment verification. If you can pay, you can scan. This makes CryptoRugMunch instantly accessible to any AI agent or bot.

**Endpoints:**

| Endpoint | Method | Cost | Description |
|----------|--------|------|-------------|
| `/check-risk` | POST | $0.01 | Standard token risk analysis |
| `/check-risk` (premium) | POST | $0.025 | Deep analysis with full breakdown, deployer cross-reference, social OSINT, holder intelligence |
| `/check-batch` | POST | $0.10 | Batch screening up to 20 tokens |
| `/deployer/{addr}` | GET | $0.02 | Deployer history and classification |
| `/market-risk` | GET | $0.005 | Marcus Index — daily market risk score |
| `/serial-ruggers` | GET | $0.005 | Known serial rugger watchlist |
| `/health` | GET | Free | Service availability check |

**Payment flow:**
1. Agent sends request with x402 payment header
2. Payment is verified on-chain
3. Analysis runs
4. Results returned in structured JSON

**Response format:** All endpoints return structured JSON with risk scores, evidence arrays, and actionable recommendations. Designed for machine consumption — no Markdown, no Stoic quotes (unless you want them).

### 13.2 MCP Server — 13 Tools

The MCP (Model Context Protocol) server enables AI assistants to use CryptoRugMunch as a tool. Compatible with Claude Desktop, Cursor, Windsurf, and any MCP client.

**Available tools:**

| Tool | Cost | Description |
|------|------|-------------|
| `check_token_risk` | $0.01 | Standard risk check with SAFE/CAUTION/AVOID recommendation |
| `check_token_risk_premium` | $0.025 | Full deep analysis with category breakdown |
| `check_batch_risk` | $0.10 | Portfolio screening (up to 20 tokens) |
| `check_deployer_history` | $0.02 | Deployer classification and track record |
| `get_token_intelligence` | $0.02 | Full token report: price, volume, holders, LP, authorities |
| `get_holder_deepdive` | $0.03 | Sniper detection, bundle analysis, cluster detection, whale concentration |
| `get_social_osint` | $0.015 | Social legitimacy: Twitter recycling, domain age, Telegram analysis |
| `get_kol_shills` | $0.02 | KOL shill pattern detection with buy vs. shill timing |
| `get_coordinated_buys` | $0.01 | Multi-KOL convergence detection |
| `check_blacklist` | $0.005 | Community blacklist check |
| `check_scammer_wallet` | $0.005 | Known scammer/serial rugger wallet check |
| `get_market_risk_index` | $0.005 | Daily market-wide rug risk score |
| `get_serial_ruggers` | $0.005 | Serial rug deployer watchlist |

**Example interaction with Claude Desktop:**

> User: "Is this token safe? 7xKXtg2CW87d97TXJSDpbD5jBkheTqA83TZRuJosgAsU"
>
> Claude: *[calls check_token_risk]* "This token has a risk score of 73/100 (High Risk). The deployer has previously rugged 2 of 3 tokens, holder concentration is 78% in top 10 wallets, and LP is unlocked. I'd strongly recommend avoiding this one."

---

## 14. Tier System & Pricing

CryptoRugMunch uses a 7-tier system. Every paid tier is accessible via three paths: $CRM token holdings (hold-to-access, perpetual), Telegram Stars subscription (monthly/annual), or SOL/USDC on-chain payment. The highest tier from any source wins.

### 14.1 Tier Overview

| Tier | $CRM Hold | Stars/mo | SOL/mo | USD/mo |
|------|-----------|----------|--------|--------|
| 🆓 Free | 0 | — | — | — |
| 🥉 Holder | 100K | 500 ⭐ | 0.05 | $10 |
| ⭐ Scout | 250K | 750 ⭐ | 0.08 | $15 |
| 🐋 Whale | 1M | 2,000 ⭐ | 0.22 | $40 |
| ⭐⭐ Analyst | 2.5M | 3,500 ⭐ | 0.38 | $70 |
| ⭐⭐⭐ Syndicate | 10M | 5,000 ⭐ | 0.55 | $100 |
| 💎 OG | 50M | — | — | Invite only |

Annual subscriptions available at ~17% discount (2 months free).

### 14.2 Feature Limits by Tier

| Feature | Free | Holder | Scout | Whale | Analyst | Syndicate | OG |
|---------|------|--------|-------|-------|---------|-----------|-----|
| Scans/day | 3 | 15 | 30 | ∞ | ∞ | ∞ | ∞ |
| Marcus queries/day | 0* | 3 | 10 | 25 | 50 | ∞ | ∞ |
| Cooldown (sec) | 60 | 30 | 10 | 10 | 0 | 0 | 0 |
| History (days) | 3 | 7 | 30 | 90 | 90 | ∞ | ∞ |
| Portfolio positions | 3 | 5 | 10 | 30 | 30 | ∞ | ∞ |
| Tracked wallets | 0 | 1 | 2 | 10 | 10 | 50 | ∞ |
| Price alerts | 1 | 3 | 5 | 15 | 15 | ∞ | ∞ |
| Win cards/day | 1 | 3 | 5 | ∞ | ∞ | ∞ | ∞ |
| Comparisons/day | 0 | 0 | 3 | 5 | ∞ | ∞ | ∞ |
| Deep analysis | — | — | Basic | Basic | Full | Full+API | Full+API+Beta |
| API access | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ |
| Priority support | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ |
| Beta features | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ |

*Free tier gets 1 Marcus query per week as a teaser.

### 14.3 Tier Resolution

When a user has multiple access paths (e.g., holding 300K $CRM and paying for Scout via Stars), the system resolves to the highest tier. A user holding 1M $CRM who also subscribes to Analyst gets Analyst features. VIP and Admin users map to OG tier.

---

## 15. User Journeys

### 15.1 Journey A: Retail Trader Scanning Before Buying

**Scenario:** Alex sees a token being shilled in a Telegram group. Before buying, they want to check if it's safe.

1. Alex opens the CryptoRugMunch bot (`@cryptorugmuncher`)
2. Pastes the contract address — no command needed
3. Within 5 seconds, receives a full scan:
   - Risk Score: 72/100 (🔴 High Risk)
   - Contract: Honeypot detected by GoPlus — sell tax is 99%
   - Deployer: Has rugged 2 of 3 previous tokens
   - Holders: Top 3 wallets hold 67% of supply
   - LP: Unlocked, deployer can pull at any time
   - Marcus verdict: *"⛔ Memento mori. This token smiles at your portfolio. Walk away."*
4. Alex decides not to buy
5. Two days later, receives a "You Dodged This" DM:
   - *"The token you scanned rugged yesterday. 99.3% price crash. 2,847 holders affected. Estimated loss avoided: $500. Your scan saved you."*
6. Alex shares the win card on X. Their friend joins the bot.

**Time invested:** 5 seconds for the scan. Value received: potentially hundreds of dollars saved.

### 15.2 Journey B: DEX User with Browser Extension

**Scenario:** Maya trades actively on DexScreener and BullX. She installs the CryptoRugMunch extension.

1. Maya installs the extension from the Chrome Web Store
2. Navigates to DexScreener to browse trending tokens
3. Risk badges appear automatically on token pages:
   - 🟢 Low risk tokens show green badges
   - 🟠 Elevated risk tokens show orange badges with warning count
   - 🔴 High risk tokens show red badges with "AVOID" recommendation
4. She clicks on a token that interests her — the badge shows "Risk: 34 (Moderate)"
5. She opens the side panel for a deeper conversation with Marcus
6. Asks: "What about the deployer?"
7. Marcus responds with deployer history — clean record, 4 tokens deployed, all still active
8. Maya decides to buy, uses the Phantom deeplink integration to execute the trade
9. She keeps the extension's auto-scan enabled — every new token page she visits is analyzed automatically

**Experience:** Risk intelligence is ambient. Maya never leaves her trading workflow.

### 15.3 Journey C: AI Agent Using the API

**Scenario:** A trading bot needs to screen tokens before executing trades automatically.

1. The bot's risk management module calls the MCP server's `check_token_risk` tool
2. Passes the token address and chain
3. Receives structured JSON:
```json
{
  "risk_score": 23,
  "risk_level": "low",
  "recommendation": "SAFE",
  "honeypot": false,
  "deployer_rug_count": 0,
  "top10_holder_pct": 31.2,
  "lp_locked": true,
  "lp_lock_duration_days": 365,
  "contract_verified": true,
  "flags": []
}
```
4. Risk score is below threshold (50) — bot proceeds with the trade
5. For portfolio screening, the bot calls `check_batch_risk` with all 15 held positions
6. One position returns risk_score 68 — the bot flags it for human review
7. The bot checks `get_market_risk_index` daily — on high-risk days (>60), it reduces position sizes automatically

**Integration effort:** 13 MCP tools, no API keys needed, x402 payment per call. Works with Claude Desktop, Cursor, or any custom MCP client.

---

## 16. Distribution Strategy

| Channel | Target User | Value Proposition | Status |
|---------|-------------|-------------------|--------|
| Telegram Bot | Crypto traders | Instant risk analysis without leaving Telegram | Live |
| Browser Extension | DEX users | See risk before you click buy | Live (Chrome, Firefox, Safari) |
| Agent API | Developers, trading bots | Programmatic risk intelligence with x402 payment | Live |
| MCP Server | AI tools (Claude, Cursor) | Natural language token analysis via tool calling | Live |
| X/Twitter (Marcus) | Crypto community | Free intelligence, brand awareness, rug commentary | Live |
| Telegram Mini App | All users | Rich UI for payments, reputation, wallet tools | Live |

### Growth Flywheel

```
More users scanning → More community intelligence → Better risk scores
     ↑                                                      ↓
More "You Dodged This" wins ← More accurate predictions ←──┘
     ↓
More social sharing → More new users → (repeat)
```

Each component reinforces the others. The product gets smarter with every user, and every user's success becomes marketing for the next user.

---

## 17. Conclusion

CryptoRugMunch delivers crypto risk intelligence through every channel that matters — messaging, browser, API, and AI tools. The platform combines:

- **53 feature modules** powering token analysis, holder intelligence, bundle detection, rug pattern matching, social OSINT, and more
- **Marcus Aurelius** — an AI engine that aggregates 8 intelligence sources, learns from outcomes, and generates proactive alpha
- **KOL Intelligence** — a full pipeline from influencer identification to actionable trading signals
- **Community Intelligence** — a flag/vote/appeal system that turns every user into a sensor
- **Multi-channel distribution** — Telegram, browser extension (8 DEX platforms), Agent API, MCP server, and X/Twitter
- **Gamification** — leagues, achievements, reputation, and win cards that make safety engaging

The product is built, deployed, and serving users across a genuine multi-service architecture. Growth comes from the compounding value of community intelligence: every scan makes the platform smarter, and every dodged rug proves it.

---

## Contact

- **Telegram**: [@newInstanceOfObject](https://t.me/newInstanceOfObject)
- **X/Twitter**: [@CryptoRugMunch](https://x.com/CryptoRugMunch)
- **Email**: dev.crm.paradox703@passinbox.com
