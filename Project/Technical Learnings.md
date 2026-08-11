---
tags: [project, technical, woocommerce]
---

# Technical / Import Learnings

← [[Home]] · [[Project Status Overview]]

- **Make.com + JSON category/tag formatting** caused repeated import friction — abandoned in favour of plain text categories and comma-separated tags.
- **"Product Import Export for WooCommerce" plugin** didn't map custom meta (Rank Math) fields cleanly out of the box — required explicit `meta:` / `rank_math_` prefixed columns.
- **Native WooCommerce CSV importer** was ultimately recommended as the simplest, free, reliable path for the base 121 products — SEO meta to be layered in afterwards rather than blocking the initial import.
- **General principle adopted:** get products live first, then iterate SEO fields — rather than blocking launch on 100% SEO completeness.
- **`wc/v3/products` fails with `per_page`/`status` query params (Session 7, 2026-08-11)** — via the `concreteworxni-wp` `wp_raw_request` escape hatch, adding `per_page` or `status` to the query consistently returned an opaque `fetch failed` with no further detail. Plain `{"page": "N"}` pagination (default page size 10) worked reliably and was used to pull the full 112-product catalogue across 13 calls instead. Not root-caused — could be a connector-side limitation, not necessarily WooCommerce/WordPress itself.
- **Large `wp_raw_request` responses get written to a cache file, and the format of that file isn't consistent** (Session 7) — most responses land as plain multi-line JSON text files, but some come back as an inline JSON-escaped single-line preview (`\"key\": \"value\"` instead of `"key": "value"`) saved under a different filename pattern. A parsing script written against one format silently under-matched the other — worth normalizing/unescaping first, or checking file structure, before writing extraction regex/awk against cached tool output.

## See also
- [[Outstanding Work]]
- [[Catalogue Data Status]]
