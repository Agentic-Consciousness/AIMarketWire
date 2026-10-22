# Memory: Decisions

> Past choices made during this project for consistency. Dated entries.
> Claude adds here when a decision is made. Auto-loaded every session.

## Format

Each entry: `[YYYY-MM-DD] Decision — Rationale`

## Decisions

<!-- Claude: add new entries at the top -->

- [2026-10-22] Pin Node.js to 22.23.4 (`>=22.23.4 <23`) — Oct 21 2026 security releases fix high CVEs including Brotli RCE CVE-2026-111497 on 22/24/26 only; Node 20 is unpatched. Vercel setting must be 22.x and needs a redeploy.
- [2026-02-28] Semver + git tags for versioning — npm version patch/minor/major scripts, NEXT_PUBLIC_APP_VERSION injected at build time, version badge in shared Footer
- [2026-02-28] Shared Footer component — extracted from 6 duplicated footers into src/components/Footer.tsx with activePath and maxWidth props
- [2026-02-28] Slug URLs over UUIDs — SEO-friendly, generateUniqueSlug(title, id) appends 8-char UUID suffix for uniqueness
- [2026-02-28] Homepage ISR (60s) instead of force-dynamic — better performance, API data cached and revalidated
- [2026-02-27] Domain aimarketwire.ai — registered and connected to Vercel
- [2026-02-27] Vercel Hobby plan — daily cron (0 0 * * *) for ingestion, hourly requires Pro
- [2026-02-27] Neon free tier in ap-southeast-2 (Sydney) — low latency for Australian users
- [2026-02-27] claude-sonnet-4-6 for scoring/summarisation — updated from claude-sonnet-4-20250514
- [2026-02-27] Force-dynamic homepage — page fetches from API at runtime, not statically generated
- [2026-02-25] 7 RSS sources for launch — Bloomberg Tech, TechCrunch AI, AI Business, The Decoder, MIT Tech Review, The Verge AI, VentureBeat AI. Reuters dropped (no free RSS since 2020)
- [2026-02-25] Lazy DB connection via Proxy — avoids build-time errors when DATABASE_URL not set
- [2026-02-25] Next.js 16 instead of 15 — latest stable at scaffold time, same App Router architecture, React 19 support
- [2026-02-25] Vitest over Jest for testing — faster, native ESM, better TypeScript support
- [2026-02-25] Relevance threshold at 40/100 — will tune after Week 2 data, targeting <5% false positive rate
- [2026-02-25] Five AI categories at launch (Infrastructure, Regulation, Applications, Chips, Models) — expandable later
- [2026-02-25] Inngest first, BullMQ fallback for background jobs — evaluate during Week 1 implementation
- [2026-02-25] Drizzle ORM over Prisma — lighter weight, better edge runtime compatibility, no binary engine
- [2026-02-25] Neon serverless Postgres — native Vercel integration, connection pooling, generous free tier
- [2026-02-25] Next.js App Router on Vercel with pnpm — SSR/ISR for <200ms page loads
