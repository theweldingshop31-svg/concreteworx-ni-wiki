---
tags: [project, seo, audit, findings]
---

# SEO Audit Findings — concreteworxni.com

← [[Home]] · [[Project Status Overview]] · [[SEO Strategy]]

**Audit date:** 2026-08-10. **Method:** live site inspection (robots.txt, sitemaps, HTML, schema via `curl`/`WebFetch`) plus, once GSC access was connected, real Search Console data via [[CWNI-GSC-MCP]].

**Verification state:** Technical/on-page findings below are directly verified against the live site. Indexation findings are directly verified against the Search Console API (ground truth, not inferred). Root-cause diagnosis for the indexation gap is **not yet verified** — flagged explicitly below.

## Critical: Product & category pages are not indexed by Google

**Verified via `gsc_inspect_url` (Search Console API, ground truth):**

| URL | Status |
|---|---|
| Homepage `/` | ✅ Indexed, healthy |
| `/shop/` | ✅ Indexed, healthy |
| `/product-category/garden-benches/` | ❌ "URL is unknown to Google" |
| Roman Bench (product) | ❌ "URL is unknown to Google" |
| Wood Stump Planter (product) | ❌ "URL is unknown to Google" |
| Elephant Bench (product) | ❌ "URL is unknown to Google" |
| Donkey and Cart (product) | ❌ "Discovered — currently not indexed" |

Cross-confirmed by `gsc_list_sitemaps`: the submitted sitemap (`https://concreteworxni.com/sitemap.xml`, last downloaded by Google 2026-08-09) shows **58 web + 86 image URLs submitted, 0 indexed**.

**Impact:** the 208 clicks / 2,533 impressions measured in the last 28 days ([[Project Status Overview]] traffic figures) are almost certainly landing entirely on the homepage/shop/services pages. **None of the 50 live products are earning any organic visibility.** This is a larger lever than any on-page copy fix below — fixing it is a prerequisite for the SEO strategy in [[SEO Strategy]] to work at all, since that strategy is entirely product-page-driven (three-tier keyword targeting per product).

**Root cause — verified 2026-08-10 (later same session):** fetched raw HTML of homepage, all 4 paginated `/shop/` pages, and a sample product page as Googlebot (`curl -A Googlebot`, no JS execution).

- ✅ Homepage: real `<a href>` links (not JS-injected) to 6 category pages + 5 products, no `nofollow`.
- ✅ `/shop/`: 16 products/page × 4 pages (`rel="next"` chain intact) — covers all ~50 live products, plus 8 category links.
- ✅ Sample product page: `robots: index, follow`, correct self-referencing canonical, no `noindex`.
- ✅ `robots.txt`: no disallow on `/product/` or `/product-category/`.

**Internal linking is not the problem — hypothesis #1 (no crawlable link path) is disproven.** Product/category URLs are fully reachable and followable from indexed pages in plain HTML.

Remaining live hypotheses, ranked:
1. **Crawl backlog / low domain authority** — sitemap submitted 2026-01-08 (7+ months ago), still 0/58 indexed despite good internal linking. Plausible for a low-authority new domain; Google can sit on "Discovered — currently not indexed" a long time regardless of link structure.
2. Minor hygiene issue spotted in passing: homepage has both `http://` and `https://` versions of the same category links (e.g. `garden-benches` appears twice, once on each protocol) — splits link equity slightly, worth fixing but not a blocker.

**Next diagnostic step:** use `gsc_inspect_url`/Search Console "Request Indexing" on 2-3 product URLs and watch whether they get crawled within days — if they do, it's pure backlog; if Google keeps skipping them, look harder at authority/quality signals.

## Other findings (site inspection only, see prior audit for full detail)

- Homepage title tag ~76 characters, will truncate in SERPs.
- Homepage schema typed `Article`/`Person` instead of `Organization`/`WebSite`.
- `/shop/`, About Us, Contact pages have boilerplate/generic meta descriptions.
- Homepage H2 typo: "Northen Irelands" → "Northern Ireland's."
- Cart/checkout/my-account included in sitemap despite being noindexed (low priority).
- Only 50/121 catalogued products are published (already tracked in [[Outstanding Work]] and [[Catalogue Data Status]] — same root gap, independently confirmed here via WP REST `X-WP-Total: 50`).
  - **Update 2026-08-11 (Session 7):** a full `wc/v3/products` pull (done for pricing reconciliation, not indexation — see [[log]] Session 7) found **46 published / 66 draft, 112 total** — 4 fewer published than the 50 counted here on 2026-08-10. Cause not investigated (could be products unpublished since, a counting-method difference, or products deleted/added) — flagged as a discrepancy, not yet explained.

## Traffic snapshot (real GSC data, last 28 days vs. prior 28)

| Metric | Current | Prior | Change |
|---|---|---|---|
| Clicks | 208 | 127 | +81 (+63.8%) |
| Impressions | 2,533 | 2,242 | +291 (+13.0%) |
| CTR | 8.21% | 5.66% | +2.55pp |
| Avg. position | 9.4 | 10.3 | improved 0.9 |

Real growth on all metrics — but per the indexation finding above, this traffic is coming from a handful of indexed pages, not the product catalogue.

## See also
- [[Outstanding Work]] — action items derived from this audit
- [[CWNI-GSC-MCP]] — tool used to gather the Search Console data above
- [[SEO Strategy]]
