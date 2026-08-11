---
tags: [project, tooling, mcp, seo]
---

# CWNI-GSC-MCP

← [[Home]] · [[SEO Audit Findings]]

> ⚠️ **Tool prefix: `mcp__cwni-gsc__*`.** Do not use `mcp__gsc__*` for this project — that connector is hardcoded to a different client's Search Console property (secretsense.co.za) and will return that property's data without error on most calls (only `inspect_url` rejects concreteworxni.com URLs outright). See `CLAUDE.md` at the repo root and `log.md` Session 6 (2026-08-11) for how this was discovered.

A local Google Search Console MCP server scoped to concreteworxni.com, built 2026-08-10. Lives in `cwni-gsc-mcp/` in this repo but is **not** committed/pushed (gitignored `.env`-equivalent secrets + kept local-only, same policy as [[WordPress MCP]] — see that page's rationale).

## Why it exists
A previously-connected shared `gsc` MCP connector turned out to be hardcoded to a different Search Console property (`secretsense.co.za`) with no way to repoint it — `inspect_url` rejected concreteworxni.com outright. This server is a local fork of the open-source [Suganthans-GSC-MCP](https://github.com/Suganthan-Mohanadasan/Suganthans-GSC-MCP) (Apache-2.0, attribution preserved in `cwni-gsc-mcp/LICENSE` + `NOTICE`), reconfigured and OAuth-authenticated specifically for this site.

## Configuration (verified working)
- Auth: OAuth (`GSC_AUTH_MODE=oauth`), using `oauth-client-secret.json` (an existing Desktop-app OAuth client reused from a prior setup — not freshly created for this project).
- Site: `GSC_SITE_URL=https://concreteworxni.com/` (URL-prefix property). The domain-property form (`sc-domain:concreteworxni.com`) returns "insufficient permission" for the authenticated account even though the URL-prefix property works — the account has access to one, not the other, in Search Console.
- Token cached at `~/.gsc-mcp/oauth-token.json`, refreshes silently.

## Tools
18 tools: `site_snapshot`, `inspect_url`, `list_sitemaps`, `submit_sitemap`, `submit_url`, `submit_batch`, `quick_wins`, `ctr_opportunities`, `ctr_vs_benchmark`, `traffic_drops`, `content_gaps`, `content_decay`, `content_recommendations`, `cannibalization_check`, `topic_cluster_performance`, `advanced_search_analytics`, `check_alerts`, `generate_report`, `multi_site_dashboard`, `verify_claim`.

## Status
Confirmed working end-to-end 2026-08-10 — `site_snapshot` and `inspect_url` both returned real, verified concreteworxni.com data (see [[SEO Audit Findings]]).

**Known gap (Session 5, 2026-08-10, still unresolved):** `submit_batch` (Google Indexing API) fails with `Permission denied. Failed to verify the URL ownership.` — tried twice (initial attempt + retry after a user permissions fix), same error both times. Since this connector uses OAuth (not a service account), the fix requires either enabling the Indexing API on the correct GCP project, or the OAuth-authenticated account holding **Owner** (not just full/restricted user) role on the `https://concreteworxni.com/` Search Console property — neither has been confirmed done. Read/reporting tools (`site_snapshot`, `inspect_url`, etc.) are unaffected and work fine; only the write path (`submit_batch`/`submit_url`/`submit_sitemap`) is suspect. See [[log]] Session 5 and [[Outstanding Work]].

## See also
- [[SEO Audit Findings]] — first real analysis run through this tool
- Full setup instructions: `cwni-gsc-mcp/README.md`
