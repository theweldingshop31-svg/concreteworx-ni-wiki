---
tags: [project, tooling, mcp, wordpress]
---

# WordPress MCP (concreteworxni-wp)

← [[Home]] · [[Outstanding Work]]

> ⚠️ **Tool prefix: `mcp__concreteworxni-wp__*`.** Do not use `mcp__wordpress-mcp__*` for this project — that connector is hardcoded to a different client's site (horseaddict.co.za) and will return that site's data without error. See `CLAUDE.md` at the repo root and `log.md` Session 6 (2026-08-11) for how this was discovered.

A local MCP server giving Claude full read/write access to concreteworxni.com — content, media, taxonomies, users, comments, plugins, themes, settings, and (via a companion mu-plugin) active-theme file editing. Built 2026-08-10, lives in `mcp-server/` in this repo.

## Why it's not committed to the public repo
This repo (`concreteworx-ni-wiki`) is public. The MCP server code itself contains no secrets (auth lives in a gitignored `.env`), but as an admin-capability tool for the live site, it's kept local-only by deliberate choice rather than pushed alongside wiki content — same policy applied to [[CWNI-GSC-MCP]].

## Components
- `mcp-server/src/` — TypeScript MCP server, WP REST API v2 (Application Password auth)
- `mcp-server/wordpress-plugin/concreteworxni-mcp-theme-bridge.php` — mu-plugin adding secured theme-file read/write/delete/list endpoints core WP lacks, gated by `edit_themes` capability + a separate shared secret, path-traversal protected, auto-backs up (`.bak`) before overwriting/deleting

## Status
Confirmed working end-to-end 2026-08-10: authenticated as WP user NevWally31; theme bridge live against active theme `blocksy-child` (a child theme — the safe target for customisations, survives parent theme updates).

## See also
- Full setup instructions: `mcp-server/README.md`
- [[CWNI-GSC-MCP]] — the equivalent tool for Search Console access
