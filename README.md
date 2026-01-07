# CryptoRugMunch 🛡️

<div align="center">

  **Catch rugs before they catch you.**

  Telegram-native crypto scam detection platform | Multi-chain support | Community-powered

  [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
  [![Twitter Follow](https://img.shields.io/twitter/follow/CryptoRugMunch?style=social)](https://x.com/CryptoRugMunch)
  [![Telegram](https://img.shields.io/badge/Telegram-Join-blue)](https://t.me/cryptorugmuncher)

</div>

---

## 📖 Overview

CryptoRugMunch is a **Telegram-first crypto scam detection platform** that analyzes Solana, Ethereum, and Base tokens.

**Key Features**:
- 🌐 **Multi-chain** - Solana, Ethereum, Base (BSC, Sui coming soon)
- 🤝 **Community-powered** - Crowdsourced scam reports
- 💰 **Pay-per-scan** - $15-20/scan (vs $99-199/mo competitors)
- 🪙 **$CRM staking** - Stake 10K+ tokens for free unlimited scans

---

## 🎯 Problem & Solution

**Problem**: $10B+ lost to crypto scams in 2024 alone. Existing tools are expensive, complex, and far too often web-only.

**Solution**: Telegram-native bot with instant token risk analysis. No app switching, no monthly fees.

---

## 🏗️ Architecture

CryptoRugMunch is built as a **modular monolith** with clear separation of concerns:

```
┌────────────────┐
│ Telegram Bot   │
├────────────────┤
│ Business Logic │
│ (Scan, Reports,│
│  Payments, API)│
├────────────────┤
│ PostgreSQL +   │
│ Redis Cache    │
├────────────────┤
│ External APIs  │
│ (Helius, etc)  │
└────────────────┘
```

**Tech Stack**:
- Backend: Node.js 20, Fastify, Prisma, BullMQ
- Frontend: Next.js 14, TailwindCSS, shadcn/ui
- Database: PostgreSQL (Supabase), Redis (Upstash)
- Blockchain: Helius (Solana), Alchemy (Ethereum)
- Deployment: Railway (staging) → AWS ECS (production)

---

## 🔬 Risk Scoring Algorithm

CryptoRugMunch analyzes **20 risk metrics** to generate a 0-100 risk score:

1. **Liquidity** - Total USD value in DEX pools
2. **LP Lock** - Liquidity pool lock status
3. **Holder Concentration** - Top 10 holder percentage
4. **Mint Authority** - Can creator mint unlimited tokens?
5. **Freeze Authority** - Can creator freeze wallets?
6. **Honeypot Detection** - Buy/sell tax asymmetry
7. **And loads more advanced / pro metrics...**


---

## 💎 $CRM Token Economics

**Token Status**: ✅ LIVE on Solana mainnet
- **Mint Address**: `Eme5T2s2HB7B8W4YgLG1eReQpnadEVUnQBRjaKTdBAGS`
- **Total Supply**: 1 billion (fixed, immutable)

## 💎 $cryptorugmunch Token Economics

**Token Status**: ✅ LIVE on Zora
- **Mint Address**: `0xd3a0388e4a7ebcbdc2985e2467c91252bbdc01fb`
- **Total Supply**: 1 billion (fixed, immutable)

---

## 📊 Business Model

**Revenue Streams**:
1. **Pay-per-scan**: $15-20/scan (primary revenue)
2. **Pro subscription**: $49/mo unlimited scans
3. **Enterprise API**: $5K-20K/month (Year 2+)

**Financial Projections**:
- Year 1: $72K ARR (600 paying users)
- Year 2: $288K ARR (1,900 paying users)
- Year 3: $720K ARR (3,400 paying users)

**Unit Economics**:
- LTV: $1,500
- CAC: $0-15
- LTV:CAC: 300:1
- Gross Margin: 85%+

---

## 🗺️ Roadmap

**Month 1-2 (Alpha)**: Solana integration, basic risk scoring, 50 users
**Month 3-4 (Beta)**: Multi-chain, community reports, payments, 1K users
**Month 5-6 (Public v1.0)**: API access, viral mechanics, 2K MAU
**Month 7-12 (Scale)**: Advanced features, enterprise API, 10K MAU

---

## 🤝 Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Quick start**:
1. Fork the repo
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file.

---

## 🔗 Links

- **Website**: [cryptorugmunch.com](https://cryptorugmunch.com)
- **Twitter**: [@CryptoRugMunch](https://twitter.com/CryptoRugMunch)

---

## 📧 Contact

- **Telegram**: [@newInstanceOfObject](https://t.me/newInstanceOfObject)
- **Email**: dev.crm.paradox703@passinbox.com
- **Twitter**: [@CryptoRugMunch](https://x.com/CryptoRugMunch)
- **Community**: [Telegram Group](https://t.me/cryptorugmuncher)

---

<div align="center">

  **Built with ❤️ for the crypto community**

  **Protecting users from scams, one scan at a time** 🛡️

</div>
