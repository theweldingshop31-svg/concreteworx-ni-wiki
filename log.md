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

## 2026-08-10 — Session 5: Internal-link diagnostic + indexing requests

**Work:** Ran the diagnostic step flagged as unresolved at the end of Session 4 — fetched raw (non-JS-rendered) HTML as Googlebot (`curl -A Googlebot`) for the homepage, all 4 paginated `/shop/` pages, and one sample product page, then checked link structure, `robots` meta, canonical tags, and `robots.txt`.

**Finding (verified, direct HTML inspection):** internal linking is **not** the cause of the indexation gap. Homepage and `/shop/` contain real, crawlable `<a href>` links (no JS-injection dependency, no `nofollow`) to all category pages and — across the 4 shop pagination pages — effectively all ~50 live products. Sample product page has correct `index, follow` robots meta, self-referencing canonical, no `noindex`. `robots.txt` has no disallow on `/product/` or `/product-category/`. This **disproves hypothesis #1** from Session 4 (no crawlable internal link path). [[SEO Audit Findings]] updated in place with this result and a revised, re-ranked hypothesis list (crawl backlog / low domain authority now the leading explanation).

**Secondary finding (minor, not a blocker):** homepage has duplicate `http://` and `https://` versions of the same category links (e.g. `garden-benches` appears under both protocols) — mild link-equity dilution, not yet added to [[Outstanding Work]] as a formal item.

**Action attempted:** submitted 3 unindexed product URLs (Roman Bench, Wood Stump Planter, Elephant Bench) to Google's Indexing API via `cwni_gsc_submit_batch`, twice (initial attempt + retry after user attempted a permissions fix). **Both attempts failed** — `Permission denied. Failed to verify the URL ownership.` on all 3 URLs each time. Per [[CWNI-GSC-MCP]], this connector uses OAuth (not a service account), so the fix requires either enabling the Indexing API on the correct GCP project or the OAuth-authenticated Google account holding **Owner** (not just full/restricted user) role on the `https://concreteworxni.com/` Search Console property. **This was not confirmed fixed** — the retry failed with an identical error, so either the permission change wasn't completed, hasn't propagated, or was applied to the wrong account/project. Status: unresolved.

**Fallback:** user manually submitted the same 3 URLs via Search Console's UI ("Request Indexing") outside of any tool — confirmed done by the user in chat, but **not independently verified** by me (no tool call was made to check `inspect_url` status post-submission).

**Verification state:** internal-linking finding is directly verified (raw HTML inspected). Indexing API failure is directly verified (error returned twice). Manual Search Console submission is **user-reported, not tool-verified** — should be checked with `inspect_url` in a few days once Google has had time to (re)crawl.

**Repo:** `Project/SEO Audit Findings.md` modified, not yet committed as of session close (see Status below).

---

## 2026-08-11 — Session 6: SKU reconciliation + new short SKU scheme

**Work:** Connected `concreteworxni-wp` (the local WordPress MCP built in Session 2) to a live session for the first time — it had been registered but never actually attached. Diagnosed and fixed a real bug in the process: `mcp-server/src/wpClient.ts` used `dotenv/config`, which resolves `.env` relative to `process.cwd()`; since Claude Code launches the server from the repo root (not `mcp-server/`), env vars were silently empty and the server crashed on every launch. Fixed to resolve `.env` relative to the script's own directory via `import.meta.url`; rebuilt (`npm run build`); verified fixed by sending a raw MCP `initialize` handshake from the repo root before and after the change (failed, then succeeded). Not committed to git — `mcp-server/` remains untracked/local-only per the Session 2 decision.

**Work:** Pulled the full live WooCommerce product list (122 products, all fields) from concreteworxni.com via `wp_raw_request` against `/wp-json/wc/v3/products`, and matched it by product name against the (now-superseded) original Google Sheet (`1ReLvmImVcPqcu8IMWW1aV8lvtRmrt4GRkSSjzOmE7JM`, 91 rows). Found: 46 clean SKU matches, 4 SKU mismatches (sheet SKU ≠ live SKU), 1 sheet SKU misassigned to the wrong product (a "Pergola" row carried the SKU that actually belonged to "Donkey and Cart large" on the live site), 39 rows with no SKU on either side, and 22 live products absent from the sheet entirely (Welcome Signs, Memorial Plaques, Football Club Memorabilia, Vehicles — these categories were already documented as populated in [[Category Structure]], just not represented as rows in this particular sheet). Delivered as an artifact table, not written anywhere yet at this point.

