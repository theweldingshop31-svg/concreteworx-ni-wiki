---
tags: [project, todo]
---

# Outstanding Work — Prioritised

← [[Home]] · [[Project Status Overview]]

## Immediate (blocks going live)
- [ ] **Diagnose and fix product/category page indexation** — verified via live Search Console data that Google has not indexed any product or category page (0/58 submitted sitemap URLs indexed); only the homepage and `/shop/` are indexed. This blocks the entire product-page-driven SEO strategy from working at all. Internal linking has been ruled out as the cause (verified via raw HTML inspection — see [[SEO Audit Findings]]); leading hypothesis is now crawl backlog / low domain authority. 3 sample product URLs (Roman Bench, Wood Stump Planter, Elephant Bench) manually submitted via Search Console "Request Indexing" — **result not yet verified**, check with `inspect_url` in a few days.
- [ ] **Fix Indexing API permissions** — `cwni_gsc_submit_batch` failed twice with "Permission denied. Failed to verify the URL ownership." Needs the OAuth-authenticated Google account to hold Owner role on the `https://concreteworxni.com/` Search Console property and the Indexing API enabled in the correct GCP project; a first fix attempt did not resolve it. See [[CWNI-GSC-MCP]] and [[SEO Audit Findings]].
- [ ] Minor: homepage has duplicate `http://`/`https://` versions of the same category links — dedupe to `https://` only for link-equity hygiene.
- [ ] Recover or regenerate the completed SEO product catalogue (titles, keywords, descriptions, meta, permalinks) and save it into this project so it's the working source of truth. See [[Catalogue Data Status]].
- [ ] Backfill missing SKUs (73 products) — needed for WooCommerce import and inventory tracking.
- [ ] Backfill missing prices (54 products).
- [ ] Run the WooCommerce native CSV import for the base 121 products.

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
