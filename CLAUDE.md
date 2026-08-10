# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A data-only repository of CIDR IP ranges organized by country. There is no application code, build system, test suite, or linter — the entire content is the `CIDR/` directory plus this documentation and the README.

The data is auto-generated upstream (by EbraSha, https://github.com/ebrasha/) and the upstream project regenerates it on a schedule; commits are wholesale resets of the dataset ("Reset repository and add CIDR and IPv6 files"). Manual edits to the data files will be clobbered by the next regeneration, so treat `CIDR/` as machine-generated output, not hand-maintained source.

## Data layout

All 500 data files live flat in `CIDR/` (the README's claim that each country has its own directory does not match the actual layout — files are flat):

- `CIDR/{CC}-ipv4-Hackers.Zone.txt` — IPv4 CIDR ranges for country `{CC}`
- `CIDR/{CC}-ipv6-Hackers.Zone.txt` — IPv6 CIDR ranges for country `{CC}`

where `{CC}` is the ISO 3166-1 alpha-2 country code (e.g. `US`, `DE`, `IR`). There is one pair of files per country/territory (~250 pairs).

### File format

- Line 1: a `#` comment header with the generator attribution and generation timestamp
- Every subsequent line: exactly one CIDR block (`5.62.60.6/31` or `2001:470:8:88::/64`), no blank lines, no inline comments

Any tooling that consumes these files should skip lines starting with `#`.

## Working in this repo

- There are no build/test/lint commands. Verification of changes means checking the data files themselves (e.g. validating CIDR syntax with a quick script if needed).
- Useful lookups are plain file operations: `grep` a CIDR or prefix across `CIDR/*.txt` to find which country claims it; read `CIDR/{CC}-ipv4-Hackers.Zone.txt` to get a country's ranges.
- Country files vary enormously in size (large countries like US have hundreds of thousands of lines). Prefer `grep`/`head`/`wc -l` over reading whole files into context.
- Documentation changes (README, this file) are the realistic scope for edits here; changes inside `CIDR/` are normally overwritten by the upstream regeneration.