**Decision (user-directed):** Replace all SKUs — on both the live site and the sheet — with a new, shorter scheme: 3-letter category code + 3-digit sequence (e.g. `PLT-001`, `BEN-002`), assigned in ascending WooCommerce product-ID order within each category. Category assigned primarily from each product's live WooCommerce category taxonomy, falling back to a keyword match against the product name suffix (e.g. "— Concrete Garden Bench") for the ~90 products tagged only with the generic "Concrete Worx NI" category. Two products had no classifiable signal at all (Boy with Wheelbarrow planter → id 939; Easter Island Lopsided Head → id 961) and were assigned by manual judgment (PLT and LGE respectively) rather than by rule.

**Action:** Wrote the new SKUs to all 122 live WooCommerce products via 5 batched `POST /wp-json/wc/v3/products/batch` calls (30/30/30/30/2). Spot-verified one product (`id 937 → PLT-001`) by re-fetching it individually post-write. **The other 121 were not individually spot-checked post-write** — batch-response payloads were used to confirm item counts only (30/30/30/30/2 = 122), not full field-by-field content, since raw responses exceeded the tool's output limit and had to be read from cached files.

**Action:** Built a replacement Google Sheet (`1VeMS3LVNqNtZqYKrrd9YH6g_8XGHppU3PUUIPdUYQ9c`, created via `create_file` since no Sheets write/update tool is available in this session — only create/copy/read/download/search) containing the new SKUs matched to the original sheet's 91 product rows (not all 122 live products — the 22 live-only products were not added to the sheet). User then manually deleted the original sheet and edited the new one directly in the Sheets UI.

**Finding surfaced by the user's edit (verified 2026-08-11 by re-reading the live sheet):** the live site has **two separate WooCommerce products both named "Donkey"** (id 960, categorised under `Large Garden Ornaments`, and id 1019, categorised under both `Animal Garden Ornaments` + `Large Garden Ornaments`) — both received distinct new SKUs in the batch write (`LGE-006` and `LGE-015`). The user's manual sheet edit collapsed these to a single "Donkey" row keeping only `LGE-015`. **This means the sheet and the live site are no longer 1:1 consistent**: the live site still carries `LGE-006` as an active product SKU that no longer appears anywhere in the sheet. Not resolved this session — needs a decision on whether id 960 is genuinely a duplicate (delete/merge on the live site) or a distinct variant that the sheet should not have collapsed.

**Finding (accidental, via Drive search while verifying the rename request):** a **third, previously undocumented spreadsheet** — `Concreteworx_NI_Product_Spreadsheet_latest` (id `1_2bZU0BMLLZvm3ZlNd-mNDYZIJmeWnLgNsPF0MRVjsE`, created 2025-12-25, 121 rows) — already contains the fully SEO-optimised catalogue that [[Catalogue Data Status]] and [[Outstanding Work]] have been describing since Session 1 as "built in a separate session, output file not re-uploaded, single biggest gap to close." **This appears to be that missing file** — it has populated Product Title, three-tier keywords, full HTML Product Description, Short Description, SEO Meta Title/Description, and SEO Permalink for at least the first several rows inspected (Money Bag Planter, Trellis Planter Small confirmed by content snippet; **remaining ~119 rows not individually verified**). It uses the **old, long-format SKUs** (`CW-1006-40-Moneybag`, etc.) — not yet reconciled with the new short-code scheme adopted this session. This is a significant find that changes the shape of [[Outstanding Work]] item 4, but requires (a) full-content verification of all 121 rows, (b) reconciling its old SKUs to the new scheme, and (c) a decision on whether to treat it or the new short-SKU sheet as the master, before either can be called the source of truth.

**Requested but not completed:** user asked to delete the original sheet and rename the new one to the original's name. The delete was carried out (confirmed by the original file ID no longer appearing in a Drive search for `Concreteworx` spreadsheets). **The rename was not carried out** — no Drive rename/update-metadata tool is available in this session (only create, copy, read, download, search, get_permissions); the new sheet's title is still `Concreteworx NI Product Spreadsheet — New SKUs (2026-08-11)` as of this session's close. Flagged to the user as a manual step; not confirmed done as of session close.

