---
tags: [project, todo]
---

# Outstanding Work — Prioritised

← [[Home]] · [[Project Status Overview]]

## Immediate (blocks going live)
- [ ] **Diagnose and fix product/category page indexation** — verified via live Search Console data that Google has not indexed any product or category page (0/58 submitted sitemap URLs indexed); only the homepage and `/shop/` are indexed. This blocks the entire product-page-driven SEO strategy from working at all. Internal linking has been ruled out as the cause (verified via raw HTML inspection — see [[SEO Audit Findings]]); leading hypothesis is now crawl backlog / low domain authority. 3 sample product URLs (Roman Bench, Wood Stump Planter, Elephant Bench) manually submitted via Search Console "Request Indexing" — **result not yet verified**, check with `inspect_url` in a few days.
- [ ] **Fix Indexing API permissions** — `cwni_gsc_submit_batch` failed twice with "Permission denied. Failed to verify the URL ownership." Needs the OAuth-authenticated Google account to hold Owner role on the `https://concreteworxni.com/` Search Console property and the Indexing API enabled in the correct GCP project; a first fix attempt did not resolve it. See [[CWNI-GSC-MCP]] and [[SEO Audit Findings]].
- [ ] Minor: homepage has duplicate `http://`/`https://` versions of the same category links — dedupe to `https://` only for link-equity hygiene.
- [ ] **Verify and reconcile `Concreteworx_NI_Product_Spreadsheet_latest`** (Drive id `1_2bZU0BMLLZvm3ZlNd-mNDYZIJmeWnLgNsPF0MRVjsE`) — likely the missing fully-SEO'd catalogue, found Session 6 but only spot-checked on 2/121 rows. Read all rows to confirm genuine completeness, then remap its old-format SKUs to the new short-code scheme before treating it as source of truth. See [[Catalogue Data Status]].
- [x] ~~Backfill missing SKUs~~ — done Session 6: all 122 live WooCommerce products and the working sheet now use a new short-code scheme (`PLT-001`, `BEN-002`, etc.). **Not fully closed out**, see below.
- [ ] **Resolve the live "Donkey" duplicate** — two separate WooCommerce products both named "Donkey" (id 960 = `LGE-006`, id 1019 = `LGE-015`). The working sheet was manually edited to show only one; the live site still has both. Decide whether this is a true duplicate (merge/delete one) or a distinct variant that needs a clearer name, then align sheet and site.
- [ ] **Rename the new working sheet** (id `1VeMS3LVNqNtZqYKrrd9YH6g_8XGHppU3PUUIPdUYQ9c`) from "Concreteworx NI Product Spreadsheet — New SKUs (2026-08-11)" to the original sheet's name — requires manual action in the Sheets UI, no Drive rename tool available in this session.
- [ ] **Spot-check the remaining 121 of 122 live SKU writes** — only `id 937` was individually re-fetched to confirm the new SKU actually persisted; the other 121 were only confirmed via batch-response item counts, not per-item field verification.
- [ ] Backfill missing prices (54 products).
- [ ] Run the WooCommerce native CSV import for the base 121 products (note: may now be moot if products already exist live and only need field updates rather than import).

## Near-term
- [ ] Source/upload product photography and populate the 5-image URL + alt-tag fields per product (currently 0/121).
- [ ] Add featured category images for **Garden Benches** and **Vehicle Garden Ornaments** (only 2 categories missing — see [[Category Structure]]).
- [ ] Backfill dimensions/weight where available (currently only 8/121) — useful for shipping and for "what size will this be" search intent.

## Post-launch
- [ ] Layer Rank Math SEO meta titles/descriptions/focus keywords onto live products.
- [ ] Build out Gallery / social-proof section (TikTok integration) per the homepage outline — see [[Site Structure]].
- [ ] Consider phased content push by category, prioritising Animal Garden Ornaments (largest) and Football Club Memorabilia (strong brand-search potential) first.

## See also
- [[SEO Strategy]]
- [[Technical Learnings]]
- [[SEO Audit Findings]]
