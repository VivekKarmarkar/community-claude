# community-claude

A systematic investigation into building a platform to solve specific personal problems that fall under the category of community problems and may naturally extend to benefit the broader Claude Code community.

## Problems

1. **Twitter/X Signal Extraction** — The Claude Code team tweets non-stop, retweets each other, and noise drowns signal. Extracting useful technical nuggets requires wading through sensory overload.
2. **Jobs Board** — No Claude Code jobs board exists. Julia and Biomch-L have them. The CC community should too.
3. **Issues, Fixes & Hacks** — A place to share what broke and what worked, with MCP integration so Claude Code can search it directly.
4. **Gallery** — A tile-icon gallery for sharing creations. Solves isolation and sparks inspiration.

## Technical Vision

- **Discourse** as the community backbone (official MCP server, proven model via Julia's 24K-user community)
- **Claude Agent SDK** powering a standalone scraper app for Twitter/X signal extraction
- **Discourse MCP server** enabling Claude Code to plug directly into the platform

## Research

| File | Contents |
|------|----------|
| `problem_statement.md` | The four problems defined |
| `vision.md` | Platform vision and phases |
| `phases.md` | Phase 0 through Phase 3 |
| `existing_approaches.md` | Research on Julia, Biomch-L, Discourse, MCP servers, alternative platforms |
| `hosting.md` | Hosting options for the scraper app |
| `twitter_economics.md` | Twitter/X data access pricing and options |
| `setup.md` | Phase 0 local setup (Python venv, Claude Agent SDK) |
| `conclusions.md` | Where we landed and what to bring to office hours |
| `references/` | Articles and papers on the Twitter API ecosystem destruction |

## Status

**Paused.** The Twitter/X API is priced out of reach for indie developers ($200/mo minimum to read other users' tweets), and every workaround is fragile. The Discourse community platform would need the Claude Code team's support for distribution and marketing. Taking this to office hours for discussion.
