# CryptoRugMunch Economic Whitepaper

**Version**: 2.1
**Date**: February 2026
**Author**: CryptoRugMunch Development Team

---

## Abstract

This document describes the economic model of CryptoRugMunch: the $CRM token, the 7-tier access system, three payment methods, revenue streams, and the Agent API pricing model. CryptoRugMunch is a receipt-first crypto intelligence platform that monetizes through Telegram Stars subscriptions, on-chain payments, and pay-per-request Agent API calls.

---

## 1. $CRM Token

### 1.1 Overview

$CRM is a Solana SPL token that serves as the native utility token of the CryptoRugMunch platform.

| Parameter | Value |
|-----------|-------|
| **Blockchain** | Solana |
| **Mint Address** | `Eme5T2s2HB7B8W4YgLG1eReQpnadEVUnQBRjaKTdBAGS` |
| **Total Supply** | 1,000,000,000 (fixed, immutable) |
| **Treasury Holdings** | 200,000,000 (20%) |
| **Token Standard** | SPL Token |

### 1.2 Utility: Hold-to-Access

$CRM provides **tier eligibility**. Holding $CRM in a verified wallet determines the user's access tier. No staking, no locking — simply hold tokens to qualify.

### 1.3 Distribution

| Allocation | Amount | Percentage |
|-----------|--------|------------|
| Circulating | 800,000,000 | 80% |
| Treasury | 200,000,000 | 20% |

The supply is fixed and immutable. No mint authority exists.

---

## 2. The 7-Tier System

CryptoRugMunch uses a progressive 7-tier access model. Users qualify through $CRM holdings, Telegram Stars subscriptions, or SOL/USDC on-chain payments. The system always applies the **highest qualifying tier**.

### 2.1 Tier Hierarchy

🆓 Free → 🥉 Holder → ⭐ Scout → 🐋 Whale → ⭐⭐ Analyst → ⭐⭐⭐ Syndicate → 💎 OG

### 2.2 Pricing Table

| Tier | $CRM Hold | Stars/mo | Stars/yr | SOL/mo | USDC/mo |
|------|-----------|----------|----------|--------|---------|
| 🆓 Free | 0 | — | — | — | — |
| 🥉 Holder | 100,000 | 500 (~$10) | 5,000 (~$100) | 0.05 | $10 |
| ⭐ Scout | 250,000 | 750 (~$15) | 7,500 (~$150) | 0.08 | $15 |
| 🐋 Whale | 1,000,000 | 2,000 (~$40) | 20,000 (~$400) | 0.22 | $40 |
| ⭐⭐ Analyst | 2,500,000 | 3,500 (~$70) | 35,000 (~$700) | 0.38 | $70 |
| ⭐⭐⭐ Syndicate | 10,000,000 | 5,000 (~$100) | 50,000 (~$1,000) | 0.55 | $100 |
| 💎 OG | 50,000,000 | Hold-only | — | — | — |

**OG tier** is invite-only and requires holding 50M $CRM. It cannot be purchased via Stars or SOL/USDC.

### 2.3 Tier Limits

| Tier | Scans/day | Marcus AI/day | Cooldown | History | Tracked Wallets | Deep Analysis | API Access |
|------|-----------|---------------|----------|---------|-----------------|---------------|------------|
| 🆓 Free | 3 | 0 (1/week) | 60s | 3 days | 0 | none | ❌ |
| 🥉 Holder | 15 | 3 | 30s | 7 days | 1 | none | ❌ |
| ⭐ Scout | 30 | 10 | 10s | 30 days | 2 | basic | ❌ |
| 🐋 Whale | ∞ | 25 | 10s | 90 days | 10 | basic | ❌ |
| ⭐⭐ Analyst | ∞ | 50 | 0s | 90 days | 10 | full | ❌ |
| ⭐⭐⭐ Syndicate | ∞ | ∞ | 0s | ∞ | 50 | full_api | ✅ |
| 💎 OG | ∞ | ∞ | 0s | ∞ | ∞ | full_api_beta | ✅ |

### 2.4 Access Methods

**Three independent paths to tier access** — highest wins:

