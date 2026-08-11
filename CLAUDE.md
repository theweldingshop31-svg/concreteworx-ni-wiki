# ConcreteWorx NI — Project Instructions for Claude

This is the working vault/repo for ConcreteWorx NI (concreteworxni.com). Read this before using any MCP tool in this project — several similarly-named MCP connectors are registered globally on this machine and point at **other clients' sites**, not this one. Using the wrong one has already wasted a full session (2026-08-11) before being caught.

## MCP connectors: use these, not the look-alikes

| Need | ✅ Correct connector (tool prefix) | ❌ Do NOT use | Why |
|---|---|---|---|
| WordPress content/SEO/theme access | `mcp__concreteworxni-wp__*` | `mcp__wordpress-mcp__*` | `wordpress-mcp` is hardcoded to **horseaddict.co.za** — a different client's site. It will silently return that site's data with no error telling you it's the wrong property. |
| Google Search Console data | `mcp__cwni-gsc__*` | `mcp__gsc__*` | `gsc` is hardcoded to **secretsense.co.za** — a different client's Search Console property. `inspect_url` rejects concreteworxni.com URLs outright when you accidentally use it, but other calls (e.g. `list_sitemaps`) will return the wrong site's data without erroring. |

**If a tool call for this project needs to touch WordPress or Search Console, verify the tool name starts with `concreteworxni-wp` or `cwni-gsc` before calling it.** If neither is available in the current session's tool list, they are registered but not attached — see "If the connectors aren't attached" below. Do not fall back to `wordpress-mcp` or `gsc` "just to check something quickly" — there is no read that's safe to run against the wrong client's live property by accident.

## Background — how this was discovered

Session 2026-08-11 started by using `wordpress-mcp` and `gsc` (available, connected, no error) to look up ConcreteWorx NI data. Both returned real data with no indication it was for the wrong site — `wordpress-mcp`'s own tool descriptions literally name "horseaddict.co.za" in places, which is what eventually gave it away. `concreteworxni-wp` and `cwni-gsc` are the actual project-specific servers, built specifically for this site in earlier sessions (see [[WordPress MCP]] and [[CWNI-GSC-MCP]] in this vault, and `log.md` Session 2 / Session 4). Full detail on this specific incident: `log.md`, Session 6 (2026-08-11).

## If the connectors aren't attached

Both are local stdio MCP servers registered project-locally (`claude mcp list` should show `concreteworxni-wp` and `cwni-gsc`). If they don't appear in the current session's tool list:
1. Run `claude mcp list` to confirm they're registered and check connection status.
2. If "Failed to connect," check `mcp-server/.env` and `cwni-gsc-mcp/.env`-equivalent secrets exist and are populated (see each tool's own README for setup).
3. MCP servers only attach at session start — if you just fixed a config or registration issue, the session needs to be restarted before the fix takes effect. Tell the user this rather than retrying tool calls in the same session.

## Repo layout notes

- `mcp-server/` (→ `concreteworxni-wp`) and `cwni-gsc-mcp/` (→ `cwni-gsc`) are **deliberately untracked/local-only** — not pushed to this public wiki repo, to avoid publicly associating admin-level site credentials/tooling with a public repo. This is intentional, not an oversight — don't try to `git add` them.
- `Files to ingest/` is untracked scratch space for source documents being folded into the wiki — also intentional.
- Wiki content (`Home.md`, `log.md`, `Project/*.md`) is the tracked, public part of this repo and should stay in sync with actual project/tooling state — update it when tooling, data, or major findings change, per the pattern in `log.md`.
