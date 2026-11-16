# Issue

**Title:** docs(citation): add CITATION.cff and .zenodo.json for v2.2.0

## Description

## Summary

- The Zenodo record at <https://zenodo.org/records/5127899> is from the Perl 0.6.x era and won't auto-update. Add the two metadata files that drive the next Zenodo deposit and the GitHub "Cite this repository" sidebar.
- `CITATION.cff` — v2.2.0 + 2026-05-07 release date. ORCID and DOI identifiers left as `TODO` comments so they can be filled in once the v2.2.0 Zenodo deposit is minted.
- `.zenodo.json` — overrides default metadata (title, abstract, keywords, related identifiers) on the next GitHub-release-triggered deposit so the Zenodo webhook doesn't have to guess from the release notes.
- Tightened `docs/src/content/docs/reference/credits.md` to reference `CITATION.cff` instead of the vague "pick the version-specific DOI from the release page" line.

## Out of scope (manual follow-up on Zenodo)

The DOI minting itself happens on Zenodo, not in the repo:

1. Enable the GitHub→Zenodo webhook at <https://zenodo.org/account/settings/github>, or
2. Click **New version** on the existing 5127899 record and upload the v2.2.0 tarball.

Then fill in the `identifiers:` block (concept + version DOI) and the `orcid:` field in `CITATION.cff`.

## Test plan

- [ ] GitHub renders **"Cite this repository"** in the sidebar from `CITATION.cff` (visible after merge to a default-branch ancestor; on `dev` it'll appear once `dev` becomes default or post-FF to `master`).
- [ ] `.zenodo.json` validates as JSON: `python -m json.tool .zenodo.json`.
- [ ] `CITATION.cff` validates against the CFF schema (e.g. `cffconvert --validate`).
- [ ] No effect on `cargo build`, `cargo test`, CI validation matrix — metadata-only PR.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65e4378fc30b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.