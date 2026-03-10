# Project Roadmap: community-claude

> **Created:** 2026-03-10
> **Status:** Draft
> **Owner:** Vivek Karmarkar

## Vision
A platform to solve specific personal problems (issues/fixes/hacks, jobs board, gallery, Twitter signal extraction) that fall under community-type problems and may naturally extend to the Claude Code community.

## Current State
- Systematic research completed on platforms, MCP servers, hosting, Twitter API economics
- **Twitter/X scraper blocked** by API costs ($200/mo minimum, all workarounds fragile)
- Discourse identified as the right platform (official MCP server, proven model via Julia)
- Claude Agent SDK installed and ready in local venv
- Docker, Node.js, npm all available on laptop
- Office hours meeting with Claude Code team upcoming

---

## Phase 1: Discourse + MCP Experiment — Prove It Works
**Goal:** Stand up a local Discourse instance, populate it with real issues/bugs/fixes, and verify Claude Code can plug in via MCP to search and find solutions.
**Status:** Not Started

| Priority | Task | Description | Dependencies |
|----------|------|-------------|-------------|
| P0 | Run Discourse locally | Set up Discourse in Docker (developer mode) on laptop | Docker installed |
| P0 | Create categories | Set up Issues, Bugs, Fixes/Hacks categories | Discourse running |
| P0 | Seed content | Post real Claude Code bugs, issues, and fixes as test data | Categories created |
| P1 | Generate API key | Create an admin API key in Discourse for MCP access | Discourse running |
| P1 | Install Discourse MCP server | Run `npx @discourse/mcp@latest` pointed at local instance | API key ready |
| P1 | Add to Claude Code config | Configure `.mcp.json` so Claude Code can use the Discourse MCP | MCP server running |
| P0 | Test the loop | Ask Claude Code to search for a fix to a specific bug via MCP and verify it finds the right answer | Everything above |

**Exit criteria:**
- [ ] Discourse running locally with seeded content
- [ ] Claude Code can search Discourse via MCP and return relevant fixes
- [ ] The experience is useful — searching the community actually helps solve problems

---

## Phase 2: Office Hours — Get Feedback & Support
**Goal:** Present the project and findings to the Claude Code team. Ask for help with distribution, Twitter access, and permissions.
**Status:** Not Started

| Priority | Task | Description | Dependencies |
|----------|------|-------------|-------------|
| P0 | Prepare demo | Have Phase 1 working as a live demo showing Claude Code plugging into Discourse | Phase 1 complete |
| P0 | Present problems | Walk through the four problems and the research | — |
| P1 | Ask about Twitter/X | Can the CC team help with data access? A feed, partnership, or official channel? | — |
| P1 | Ask about distribution | Would the CC team endorse/promote a community Discourse? | — |
| P1 | Ask about permissions | Any permissions needed to build on/for the CC ecosystem? | — |

**Exit criteria:**
- [ ] CC team has seen the demo and research
- [ ] Clear answer on whether they'd support distribution
- [ ] Direction on Twitter/X data access (help or not)

---

## Phase 3: Deploy & Populate — If Green-Lit
**Goal:** Host Discourse publicly, set up all categories, and start building real community content.
**Status:** Not Started

| Priority | Task | Description | Dependencies |
|----------|------|-------------|-------------|
| P0 | Host Discourse | Deploy to managed hosting ($20/mo Starter) or self-host | CC team green light |
| P0 | Set up all categories | Issues/Fixes/Hacks, Jobs Board, Gallery | Discourse hosted |
| P1 | Configure MCP for production | Point Discourse MCP at production URL | Discourse hosted |
| P1 | Seed with real content | Post genuine issues, fixes, job listings | Categories ready |
| P2 | Gallery theme | Customize Discourse theme for tile-icon gallery display | — |

**Exit criteria:**
- [ ] Public Discourse instance running with all categories
- [ ] Claude Code can plug into the production instance via MCP
- [ ] At least 10 real posts across categories

---

## Phase 4: Twitter/X Integration — If Unblocked
**Goal:** Solve the Twitter signal extraction problem, contingent on API access being resolved.
**Status:** Blocked

| Priority | Task | Description | Dependencies |
|----------|------|-------------|-------------|
| P0 | Resolve data access | Use whatever path emerges (CC team help, API partnership, or viable third-party) | Office hours outcome |
| P0 | Build scraper app | Claude Agent SDK app that fetches, deduplicates, extracts signal | Data access resolved |
| P1 | Connect to Discourse | Post curated Twitter content to Discourse via MCP | Scraper working + Discourse hosted |
| P2 | Schedule in cloud | Host scraper on Railway or similar, run on cron | Scraper working |

**Exit criteria:**
- [ ] Curated Claude Code team tweets appearing in Discourse automatically
- [ ] Signal-to-noise ratio is meaningfully better than raw Twitter

---

## Risks & Mitigations

| Risk | Impact | Likelihood | Mitigation |
|------|--------|-----------|-----------|
| Twitter/X API remains inaccessible | High | High | Focus on Discourse + MCP value; raise at office hours |
| CC team doesn't support distribution | High | Medium | Platform still useful personally; may find organic adoption |
| Discourse MCP integration doesn't work well in practice | Medium | Low | Official MCP server is production-ready; test in Phase 1 |
| Discourse maintenance burden too high | Medium | Low | Use managed hosting ($20/mo) to eliminate ops work |

## Open Questions
- Will the CC team support distribution of a community Discourse?
- Is there any path to Twitter/X data that doesn't cost $200/mo or break every 2 weeks?
- Should the Discourse be public from day one or start invite-only?
- Could this eventually become an official Anthropic community resource?

## Out of Scope
- Educational resources / content vetting (too messy without curation process)
- Building a custom platform from scratch (Discourse already exists and has MCP)
- Replacing Twitter/X as the CC team's posting platform
