# Issue

**Title:** ci(docs): build the docs site on pull requests

## Description

Closes a gap found while merging #368: **a docs dependency bump can merge with eight green checks, none of which builds the docs site.**

`docs.yml` triggers only on `push` to `master`/`dev`, and a push to `dev` auto-deploys to www.trimgalore.com. So the first validation of any docs change — content or dependency — was the live deploy on the trunk. #368 bumped `satori` 0.28 → 0.29 (a 0.x minor, which can break under semver-for-0.x); I built the site by hand before merging it. This automates that step.

**This PR is its own first test** — the new `Docs build (Astro)` check below is the thing being added.

## Why `ci.yml` and not a `pull_request` trigger on `docs.yml`

The decisive reason: `docs.yml` carries a `paths` filter, and a path-filtered workflow triggered on `pull_request` reports **nothing at all** on a PR touching no `docs/**` path — not a skipped check, not a neutral one. If that check were ever made required, those PRs would block forever, and the standard workaround is a duplicate no-op workflow with the same name.

Two lesser reasons, both *soluble* and therefore not decisive on their own: `docs.yml` grants `pages: write` at workflow level, which same-repo PR runs inherit (job-level `permissions:` would override it); and its `concurrency: group: pages` would serialise PR builds behind live deploys (a per-event group would fix it). Its `deploy` job would also need an event guard, and that path is the one worth not touching.

Cost: the four build steps now exist in two workflows. Cross-referenced in both, and dependabot's `github-actions` group already updates their pinned SHAs together — observed on #367.

## The assertion is the point, not the build

A satori renderer failure can leave a **zero-byte PNG while `astro build` still exits 0**. Verified by patching the OG endpoint two ways:

| Simulated failure | exit | on disk |
|---|---|---|
| endpoint throws | **1** | build aborts, no `dist/og` |
| renderer returns an empty buffer | **0** — `31 page(s) built` | a **0-byte** PNG |

Hard failures are already caught by build status. The silent write is the gap, and it is the same shape that let the `-a2` defect (#369) survive three releases behind a green parity gate.

Four properties of the check, each from a measured failure mode:

- **`test -d dist/og` first.** A wrong path under `bash -e` without `pipefail` prints to stderr and exits **0**, so the job would be inert and green. A bare `-d` test cannot be pipeline-swallowed.
- **Counts before the size check.** With `dist/og` absent, the size check alone exits 0 — `find`'s status is discarded by `$(…)`.
- **Recursive `find`, not a glob.** Of 30 OG images only **3** are top-level; 27 are nested. A top-level glob passes with a nested zero-byte PNG present.
- **`-size -10240c`, not `-size 0` or `-size -1k`.** Both BSD and GNU `find` round `-1k` up to a block, so a 500-byte truncation escapes. The smallest real OG image is 23 kB, so a 10 kB floor never needs updating as pages are added.

Paths are relative to `docs/` because `working-directory` is set. Worth noting `docs.yml` itself mixes conventions — its `path: docs/dist` is repo-root-relative, because `with:` inputs ignore `working-directory` — which is easy to copy wrongly.

## Also in this PR

`justfile`'s `logos`, `docs` and `docs-dev` recipes ran `cd Docs`; the directory is `docs/` (`git ls-files` has 0 entries under `Docs/`, 154 under `docs/`). They worked on case-insensitive filesystems and failed on Linux. Those recipes exist to give contributors local CI parity, so adding a docs-build gate while `just docs` fails on Linux would ship half of it.

## Verification

Every check was shown to **fail** before being trusted to pass — the lesson of #369, where a plausible parity gate never exercised the flag it was meant to protect:

| Case | Result |
|---|---|
| Clean build | assertion exits 0, reports 32 HTML pages / 30 OG images |
| Nested **empty** PNG | exits 1, names the file |
| Nested **500-byte truncated** PNG | exits 1 (`-size 0` and `-size -1k` both miss this) |
| `dist/og` **absent** | exits 1 from `test -d` |
| Missing required `title:` in a page | build exits 1 |
| Bad sidebar `slug:` in `astro.config.mjs` | build exits 1 |
| Non-recursive glob, nested empty PNG | exits **0** — the form this deliberately avoids |
| `just docs` after the fix | exits 0 |

All rehearsed from `docs/`, matching the job's cwd — rehearsing from the repo root would have passed while the workflow step was inert.

Reviewed by two independent plan reviewers before implementation (read-only). They found two Criticals and six Importants, all in the *verification* rather than the change: the break I had chosen for the "prove it can fail" test **did not fail the build** (Starlight ignores unknown frontmatter keys), and the assertion as first specified could have been a silent no-op that my own validation table could not detect. Full record in `plans/docs-build-pr-check/PLAN.md` §11.

Checks go 8 → 9.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c5c18342504b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.