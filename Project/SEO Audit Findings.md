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

**Likely causes, not yet verified — ranked by probability:**
1. No crawlable internal link path from indexed pages (homepage/shop) to product/category pages — sitemaps are a weak signal; Google prioritises internally-linked pages, especially on a low-authority site.
2. Site/sitemap still working through Google's crawl backlog — weakened by the fact the sitemap was submitted 2026-01-08, over 7 months ago.
3. JavaScript-rendered product links not visible to Googlebot's crawl of the homepage/shop.

**Unresolved — next diagnostic step:** fetch the raw (non-JS-rendered) HTML of the homepage and `/shop/` and check whether product/category URLs actually appear as `<a href>` links. This determines whether it's a crawl-discovery problem (fixable via internal linking) or something else. **Not yet done as of session close.**

## Other findings (site inspection only, see prior audit for full detail)

- Homepage title tag ~76 characters, will truncate in SERPs.
- Homepage schema typed `Article`/`Person` instead of `Organization`/`WebSite`.
- `/shop/`, About Us, Contact pages have boilerplate/generic meta descriptions.
- Homepage H2 typo: "Northen Irelands" → "Northern Ireland's."
- Cart/checkout/my-account included in sitemap despite being noindexed (low priority).
- Only 50/121 catalogued products are published (already tracked in [[Outstanding Work]] and [[Catalogue Data Status]] — same root gap, independently confirmed here via WP REST `X-WP-Total: 50`).

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
