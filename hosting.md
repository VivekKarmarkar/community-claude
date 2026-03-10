# Hosting: Phase 1 - Twitter/X Scraper App

The app runs the Claude Agent SDK to scrape Twitter/X, process tweets (extract signal from noise), and output a file.

## Claude Agent SDK Requirements

- **RAM:** 1 GB
- **CPU:** 1 vCPU
- **Disk:** 5 GB
- **Software:** Node.js (CLI is bundled with the SDK)
- **Network:** Outbound HTTPS to api.anthropic.com
- **Key constraint:** The SDK spawns the CLI as a subprocess - platforms that block subprocess spawning (e.g., Cloudflare Workers) will NOT work

Heavy compute (LLM inference) happens on Anthropic's servers - the local process is lightweight.

## Options

### Serverless/Scheduled

| Platform | Monthly Cost | Max Execution Time | Notes |
|----------|-------------|-------------------|-------|
| **Railway (Hobby)** | **$5** (within free credit) | No limit | Cron jobs built in, recommended |
| **AWS Lambda + EventBridge** | **$0 (free tier)** | 15 min | Works but Anthropic discourages for Agent SDK |
| **Google Cloud Functions 2nd gen** | **~$0.10** | 60 min | Near-free, good timeout headroom |
| **Fly.io (Cron Manager)** | **~$5** | No limit | Good but more setup complexity |

### VPS (Always-On)

| Provider | RAM | vCPU | Monthly Cost |
|----------|-----|------|-------------|
| **Oracle Cloud** (Always Free ARM) | Up to 24 GB | Up to 4 OCPUs | **$0 (free forever)** |
| **Vultr** | 512 MB | 1 vCPU | **$2.50/mo** |
| **Hetzner** CAX11 | 2 GB | 2 vCPU | **~$4.50/mo** |
| **DigitalOcean** | 1 GB | 1 vCPU | **$6/mo** |

### Won't Work

- **Cloudflare Workers** - V8 isolates block subprocess spawning (hard blocker)
- **Azure Functions (Consumption)** - 5-10 min timeout too tight for 2-10 min jobs
