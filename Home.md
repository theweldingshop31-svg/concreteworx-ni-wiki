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
- [[WordPress MCP]] — local admin-level WP access (content, theme files)
- [[CWNI-GSC-MCP]] — local Search Console access, scoped correctly to concreteworxni.com

## Status at a Glance
- 🔴 **Biggest gap:** product and category pages are not indexed by Google at all (0/58 sitemap URLs indexed, verified via Search Console) — see [[SEO Audit Findings]]. This blocks the entire product-page SEO strategy regardless of catalogue completeness. **Internal linking has been ruled out as the cause** (verified via raw HTML inspection 2026-08-10) — leading hypothesis is now crawl backlog/low domain authority. 3 sample product URLs manually submitted for indexing via Search Console; result not yet verified. Indexing API access is separately broken (permission error) and still needs fixing — see [[Outstanding Work]].
- 🔴 The fully SEO-optimised catalogue (titles/keywords/descriptions/meta) was built in a separate session and never re-uploaded — see [[Outstanding Work]].
- 🟡 SKUs missing on 73/121 products; prices missing on 54/121.
- 🟢 Category structure is finalised and locked (10 categories, all SEO fields complete).
- 🟢 Real organic traffic is growing (clicks +63.8% period-over-period per [[SEO Audit Findings]]) — but currently limited to homepage/shop, not products.

---
*Compiled from `Concrete_Worx_NI_Brand_CI.docx` and `Concrete_Worx_NI_Project_Status_Reference.docx` (source docs 10 Aug 2026). Log of session-by-session work: [[log]].*
