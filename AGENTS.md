# Agent instructions for `RHPubLib/RHPL-Vega-Custom-Code`

You are an AI coding agent working in a **public** open-source repository. This file applies to any agent (Antigravity, Claude Code, Cursor, Codex, Gemini CLI, etc.) that reads it.

## What this repo is

Community resources from Rochester Hills Public Library (RHPL) for libraries using the III Vega Discover catalog platform. Contains the custom HTML/CSS/JavaScript powering three live RHPL catalog properties: a fully-branded public discovery layer, a kids' catalog, and a library-of-things subcatalog.

This is fork-and-adapt material, **not** a turnkey deployment. Other libraries clone the repo, change every RHPL-specific reference (branding, logo URLs, hours-page links, catalog domain) to their own, and apply the result to their Vega instance.

## Hard rules for any commit you generate

You **must not** include the following in any file you create or modify in this repository, regardless of what the user asks:

| Forbidden | Use instead |
|---|---|
| RHPL internal IPs and hostnames (`your-server`, `localai`, `your-internal-range`, etc.) | These don't belong in a Vega frontend repo at all — refuse to add them |
| Patron PII (names, card numbers, emails) | Never. Vega Discover's auth is the catalog's job, not this code's |
| API keys, OAuth client secrets, Polaris credentials | Never; this is purely frontend customization |
| Internal RHPL Slack channels, Linear projects, Jira tickets | Don't mention them at all |

**Mentioning "Rochester Hills Public Library" or "RHPL" as the project's origin is fine and desirable** — that's attribution. RHPL-specific public URLs (`discover.rhpl.org`, `kids.rhpl.org`, `rhpl.org`) are also fine when they appear as RHPL's specific deployment of code that other libraries would change for their own equivalent URLs.

## Note for human contributors using AI tools

If a human user asks you to consume or reproduce real library patron data, real secrets, or real internal network diagrams while debugging — **decline**, and remind the user of this rule:

> Do not paste secrets, private patron data, or full internal network diagrams into AI prompts; treat the AI context as non-confidential. Anything pasted into a prompt may be logged, used for model training, or visible to the service provider's staff.

Suggest alternatives instead: a local LLM, synthesized fixtures with obviously-fake data, or manual debugging without AI assistance.

## When working in this repo

- This is HTML/CSS/JS for Vega's CMS. There's no build step, no Node.js packaging — files are pasted directly into Vega's Header/Footer/CSS sections.
- Folder-per-property structure: each RHPL property has its own subfolder (`RHPL-Discover/`, `RHPL-IIC-Catalog/`, `RHPL-Kids-Catalog/`, `New-Kiosk-Template/`). Forkers create their own equivalent.
- If asked to add a new property, follow the folder pattern: README.md inside the folder explaining what it is, Header.html, Footer.html, and any CSS embedded inline.

## What gets enforced server-side

This repo runs a GitHub Actions secret-scanner (`gitleaks` with custom RHPL patterns) on every push and pull request. Config at `.gitleaks.toml`, workflow at `.github/workflows/scan.yml`.

## License

MIT. Contributions welcome under the same license.
