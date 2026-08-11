---
tags: [project, catalogue, data]
---

# Product Catalogue — Data Status

← [[Home]] · [[Project Status Overview]]

> **UPDATE 2026-08-11 (Session 6):** the sheet described below (`1ReLvmImVcPqcu8IMWW1aV8lvtRmrt4GRkSSjzOmE7JM`) has been **deleted**. Its SKU-updated replacement is `1VeMS3LVNqNtZqYKrrd9YH6g_8XGHppU3PUUIPdUYQ9c` ("Concreteworx NI Product Spreadsheet — New SKUs (2026-08-11)" — rename to the original title still pending, no Drive rename tool available this session). The completeness table below (SKU/price/dimensions) still describes that sheet's data shape; only the SKU column has since changed (new short-code scheme, e.g. `PLT-001`) — see [[log]] Session 6.
>
> **Possible resolution to the missing-SEO-catalogue gap:** a spreadsheet called `Concreteworx_NI_Product_Spreadsheet_latest` (id `1_2bZU0BMLLZvm3ZlNd-mNDYZIJmeWnLgNsPF0MRVjsE`, created 2025-12-25) was found in Drive during Session 6 and appears to be the fully SEO-optimised version described below — it has populated Product Title, keywords, HTML Product Description, Short Description, SEO Meta Title/Description, and SEO Permalink. **This was only spot-checked on 2 of 121 rows, not fully verified**, and it uses the old long-format SKUs (e.g. `CW-1006-40-Moneybag`), not the new short codes now live on the site. Do not treat it as confirmed-complete or as the source of truth until (a) all 121 rows are read and checked for genuine completeness, and (b) its SKUs are reconciled to the new scheme.
>
> **UPDATE 2026-08-11 (Session 7):** the sheet at `1VeMS3LVNqNtZqYKrrd9YH6g_8XGHppU3PUUIPdUYQ9c` was designated **source of authority for pricing** and now has a populated Regular price column reconciled against the live site (sheet wins, site updated — never the reverse). Cross-referencing all sheet SKUs against all 112 live WooCommerce products found 5 live-product mismatches, of which 4 were corrected on the site (BEN-001 Roman Bench, BEN-002 Elephant Bench, LGE-004 Donkey and Cart large, LGE-014 Bali lion / Fu Dog); the 5th (PLT-011 Swan) was already correct at the variation level. See [[log]] Session 7 for full method and the list of draft-product price mismatches deliberately left unresolved (not live, out of scope for that session).

## Raw Data Completeness (original sheet, 121 rows — pre-Session 6, SKU column now superseded)

| Field | Populated | Missing |
|---|---|---|
| SKU | 48 / 121 (now: 122/122 on live site + new sheet, new short-code scheme — see [[log]] Session 6) | — |
| Regular price | 67 / 121 in original sheet count. **Session 7: for live (published) products with a sheet price, site now matches sheet — 4 corrected, 1 already correct.** Draft-product mismatches still exist (not in scope), and rows with no SKU couldn't be matched at all. | 54 products in original count; current gap not recounted against the new/priced sheet |
| Dimensions (H/W/L/weight) | 8 / 121 | 113 products (93%) |
| Product Title (SEO) | 0 / 121 in this sheet | Possibly complete in `Concreteworx_NI_Product_Spreadsheet_latest` — unverified, see above |
| Keyword Focus | 0 / 121 in this sheet | Possibly complete in `Concreteworx_NI_Product_Spreadsheet_latest` — unverified, see above |
| Product Description (HTML) | 0 / 121 in this sheet | Possibly complete in `Concreteworx_NI_Product_Spreadsheet_latest` — unverified, see above |
| SEO Meta Title / Description | 0 / 121 in this sheet | Possibly complete in `Concreteworx_NI_Product_Spreadsheet_latest` — unverified, see above |
| SEO Permalink | 0 / 121 in this sheet | Possibly complete in `Concreteworx_NI_Product_Spreadsheet_latest` — unverified, see above |
| Product images (1–5, URL + alt) | 0 / 121 | All — not yet sourced/uploaded |

## See also
- [[Category Structure]]
- [[SEO Strategy]]
- [[Outstanding Work]]
- [[log]] — Session 6 for full SKU reconciliation detail, Session 7 for pricing reconciliation detail
