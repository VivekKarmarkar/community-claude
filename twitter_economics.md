# Twitter/X Data Access Economics

Our use case: Read tweets from ~10-20 Claude Code team accounts, a few times per day.
Estimate: ~1,800 timeline requests/month, ~36,000 tweets/month.

---

## Official Twitter/X API

| Tier | Monthly Cost | Read Cap | Can Read Other Users' Timelines? |
|------|-------------|----------|----------------------------------|
| **Free** | $0 | Extremely limited | **NO** - only your own profile |
| **Basic** | **$200/mo** | 15,000 tweets | Yes (up to 3,200 per user) |
| **Pro** | **$5,000/mo** | 1,000,000 tweets | Yes |
| **Enterprise** | **$42,000-50,000+/mo** | Custom | Yes |
| **Pay-Per-Use** (new Feb 2026) | Variable | 2M cap | TBD - worth investigating |

**Verdict:** Free tier is useless for our case. Basic at $200/mo is the minimum - way too expensive for what we need.

---

## Third-Party APIs (No Official Twitter API Key Needed)

| Service | Monthly Cost | Reliability | Notes |
|---------|-------------|-------------|-------|
| **Xpoz.ai** | **$0 (free tier)** | TBD | 100K results/mo free. MCP-based interface - needs verification on REST availability |
| **SociaVault** | **~$4** | Good | Pay-as-you-go, $0.002/request, credits never expire |
| **TwitterAPI.io** | **~$6** | Excellent | 99.99% uptime, ~800ms response, drop-in replacement for official API |
| **SocialData** | **~$7** | Good | $0.0002/tweet, also has monitoring API |
| **Apify** | **~$7-14** | Medium | Scraper-based, $5 free credits/mo |
| **TweetAPI.com** | **$17** | Good | Fixed monthly, includes write access |

**Best pick: TwitterAPI.io (~$6/mo)** - best balance of cost, reliability, and developer experience.
**Cheapest reliable: SociaVault (~$4/mo)** - simple pay-as-you-go.
**Free option: Xpoz.ai** - needs investigation on whether REST API or MCP-only.

---

## Free/Open-Source Scraping Tools

| Tool | Status (2026) | Works? | Risk |
|------|--------------|--------|------|
| **twikit** (d60/twikit) | Actively maintained (v2.3.3) | Yes | Account bans, ToS violation |
| **twscrape** (vladkens/twscrape) | Actively maintained (March 2026) | Yes | Account bans, ToS violation |
| **Playwright automation** | Works | Yes (most effort) | Account bans, detection |
| **XRSS** | Exists but fragile | Uncertain | X blocks scrapers every 2-4 weeks |
| **Nitter** | Resumed Feb 2025 | Partially | Requires sacrificial accounts |
| **snscrape** | Poorly maintained | Intermittent | Unreliable |
| **twint** | **Dead** | No | Do not use |
| **RSS Bridge** | Requires paid API key | N/A | Not free |

**Risks of all free scraping:**
- X's ToS: accessing >1M posts/24hrs via automation = $15,000 liquidated damages
- Account bans from IP tracking, CAPTCHAs, behavioral analysis
- X updates defenses every 2-4 weeks, breaking scrapers regularly
- Not suitable for reliable production use

---

## Twitter MCP Servers

| Server | Data Access Method | Cost | Tools | Verdict |
|--------|-------------------|------|-------|---------|
| **crazyrabbitLTC/mcp-twitter-server** | Official API + SocialData.tools | API key + ~$0.20/1K tweets | 53 tools | **Most feature-rich** |
| **lord-dubious/x-mcp** | Twikit (scraping) | Free (just account creds) | Comprehensive | Free but risky |
| **EnesCinr/twitter-mcp** | Official API v2 | Paid API key needed | 2 tools only | Too minimal |
| **Dishant27/twitter-mcp** | Official API v2 | Paid API key needed | CRUD ops | Requires paid API |
| **Barresider/x-mcp** | Playwright (browser) | Free | Timeline + search | Very fragile |

All of these MCP servers can be plugged directly into the Claude Agent SDK as tool providers.

---

## Recommendation

**For Phase 0 (laptop prototype):** Use **TwitterAPI.io** at ~$6/mo. It's reliable (99.99% uptime), cheap, needs no official Twitter API key, and is a drop-in REST API replacement. Write a simple Python script to fetch tweets from CC team accounts, then pass them to Claude Agent SDK for signal extraction.

**Alternative:** Start with **Xpoz.ai free tier** if it supports REST API calls (not just MCP). If it does, that's $0/mo.

**Avoid:** Free scraping tools for production - they're fragile, risky, and require ongoing maintenance. The $4-6/mo for a third-party API is worth the reliability.
