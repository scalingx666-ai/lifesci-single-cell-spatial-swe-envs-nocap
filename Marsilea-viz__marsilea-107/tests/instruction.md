# Issue

**Title:** docs: canonical llms.txt URL, add context7.json

## Description

## Summary

Two small discovery fixes for AI agents, following on from #106.

## Canonical `llms.txt` URL

Read the Docs serves `llms.txt` at the domain root natively, from the project's
default version. Confirmed after the `v0.7.0.post1` release:

```
https://marsilea.readthedocs.io/llms.txt            200   x-rtd-path: /proxito/html/marsilea/stable/llms.txt
https://marsilea.readthedocs.io/en/stable/llms.txt  200
https://marsilea.readthedocs.io/en/latest/llms.txt  200
```

`README.md`, `docs/README.md` and `ai_assistants.rst` now point at
`https://marsilea.readthedocs.io/llms.txt` — the path assistants actually probe,
and the one that does not pin a version.

`docs/README.md` also claimed the root URL needs a Read the Docs **Exact
redirect**. It does not — the response above is a direct 200, no redirect. That
note is replaced with the constraint that actually bites: the root URL only
reflects a change once it lands in a release, because the default version is
`stable`, which tracks the latest tag. That is precisely why the file 404'd at
the root between #106 and `v0.7.0.post1`.

## `context7.json`

Marsilea is already indexed on [Context7](https://context7.com/marsilea-viz/marsilea)
(182 snippets, trust score 6.2), which agents use to pull library docs on demand.
`context7.json` steers that indexing at `docs/` and `src/` instead of the whole
repository, and ships a few usage rules with the extracted snippets.

## Test plan

- [x] Probed all three `llms.txt` URLs; all 200
- [x] Confirmed the root URL is served directly, not via redirect (`x-rtd-path`)
- [x] `context7.json` validates as JSON against the documented schema fields

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `11d20cd16c8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.