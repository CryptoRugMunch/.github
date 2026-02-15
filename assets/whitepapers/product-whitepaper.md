# CryptoRugMunch Product Whitepaper

**Version**: 2.0
**Date**: February 2026
**Author**: CryptoRugMunch Development Team

---

## Abstract

CryptoRugMunch is a multi-channel crypto intelligence platform delivering token risk analysis through a Telegram bot, browser extension, Agent API, and MCP server. This whitepaper describes the product design, user experience, feature set, and distribution strategy.

---

## 1. Product Philosophy

**Receipt-first intelligence.** Every claim is backed by on-chain data. CryptoRugMunch doesn't predict — it surfaces evidence and quantifies risk.

**Meet users where they are.** Telegram for traders. Browser extension for DEX users. API for developers and AI agents. MCP server for AI tools.

**Community as infrastructure.** Every scan, flag, vote, and appeal feeds back into the intelligence network. The product improves with use.

---

## 2. Telegram Bot

### 2.1 Core Commands

The bot (`@cryptorugmuncher`) provides 40+ commands organized into functional groups:

**Scanning & Analysis**
- `/scan <address>` — Full multi-chain token risk analysis
- `/compare <addr1> <addr2>` — Side-by-side risk comparison
- `/comparewallets <w1> <w2>` — Cross-chain wallet comparison
- Auto-scan — Paste a contract address, get instant analysis

**Portfolio & Tracking**
- `/portfolio` — View tracked positions with live P&L
- `/addposition` / `/removeposition` — Manage portfolio
- `/trackwallet <address>` — Monitor wallet activity
- `/watch` / `/watchlist` — Token watchlist with priority levels
- `/alerts` / `/createalert` — Custom price and risk alerts

**Community Intelligence**
- `/flag` — Report a suspicious token with evidence
- `/vote` — Vote on pending flags
- `/appeal` — Challenge a flag decision
- `/voteappeal` — Community review of appeals
- `/votewallet` — Vote on wallet reputation

**Reputation & Competition**
- `/myreputation` — View reputation score and history
- `/leaderboard` — Global reputation rankings
- `/league` / `/myrank` — Competitive league system
- `/sharerank` — Share rank card image

**Education**
- `/lesson` / `/learn` — Educational content on spotting scams
- `/quiz` — Interactive knowledge tests
- `/lessons` — Browse all available lessons
- `/myprogress` — Track educational progress

**KOL Management** (Admin)
- `/addkol` / `/removekol` / `/listkols` — Manage tracked influencers
- `/searchkol` / `/kolstats` — KOL intelligence queries

### 2.2 Auto-Scan

Users can paste a contract address in any chat with the bot — no command prefix needed. The bot detects Solana (base58) and EVM (0x) addresses automatically and returns a full analysis.

### 2.3 "You Dodged This"

When a previously scanned token rugs, all users who scanned it receive a DM confirming they dodged the rug. This reinforces the value of scanning and creates a memorable user moment.

### 2.4 Scan Cards

Visual summary cards generated for scan results, shareable as images. Win cards celebrate successful rug avoidance.

---

## 3. Browser Extension

### 3.1 Platforms
Chrome (Manifest V3), Firefox, Safari (iOS + macOS via Xcode conversion).

### 3.2 Risk Badge Injection

The extension injects risk badges directly into the DOM of supported DEX platforms:
- DexScreener
- Pump.fun
- Jupiter
- Raydium
- BullX
- GMGN
- Birdeye
- Photon

Badges are rendered inside Shadow DOM containers to prevent style conflicts with host pages.

### 3.3 Popup & Side Panel

- **Popup** — Quick token scan from any page via the extension icon
- **Side panel** — Marcus AI chat interface for conversational token analysis

### 3.4 Feature Flags

- `EXT_AUTO_SCAN` — Automatic analysis when navigating to a token page
- `EXT_RISK_OVERLAY` — Toggle for risk badge injection

---

## 4. Agent API

### 4.1 Design

HTTP API with x402 payment protocol — no API keys, no subscriptions. Each request carries payment verification. Designed for AI agents, trading bots, and dApp integrations.

### 4.2 Endpoints

| Endpoint | Cost | Use Case |
|----------|------|----------|
| `POST /check-risk` | $0.01 | Pre-trade token screening |
| `POST /check-risk` (premium) | $0.025 | Deep due diligence |
| `POST /check-batch` | $0.10 | Portfolio audit (up to 20) |
| `GET /deployer/{addr}` | $0.02 | Deployer background check |
| `GET /market-risk` | $0.005 | Marcus Index market sentiment |
| `GET /serial-ruggers` | $0.005 | Known bad actor list |
| `GET /health` | Free | Service availability |

### 4.3 MCP Server

Full Model Context Protocol integration with 13 tools. Compatible with Claude Desktop, Cursor, Windsurf, and any MCP client. Enables AI agents to check token risk, analyze deployers, screen portfolios, and query market intelligence through natural tool calling.

---

## 5. Marcus Aurelius — AI Intelligence Engine

