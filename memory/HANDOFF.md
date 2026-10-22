# Session Handoff

> Bridge between Claude Code sessions. Updated at the end of every session.
> The SessionStart hook auto-injects this into context.

## Last Updated

- **Date:** 2026-10-22
- **Branch:** cursor/node-22-security-pin-ab1d
- **Version:** v1.0.0
- **Focus:** Pin Node.js to 22.23.4 after the 21 Oct 2026 security releases.

## Accomplished

### This Session (2026-10-22)
- Pinned the runtime off unpatched Node 20: `.nvmrc` is `22.23.4`, `package.json` `engines.node` is `>=22.23.4 <23`, `@types/node` is `^22` (lockfile `22.20.5`)
- No GitHub Actions or other CI `setup-node` step exists, so nothing there to pin
- Verified on Node v22.23.4: `pnpm install`, `pnpm lint`, `pnpm exec tsc --noEmit`, and `pnpm build` all passed
- Vercel only offers major Node versions and `engines` overrides the dashboard. Set Project Settings → Build and Deployment → Node.js Version to **22.x**, then redeploy. An engines range without `<23` would deploy 24.x

### Previous session (2026-02-28 → 2026-03-01)
- Completed slug URL migration: RSS feed, category pages now use article.slug
- Security headers in next.config.ts: HSTS, X-Frame-Options, X-Content-Type-Options, Referrer-Policy, Permissions-Policy
- 301 redirects: /?category= → /category/, www → apex domain
- Expanded LLM summary prompt: 4-6 sentences (was 2-3), max_tokens 1024→2048
- About page JSON-LD (AboutPage + Organization schema)
- Explicit twitter:images on article detail pages
- Shared `<Footer />` component replacing 6 duplicated footers, with version badge
- Version system: NEXT_PUBLIC_APP_VERSION injected at build time, CHANGELOG.md, git tags v0.1.0/v1.0.0
- Version scripts: `pnpm version:patch`, `version:minor`, `version:major`
- Fixed LLM_PROVIDER env var bug: trailing newline causing "Unknown provider" — added .trim()
- Fixed git remote: switched from HallyAus/AI-News to HallyAus/AIMarketWire (Vercel-connected repo)
- Vercel now auto-deploys from GitHub pushes
- Ran 2 ingestion batches: 17 new articles published

### Previous Sessions
- Full SEO audit/fix, OG images, JSON-LD, RSS, sitemap, robots.txt (2026-02-28)
- Built polished frontend, deployed to Vercel, domain connected (2026-02-27)
- Backend pipeline: RSS ingestion, AI scoring, summaries, API routes (2026-02-25)

## In Progress

_None._

## Blocked

_None._

## Next Steps

1. In the Vercel project (danieljhall-mecoms-projects/aimarketwire), set Node.js Version to 22.x and redeploy so production leaves Node 20. Confirm the build log reports Node >= 22.23.4 (Vercel rolls the 22.x patch itself)
2. Run more ingestion batches — ~97 unprocessed articles remain in backlog
3. Upgrade to Vercel Pro for hourly cron (currently daily)
4. Delete `LLM_PROVIDER` env var from Vercel dashboard (defaults to "claude", avoids newline bug)
5. Set up monitoring/alerting for ingestion failures
6. Tune relevance threshold after more data (currently 40)
7. Add search functionality
8. GitHub release notes for v1.0.0
9. Consider Proxmox worker for more frequent ingestion
10. Also push to HallyAus/AI-News repo to keep it in sync (or archive it)

## Active Beads Issues

_Beads not yet initialised._

## Context

- **Node.js:** 22.23.4 (`.nvmrc`). `engines.node` is `>=22.23.4 <23`. Node 20 has no fix for the 21 Oct 2026 high-severity releases (including Brotli RCE CVE-2026-111497).
- **Version:** v1.0.0 (tagged, pushed)
- **Git remote:** HallyAus/AIMarketWire (Vercel auto-deploys from this)
- **Old remote:** HallyAus/AI-News (still has older commits, not connected to Vercel)
- Neon project: aimarketwire in ap-southeast-2, org-calm-flower-05958305
- Vercel project: danieljhall-mecoms-projects/aimarketwire
- Domain: aimarketwire.ai (SSL provisioned)
- Cron: daily at midnight UTC (Hobby plan limit)
- Scorer processes 20 articles per batch
- Version workflow: `pnpm version:patch` → bumps package.json, commits, tags, pushes → Vercel deploys
- Footer component: `src/components/Footer.tsx` — used by all 6 page files
- Build-time version injection: `next.config.ts` reads package.json → `NEXT_PUBLIC_APP_VERSION`
- LLM_PROVIDER env var in Vercel has trailing newline — code trims it, but should delete the env var

## Files Modified (This Session)

```
.nvmrc (new) — 22.23.4
package.json — engines >=22.23.4 <23, @types/node ^22
pnpm-lock.yaml — @types/node 22.20.5
CLAUDE.md — runtime line
specs/decisions.md — ADR-007
strategy/learnings.md — Vercel major-only Node versions
.claude/rules/memory-decisions.md
.claude/rules/memory-sessions.md
memory/HANDOFF.md
```

### Previous session files

```
next.config.ts — security headers, redirects, version env var injection
package.json — version scripts, bumped to 1.0.0
CHANGELOG.md (new) — release history
src/components/Footer.tsx (new) — shared footer with version badge
src/app/page.tsx — replaced inline footer with <Footer />
src/app/articles/[id]/page.tsx — added twitter:images, replaced footer
src/app/category/[slug]/page.tsx — slug in Article interface, slug links, replaced footer
src/app/about/page.tsx — added JSON-LD, replaced footer
src/app/privacy/page.tsx — replaced footer
src/app/terms/page.tsx — replaced footer
src/app/feed.xml/route.ts — RSS links use slug instead of id
src/lib/llm/claude.ts — expanded summary prompt (4-6 sentences, 2048 tokens)
src/lib/llm/index.ts — trim() on LLM_PROVIDER to handle trailing newline
.claude/rules/memory-decisions.md — 4 new decisions
.claude/rules/memory-sessions.md — session entry
memory/HANDOFF.md — updated
```