**Verification state:** Live WooCommerce write — confirmed via batch-response item counts (all 5 batches) and one direct re-fetch (`id 937`); not exhaustively field-verified. Sheet deletion — confirmed by absence from search. Sheet rename — **not done**. Third spreadsheet's completeness — partially confirmed (content snippet only), not fully read. Donkey duplicate-SKU conflict — directly confirmed by comparing live category-tagged data against the current sheet content.

**Wiki pages updated this session:** [[Home]], [[Catalogue Data Status]], [[Outstanding Work]] (close-out); [[WordPress MCP]], [[CWNI-GSC-MCP]] (added explicit "don't use the look-alike connector" warnings, below).

**Follow-up, same day:** added a `CLAUDE.md` at the repo root — read automatically by Claude Code at the start of every session in this directory — documenting that `mcp__concreteworxni-wp__*` (not `mcp__wordpress-mcp__*`, which is horseaddict.co.za) and `mcp__cwni-gsc__*` (not `mcp__gsc__*`, which is secretsense.co.za) are the correct tool prefixes for this project. This is the root cause fix for the wrong-connector time loss described at the top of this session: `wordpress-mcp` and `gsc` were used first because they were simply the first plausibly-named tools found, with no signal in-session that they belonged to other clients until their own data (a horseaddict.co.za page list; a `secretsense.co.za`-labelled tool description) gave it away. Also added matching warning banners to [[WordPress MCP]] and [[CWNI-GSC-MCP]] and to [[Home]]'s tooling section.

**Not done:** `wordpress-mcp` and `gsc` were **not deregistered or deleted** — they are legitimate connectors for other clients (horseaddict.co.za, secretsense.co.za respectively) registered globally on this machine, not broken or CWNI-specific clones, so removing them would likely affect other projects. Flagged to the user rather than acted on unilaterally — see chat.

---

## Open questions carried forward

1. ~~Why aren't product/category pages indexed?~~ Internal linking ruled out (Session 5). Remaining live hypothesis: crawl backlog / low domain authority on a site whose sitemap has sat unindexed for 7+ months. **Not yet resolved** — awaiting recrawl results on the 3 manually-submitted URLs.
2. **Indexing API permission fix still broken.** Two attempts, two identical "Permission denied" errors. Needs verification that (a) Indexing API is enabled in the right GCP project, (b) the OAuth account has Owner role on the correct property, (c) the token cache (`~/.gsc-mcp/oauth-token.json`) was refreshed after any permission change. Not diagnosed further this session — user chose to work around it manually rather than continue troubleshooting.
3. **Manual indexing requests not yet verified.** Roman Bench, Wood Stump Planter, and Elephant Bench product pages were submitted via Search Console UI by the user, but no `inspect_url` check has confirmed Google acted on the requests. Check in a few days.
4. Domain vs. URL-prefix property permission mismatch in Search Console — not investigated further; workaround (use URL-prefix) is in place and working, but the underlying permission gap on the domain property hasn't been explained or fixed.
5. `mobileUsability: VERDICT_UNSPECIFIED` on all `inspect_url` results — not a confirmed issue, just an unpopulated field; worth checking if this stays unspecified as more URLs are inspected, or if it's a quirk of the tool/API response for this account.
6. Minor: duplicate `http`/`https` category links on homepage (found Session 5) — not yet triaged into [[Outstanding Work]].
7. **Live "Donkey" duplicate (Session 6).** Two WooCommerce products both named "Donkey" (id 960 = `LGE-006`, id 1019 = `LGE-015`) — genuine duplicate or distinct variant needing a clearer name? The sheet now shows only one; the site still has both.
8. **Third spreadsheet's completeness unverified (Session 6).** `Concreteworx_NI_Product_Spreadsheet_latest` (id `1_2bZU0BMLLZvm3ZlNd-mNDYZIJmeWnLgNsPF0MRVjsE`) looks like the long-lost fully-SEO'd catalogue, but only 2 of 121 rows were content-checked. Needs full read-through, and its old-format SKUs need reconciling against the new short-code scheme before it can be treated as source of truth.
9. **Sheet rename not done.** New sheet (id `1VeMS3LVNqNtZqYKrrd9YH6g_8XGHppU3PUUIPdUYQ9c`) still titled "Concreteworx NI Product Spreadsheet — New SKUs (2026-08-11)" — user needs to rename manually (no Drive rename tool available in this session).
10. **121 of 122 live SKU writes not individually spot-checked** — batch counts confirmed all 122 accepted, but only 1 product (`id 937`) was re-fetched to confirm the field actually persisted correctly.