### 5.1 Persona & Philosophy
Marcus Aurelius is an LLM-powered Stoic crypto forensics analyst — the AI brain of the CryptoRugMunch platform. His persona is deliberate: a philosopher who examines evidence before passing judgement. High-risk verdicts receive stern Stoic warnings. Low-risk tokens get measured philosophical encouragement. This isn't gimmick — the persona creates memorable, educational interactions that help users internalize risk assessment.

### 5.2 User Interactions

**Natural Language Analysis**
Users interact with Marcus conversationally — paste a contract address, ask "is this token safe?", or query "what's the sentiment on $TOKEN". Marcus classifies intent, pulls data from multiple sources, and responds in character with evidence-backed verdicts.

**Stoic Risk Verdicts**
Every analysis comes with a risk-calibrated Stoic response. A high-risk token might receive: *"The wise man avoids what the fool chases. This deployer has rugged three times before."* This makes risk assessment educational and memorable rather than just a number.

**Cross-Platform Presence**
- **Telegram** — Conversational analysis through the main bot interface
- **X/Twitter** — Autonomous posts, mention replies, weekly threads, rug commentary ([@CryptoRugMunch](https://x.com/CryptoRugMunch))
- **Browser Extension** — Side panel chat for real-time Marcus interaction while browsing DEX platforms
- **Agent API** — Programmatic access to Marcus intelligence for bots and dApps

### 5.3 Proactive Alerts

**"You Dodged This"**
When a previously scanned token rugs, Marcus sends a personalized DM confirming the user dodged it — reinforcing the value of scanning and building trust.

**Discovery Posts**
Marcus autonomously hunts for suspicious new tokens — pump.fun launches, abnormal volume spikes, whale accumulation — and posts findings to X before most traders even know the token exists. Rate-limited to 3–4 posts per day to maintain signal quality.

**KOL Alpha**
- Fresh Token Radar — KOL buys on tokens less than 1 hour old
- Smart Money Daily Digest — what the tracked influencers are buying
- Exit Signals — alerts when KOLs start dumping a token you hold
- Convergence Alerts — multiple KOLs piling into the same token

**Shill Detection**
Marcus detects coordinated, inorganic promotion patterns — multiple accounts promoting the same token in a short window with similar messaging. These warnings appear in scan results and X posts.

### 5.4 Marcus Index

A daily market risk score that gives users an at-a-glance read on overall market conditions. The index aggregates rug frequency, deployment velocity, holder concentration trends, community report volume, and KOL activity anomalies. Available via the Telegram bot, Agent API, and Marcus's X posts.

### 5.5 Outcome Learning

Marcus tracks whether his predictions come true. Over time, this creates deployer scorecards ("this deployer has rugged 3 of 5 tokens"), KOL accuracy ratings, and pattern confidence scores. The system gets smarter with every outcome it observes.

### 5.6 Intelligence Depth

Unlike simple scan tools, Marcus aggregates intelligence from:
- **On-chain data** — Token contracts, holder distributions, LP locks, deployer history
- **X/Twitter sentiment** — Real-time social signal monitoring and hype detection
- **Polymarket predictions** — Prediction market data for crypto sentiment
- **Web search** — Broader context about projects and teams
- **Graph memory** — Persistent relationship tracking across deployers, tokens, and wallets
- **Community intelligence** — Flags, votes, and reputation data from CryptoRugMunch users

This multi-source approach means Marcus doesn't just scan tokens — he understands the broader context around them.

---

## 6. Telegram Mini App

### 6.1 Architecture
FastAPI backend + React frontend, embedded as a Telegram Web App.

### 6.2 Features
- User authentication (Telegram-verified)
- Payment and subscription management (Telegram Stars)
- Referral system with tracking
- Reputation dashboard
- Social features
- Wallet intelligence tools

---

## 7. Reputation & Gamification

### 7.1 Reputation Points
Earned through:
- Accurate scam flags (validated by community votes)
- Educational quiz completion
- Consistent platform usage
- Accurate wallet votes

### 7.2 League System
Competitive rankings updated periodically. Users earn rank based on scanning activity, flag accuracy, and reputation growth. Shareable rank card images for social proof.

### 7.3 Education System
Structured lessons covering common scam patterns, on-chain red flags, and analysis techniques. Interactive quizzes test comprehension. Progress tracking encourages completion.

---

## 8. Distribution Strategy

| Channel | Target User | Value Proposition |
|---------|-------------|-------------------|
| Telegram Bot | Crypto traders | Instant risk analysis without leaving Telegram |
| Browser Extension | DEX users | See risk before you click buy |
| Agent API | Developers, AI agents | Programmatic access to risk intelligence |
| MCP Server | AI tools (Claude, etc.) | Natural language token analysis via tool calling |
| X/Twitter (Marcus) | Crypto community | Free intelligence, brand awareness, community building |

---

## 9. Conclusion

CryptoRugMunch delivers crypto risk intelligence through every channel that matters — messaging, browser, API, and AI tools. The product is built, deployed, and serving users across a genuine multi-service architecture. Growth comes from the compounding value of community intelligence: every scan makes the platform smarter.

---

## Contact

- **Telegram**: [@newInstanceOfObject](https://t.me/newInstanceOfObject)
- **X/Twitter**: [@CryptoRugMunch](https://x.com/CryptoRugMunch)
- **Email**: dev.crm.paradox703@passinbox.com
