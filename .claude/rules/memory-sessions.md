# Memory: Sessions

> Rolling summary of recent work. Claude adds entries after substantive work.
> Auto-loaded every session via `.claude/rules/`.
> Keep this to ~20 most recent entries. Archive older ones to `memory/sessions/`.

## Recent Sessions

<!-- Claude: add new entries at the top. Remove oldest when >20 entries. -->

- [2026-10-22] Node 22.23.4 security pin — `.nvmrc`, `engines` `>=22.23.4 <23`, `@types/node` ^22. No CI `setup-node` in the repo. Vercel Node.js Version must be 22.x and production needs a redeploy; Node 20 gets no Oct 21 2026 CVE fix.
- [2026-03-01] Versioning + deployment fix — shared Footer with v1.0.0 badge, version scripts (patch/minor/major), CHANGELOG.md, security headers, 301 redirects, expanded LLM prompt, fixed LLM_PROVIDER newline bug, switched git remote to AIMarketWire (Vercel-connected), ran 2 ingestion batches (17 new articles)
- [2026-02-28] SEO + slugs — full SEO audit/fix (canonical, OG images, JSON-LD, RSS, sitemap), slug URLs replacing UUIDs, article detail/category/about/privacy/terms/404 pages, git tags v0.1.0/v1.0.0
- [2026-02-27] Go live — deployed to Vercel + Neon, domain aimarketwire.ai, 11 real articles published, daily cron set up, fixed scorer SQL bug (sources import + wrong column reference), updated model to claude-sonnet-4-6, added JSON extraction for markdown-wrapped LLM responses
- [2026-02-25] Phase 1B/1C pipeline — RSS ingestion from 7 sources, scoring pipeline, summary generation, API routes (articles feed + detail with ticker/category filters), CLI ingest command, 11 tests passing
- [2026-02-25] Phase 1A scaffold — installed Node.js 24 + pnpm, scaffolded Next.js 16 with Tailwind/TypeScript, created Drizzle schema (7 tables), LLM abstraction layer with Claude provider, Docker Compose, env validation, pushed to GitHub
- [2026-02-25] AIMarketWire project setup — populated CLAUDE.md, created 30-day plan, logged 6 ADRs, built architecture overview, set up todo-list and HANDOFF.md
