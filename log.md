---
tags: [log, provenance]
---

# Session Log

← [[Home]]

Chronological record of work done on this vault/project. Each entry: what changed, what sources were used, what's verified vs. inferred, what's still open.

---

## 2026-08-10 — Session 1: Wiki creation

**Work:** Built the initial Obsidian vault from two source documents.

**Sources ingested:**
- `Files to ingest/Concrete_Worx_NI_Brand_CI.docx` → [[Brand Overview]], [[Brand Voice]], [[Visual Identity]]
- `Files to ingest/Concrete_Worx_NI_Project_Status_Reference.docx` (compiled 2026-08-10 from project files) → [[Project Status Overview]], [[Category Structure]], [[Catalogue Data Status]], [[SEO Strategy]], [[Technical Learnings]], [[Outstanding Work]], [[Site Structure]]

**Verification state:** Direct transcription from source docs — not independently verified against the live site at this point.

**Decisions:**
- Created `concreteworx-ni-wiki` as a new public GitHub repo (`theweldingshop31-svg/concreteworx-ni-wiki`) rather than using an existing repo's GitHub Wiki feature, per user request.

**Repo:** initialized, committed, pushed. Commit `79ca752`.

---

## 2026-08-10 — Session 2: WordPress MCP

**Work:** Built `mcp-server/` — a local MCP server for full read/write WordPress access to concreteworxni.com, plus a companion mu-plugin (`concreteworxni-mcp-theme-bridge.php`) for theme file editing (not natively supported by WP REST API).

**Decisions:**
- Kept `mcp-server/` untracked/local-only, not pushed to the public wiki repo — user's explicit choice, to avoid publicly associating admin-level site tooling with a public repo.
- Application Password + theme-bridge shared secret generated and placed only in local `.env` / `wp-config.php`, never in chat.

**Verification state:** Confirmed working end-to-end — authenticated as WP user NevWally31; theme bridge tested live (list/read confirmed against active theme `blocksy-child`; write/delete not separately tested).

**Wiki page:** [[WordPress MCP]] (written retroactively in Session 5 close-out — see below).

---

## 2026-08-10 — Session 3: ui-ux-pro-max skill + design system

**Work:** Installed the `ui-ux-pro-max` Claude Code plugin (marketplace: `nextlevelbuilder/ui-ux-pro-max-skill`), tested it, then generated and persisted a UI design system for the project.

**Decisions:**
- The tool's auto-picked color palette and typography did not match locked brand CI — manually overrode `design-system/concreteworx-ni/MASTER.md` colors/typography/component CSS to use the actual brand values from [[Visual Identity]], while keeping the tool's useful output (style direction "Nature Distilled," spacing/shadow scale, a11y checklist).

**Verification state:** Design system is a synthesis/judgment call (mine), not a source-verified fact — flagged as such in the file itself.

**Repo:** committed and pushed (design tokens only, no secrets). Commit `6b629c4`.

---

## 2026-08-10 — Session 4: SEO audit + CWNI-GSC-MCP

**Work:** Ran a live SEO audit of concreteworxni.com using the `seo-audit` skill, direct site inspection (`curl`/`WebFetch` — robots.txt, sitemaps, HTML, schema), and WordPress REST API cross-checks.

**Finding:** the pre-existing `gsc` MCP connector was hardcoded to a different Search Console property (`secretsense.co.za`) and could not be repointed — confirmed via `inspect_url` rejecting concreteworxni.com outright, and `list_sitemaps` returning the wrong site's data.

**Decision:** built `cwni-gsc-mcp/` as a local fork of the open-source [Suganthans-GSC-MCP](https://github.com/Suganthan-Mohanadasan/Suganthans-GSC-MCP) (Apache-2.0; attribution preserved in `cwni-gsc-mcp/LICENSE`/`NOTICE`), reusing an OAuth client already downloaded in `Files to ingest/Suganthans-GSC-MCP/` rather than creating a fresh one. Kept local-only, same policy as the WordPress MCP.

**Configuration finding:** `GSC_SITE_URL=sc-domain:concreteworxni.com` (domain property) failed with "insufficient permission"; `https://concreteworxni.com/` (URL-prefix property) works. The authenticated account has access to one but not the other in Search Console.

**Verification state:** Confirmed working end-to-end with real API data — `site_snapshot` and `inspect_url` both returned live concreteworxni.com results after reconnecting.

**Critical finding (verified via Search Console API, ground truth):** homepage and `/shop/` are indexed; every product and category page checked (5 sampled) is not indexed — most "unknown to Google" (never crawled), one "discovered, not indexed." Sitemap confirms 0/58 submitted URLs indexed. Full detail: [[SEO Audit Findings]].

**Unresolved as of session close:** root cause of the indexation gap is diagnosed only as far as three ranked hypotheses (no internal links from indexed pages / crawl backlog / JS-rendered links). The next diagnostic step — checking whether product/category URLs appear as `<a href>` in the raw HTML of the homepage/shop — was proposed but **not executed**. This is the single most important open item in the project.

**Wiki pages written this close-out:** [[SEO Audit Findings]], [[CWNI-GSC-MCP]], [[WordPress MCP]] (retroactive). [[Outstanding Work]] and [[Home]] updated to reflect the indexation finding as the top-priority item, superseding catalogue completeness as the primary blocker.

---

## Open questions carried forward

1. **Why aren't product/category pages indexed?** Diagnostic step not yet run (see Session 4). Top priority for next session.
2. Domain vs. URL-prefix property permission mismatch in Search Console — not investigated further; workaround (use URL-prefix) is in place and working, but the underlying permission gap on the domain property hasn't been explained or fixed.
3. `mobileUsability: VERDICT_UNSPECIFIED` on all `inspect_url` results — not a confirmed issue, just an unpopulated field; worth checking if this stays unspecified as more URLs are inspected, or if it's a quirk of the tool/API response for this account.