1. **$CRM Token Holdings** — Hold tokens in a linked Solana wallet. Perpetual access with no recurring cost. Verified on-chain every 6 hours.

2. **Telegram Stars** — Monthly or annual subscription purchased natively through Telegram. No crypto required.

3. **SOL/USDC On-chain** — Monthly payment via Solana. For DeFi-native users who prefer on-chain transactions.

### 2.5 Tier Resolution

```
effective_tier = max(crm_tier, stars_tier, onchain_tier)
```

A user holding 250K $CRM (Scout) with a Whale Stars subscription receives Whale access.

---

## 3. Revenue Model

### 3.1 Revenue Streams

CryptoRugMunch generates revenue through three streams:

**1. Telegram Stars Subscriptions**
- 6 paid tiers from ~$10/mo to ~$100/mo
- Annual plans at ~17% discount
- Processed natively through Telegram (Apple/Google IAP on mobile)

**2. Agent API (x402 Protocol)**
- Pay-per-request pricing for machine-to-machine intelligence
- No API keys or monthly commitments
- Payment verified per request

| Endpoint | Cost |
|----------|------|
| POST /check-risk | $0.01 |
| POST /check-risk (premium) | $0.025 |
| POST /check-batch (20 tokens) | $0.10 |
| GET /deployer/{addr} | $0.02 |
| GET /market-risk | $0.005 |
| GET /serial-ruggers | $0.005 |
| GET /health | Free |

**3. SOL/USDC On-chain Payments**
- Monthly tier access via Solana transactions
- Alternative for users who prefer on-chain payments

### 3.2 Pricing Philosophy

- **Free tier exists** — Everyone gets basic scanning (3 scans/day)
- **Pay for depth** — Higher tiers unlock more analysis modules, not paywalled basics
- **No commitment for API** — x402 pay-per-request removes friction for developers
- **Token alignment** — $CRM holders get perpetual access, aligning long-term holders with usage

---

## 4. Value Drivers

### 4.1 Token Demand

$CRM demand is driven by:
- **Tier qualification** — Frequent users benefit from holding vs recurring subscriptions
- **Cost efficiency** — At Whale tier, holding 1M $CRM = saving $40/mo indefinitely
- **No inflation** — Fixed 1B supply, no minting, no emissions

### 4.2 Platform Network Effects

- More users → richer deployer history → better detection → more users
- Community intelligence (flags, votes) improves with scale
- Agent API creates B2B demand independent of consumer growth

### 4.3 Multi-Channel Distribution

| Channel | User Type | Revenue Path |
|---------|-----------|-------------|
| Telegram Bot | Retail traders | Stars subscriptions |
| Browser Extension | DEX users | Funnel to bot → Stars |
| Agent API | AI agents, bots | x402 pay-per-request |
| MCP Server | Developers | Funnel to API |

---

## 5. Financial Projections Summary

| Metric | Year 1 | Year 2 | Year 3 |
|--------|--------|--------|--------|
| MAU | 8K | 16K | 32K |
| Paid Subscribers | 800 | 2,500 | 7,000 |
| Subscription ARR | $108K | $576K | $1.15M |
| API ARR | $21K | $153K | $540K |
| **Total ARR** | **$129K** | **$729K** | **$1.69M** |
| Gross Margin | 81% | 90% | 91% |

---

## 6. Conclusion

CryptoRugMunch's economic model is built on three pillars:

1. **$CRM hold-to-access** — A utility token that provides perpetual tier access, creating sustained demand without inflation or staking complexity
2. **Telegram Stars subscriptions** — Accessible recurring revenue from non-crypto users
3. **Agent API (x402)** — Innovative pay-per-request pricing for the growing AI agent ecosystem

The 7-tier system with 3 payment methods provides maximum flexibility: crypto-native users hold $CRM, Telegram users pay Stars, DeFi users pay SOL/USDC. Revenue scales with usage, and the community intelligence network becomes more valuable as it grows.

---

## Contact

- **Telegram**: [@newInstanceOfObject](https://t.me/newInstanceOfObject)
- **X/Twitter**: [@CryptoRugMunch](https://x.com/CryptoRugMunch)
- **Email**: dev.crm.paradox703@passinbox.com
