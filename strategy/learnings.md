# Project Learnings

> Things discovered during development. Gotchas, workarounds, and non-obvious knowledge.
> Claude updates this when discoveries are made (see CLAUDE.md mandatory memory rules).

## Format

Each entry: `[YYYY-MM-DD] Learning — Context`

## Learnings

<!-- Claude: add new entries at the top -->

- [2026-10-22] Vercel Node.js versions are majors only — Settings → Build and Deployment → Node.js Version. `engines.node` overrides that setting. A range like `>=22.0.0` (no upper bound) deploys the latest 24.x; `>=22.23.4 <23` stays on 22.x. Vercel rolls the patch itself, so `.nvmrc` 22.23.4 does not pin the deployment patch. Changing the setting does not update live deployments until a redeploy. Node 20 was deprecated on Vercel on 1 Oct 2026 and got no fix in the 21 Oct 2026 security releases.
- [2026-03-01] Vercel env vars can have hidden newlines — LLM_PROVIDER was "claude\n" in dashboard even though it looked clean. Always .trim() env vars used for lookups, or better: delete unnecessary env vars that have code defaults.
- [2026-03-01] Vercel Git integration is repo-specific — pushing to HallyAus/AI-News didn't trigger deploys because Vercel was connected to HallyAus/AIMarketWire. Always verify `git remote -v` matches the Vercel-connected repo.
- [2026-03-01] generateStaticParams + API fetch = build timeout — category pages with generateStaticParams tried to fetch from localhost API during build, which isn't running. Use force-dynamic for pages that need runtime API data.
- [2026-03-01] npm version major auto-creates commit + tag — `npm version patch/minor/major` bumps package.json, creates a git commit, and creates a `vX.Y.Z` tag in one command. Clean working tree required.
- [2026-02-27] Next.js sitemap with force-dynamic — sitemap.ts fetching from API during static build times out. Must use `export const dynamic = "force-dynamic"` to generate at runtime.
- [2026-02-27] LLM JSON responses wrapped in markdown — Claude sometimes wraps JSON in ```json``` code blocks. extractJSON() regex handles this: `/```(?:json)?\s*([\s\S]*?)```/`
- [2026-02-27] Drizzle scorer bug — scorer was referencing `rawArticles.sourceId` but the join was on `sources.id`. Column name mismatch caused silent failures.
- [2026-02-27] Neon project ID vs endpoint ID — neonctl uses project ID (e.g., "withered-lake-76473178") not the endpoint ID (e.g., "ep-plain-cloud-a77h7kv9"). Run `neonctl projects list` to find it.
- [2026-02-25] Lazy DB connection via Proxy — Drizzle `drizzle(new Proxy(...))` avoids connection at import time, preventing build failures when DATABASE_URL isn't set.
