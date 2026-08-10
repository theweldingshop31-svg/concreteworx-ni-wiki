---
tags: [project, technical, woocommerce]
---

# Technical / Import Learnings

← [[Home]] · [[Project Status Overview]]

- **Make.com + JSON category/tag formatting** caused repeated import friction — abandoned in favour of plain text categories and comma-separated tags.
- **"Product Import Export for WooCommerce" plugin** didn't map custom meta (Rank Math) fields cleanly out of the box — required explicit `meta:` / `rank_math_` prefixed columns.
- **Native WooCommerce CSV importer** was ultimately recommended as the simplest, free, reliable path for the base 121 products — SEO meta to be layered in afterwards rather than blocking the initial import.
- **General principle adopted:** get products live first, then iterate SEO fields — rather than blocking launch on 100% SEO completeness.

## See also
- [[Outstanding Work]]
- [[Catalogue Data Status]]
