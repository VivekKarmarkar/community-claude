# Vision

A platform whose primary goal is solving specific problems I personally face. These problems, by my assessment, fall under what I'd categorize as community problems, which means they may naturally extend to benefit the broader Claude Code community. But that's secondary - the driver is my own needs.

## Problems to Solve

1. **Twitter/X Signal Extraction** - The Claude Code team ships and tweets non-stop. The entire team retweets each other, random people respond with emojis and noise. Extracting signal from noise means wading through Twitter/X - sensory overload, duplicates, reposts, low-value comments - to find the actually useful technical nuggets needed for doing Claude Code properly.

2. **Jobs Board** - Startups and companies (including Anthropic) are heavily using Claude Code. A dedicated jobs board, similar to Julia's on Discourse and Biomch-L's, solves a personal need for finding relevant opportunities and may be valuable to others.

3. **Issues, Fixes & Hacks** - A place to discuss things that broke and share workarounds that actually worked. The key twist: the platform should have MCP integration so Claude Code can directly plug in and search for solutions on the user's behalf.

4. **Gallery** - A tile-icon gallery where people share what they've built with Claude Code. Solves isolation and provides inspiration.

## Technical Vision

**Discourse** as the community backbone - it has an official, production-ready MCP server (`@discourse/mcp`), a proven model (Julia runs a jobs board as a Discourse category at 24K users), a comprehensive API, and is self-hostable and extensible.

A **standalone scraper application** powered by the **Claude Agent SDK** fetches tweets from Claude Code team members, uses Claude to extract signal from noise, deduplicates, and eventually posts curated content to Discourse via the Discourse MCP server. The MCP server is just an HTTP client - the scraper can run anywhere and point at the Discourse URL.

## Phases

- **Phase 0:** Build the Twitter/X scraper app using the Claude Agent SDK on laptop. Output curated content to a file.
- **Phase 1:** Phase 0 but on the cloud.
- **Phase 2:** Set up the Discourse server with categories for jobs, issues/fixes, and gallery.
- **Phase 3:** Connect the scraper app to Discourse via the Discourse MCP server so curated content posts automatically.
