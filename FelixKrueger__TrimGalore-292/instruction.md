# Issue

**Title:** docs(citation): forward citation metadata into master

## Description

## Summary

- Forwards `dev` into `master` for the single squash commit from PR #291 (`CITATION.cff`, `.zenodo.json`, credits page DOI fill-in).
- Fixes a 404 in the live docs site: `docs/src/content/docs/reference/credits.md` links to `blob/master/CITATION.cff`, which doesn't exist until this lands on master.
- Makes the GitHub **"Cite this repository"** sidebar appear on the repo — the button reads from the default branch (master).

## Why outside the usual release-time FF

Per the workflow model (dev = canonical truth, master = release pin), master normally only FFs from dev at release time. Exception is justified here because:

- The change is **metadata-only** — no source, no test surface, no behavior change. Doesn't affect the v2.2.0 binary or anyone pinning to the v2.2.0 tag.
- Real pinning model is **tag-based** (`v2.2.0`), not branch-tip-based. Tag pinners are unaffected.
- The live docs site (auto-deployed from dev) already advertises both DOIs and links to `CITATION.cff` on master — without this FF the link is broken for users.

## Mechanics

This is a **true fast-forward** — `master` is a strict ancestor of `dev`. No merge commit needed:

```
master..dev:  44444aa docs(citation): add CITATION.cff and .zenodo.json for v2.2.0 (#291)
dev..master:  (empty)
```

Recommend **"Rebase and merge"** to preserve linear history.

## Test plan

- [ ] After merge, https://github.com/FelixKrueger/TrimGalore/blob/master/CITATION.cff loads (no 404).
- [ ] "Cite this repository" button appears in the repo sidebar.
- [ ] The credits page link on https://www.trimgalore.com resolves.
- [ ] No CI surface impact (metadata-only); checks should mirror PR #291's all-green result.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65e4378fc30b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.