---
tags: [home, moc]
---

# Concrete Worx NI — Second Brain

Handcrafted concrete garden ornaments, Northern Ireland. This vault is the working knowledge base for brand identity and the WooCommerce SEO/catalogue project.

> **Quick facts:** WooCommerce (WordPress) + Rank Math SEO · 121 products / 10 categories · Ordering via WhatsApp/phone [07925740898](tel:07925740898) · Voice: "Grit & Grandeur"

## Map of Content

### Brand
- [[Brand Overview]] — positioning, mission, USP, persona
- [[Brand Voice]] — "Grit & Grandeur" voice pillars & application by product type
- [[Visual Identity]] — colour palette & typography

### Project
- [[Project Status Overview]] — snapshot, what's live, what's outstanding
- [[Category Structure]] — the locked 10-category catalogue structure
- [[Catalogue Data Status]] — field-by-field completeness of the 121-product spreadsheet
- [[SEO Strategy]] — keyword strategy, title formats, description approach
- [[Technical Learnings]] — import/tooling lessons learned
- [[Outstanding Work]] — prioritised punch list
- [[Site Structure]] — nav, homepage layout, brand touchpoints
- [[SEO Audit Findings]] — live audit of concreteworxni.com, incl. verified indexation gap
- [design-system/concreteworx-ni/MASTER.md](design-system/concreteworx-ni/MASTER.md) — persisted UI design system (colors, typography, component specs) built with `ui-ux-pro-max`, overridden to match locked brand CI

### Tooling
> ⚠️ **See `CLAUDE.md` at the repo root before using any WordPress or Search Console MCP tool in this project.** Two similarly-named connectors are registered on this machine that point at *other clients'* sites and will return their data silently, with no error — this cost a full session on 2026-08-11 before being caught.
- [[WordPress MCP]] — local admin-level WP access (content, theme files). Use `mcp__concreteworxni-wp__*` — **not** `mcp__wordpress-mcp__*` (that one is horseaddict.co.za).
- [[CWNI-GSC-MCP]] — local Search Console access, scoped correctly to concreteworxni.com. Use `mcp__cwni-gsc__*` — **not** `mcp__gsc__*` (that one is secretsense.co.za).

## Status at a Glance
- 🔴 **Biggest gap:** product and category pages are not indexed by Google at all (0/58 sitemap URLs indexed, verified via Search Console) — see [[SEO Audit Findings]]. This blocks the entire product-page SEO strategy regardless of catalogue completeness. **Internal linking has been ruled out as the cause** (verified via raw HTML inspection 2026-08-10) — leading hypothesis is now crawl backlog/low domain authority. 3 sample product URLs manually submitted for indexing via Search Console; result not yet verified. Indexing API access is separately broken (permission error) and still needs fixing — see [[Outstanding Work]].
- 🟡 **Likely-found but not yet confirmed:** a spreadsheet (`Concreteworx_NI_Product_Spreadsheet_latest`, Drive, created 2025-12-25) appears to be the fully SEO-optimised catalogue that's been listed as missing since Session 1 — titles, keywords, HTML descriptions, meta, permalinks. Only spot-checked on 2 of 121 rows so far, and it still uses the old long-format SKUs. Needs full verification and SKU reconciliation before it can be adopted as source of truth — see [[Catalogue Data Status]].
- 🟡 **SKUs replaced with a new short scheme (Session 6, 2026-08-11)** — category code + sequence number (e.g. `PLT-001`, `BEN-002`), written to all 122 live WooCommerce products and to a new working sheet. **Not fully reconciled**: a live duplicate ("Donkey" exists as two separate products, `LGE-006` and `LGE-015`) was collapsed to one row in the sheet but not resolved on the live site; the new sheet still needs renaming (Drive has no rename tool in this session, pending manual step); only 1 of 122 live SKU writes was individually spot-verified post-write. See [[log]] Session 6 for full detail.
- 🟢 Category structure is finalised and locked (10 categories, all SEO fields complete) — see [[Category Structure]]. Session 6's independent live-data classification (keyword/taxonomy-based, for SKU-coding purposes only) produced slightly different per-category counts (e.g. 122 live products found vs. 121 documented here) — not yet reconciled; likely reflects a draft/newer product added since [[Category Structure]] was last counted, not a structural disagreement.
- 🟢 Real organic traffic is growing (clicks +63.8% period-over-period per [[SEO Audit Findings]]) — but currently limited to homepage/shop, not products.
- 🟢 `concreteworxni-wp` (local WordPress MCP) is now confirmed connected and working end-to-end after a real bug fix (`.env` path resolution) — see [[WordPress MCP]] and [[log]] Session 6.

---
*Compiled from `Concrete_Worx_NI_Brand_CI.docx` and `Concrete_Worx_NI_Project_Status_Reference.docx` (source docs 10 Aug 2026). Log of session-by-session work: [[log]].*
