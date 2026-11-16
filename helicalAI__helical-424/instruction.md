# Issue

**Title:** ci: add `ci` aggregator job as the single required status check

## Description

Adds a single, uniformly-named `ci` gate job so `helicalAI/github-configs` can require **one** status check name across the org.

Refs: 
Closes the Bastion SOC 2 control `github-automated-code-checks`.

## Why two files

This repo's default branch is **`release`**, not `main`, and the two workflows have disjoint base-branch filters:

| workflow | `on.pull_request.branches` | fires for |
|---|---|---|
| `main.yml` | `[main]` | PRs based on `main` |
| `release.yml` | `[release]` | PRs based on `release` (the default branch) |

A `ci` job in `main.yml` alone would produce **no check run at all** on PRs to `release`. Making `ci` required would then leave every PR to the default branch stuck on "Expected — waiting for status to be reported", forever. So `ci` is added to both files; since the filters are disjoint, a given PR only ever triggers one of them and only one check named `ci` is produced.

Per `CONTRIBUTING.md` this PR targets `main`; the `ci` job reaches `release.yml` on the branch via the team's periodic `main` → `release` merge.

## `needs:` used, and why

**`main.yml`** — `[tests, integration-tests, flash-attn-integration, notebooks]`
Every job in the file.

**`release.yml`** — `[fresh-install, tests, integration-tests, flash-attn-integration, notebooks]`
Every job except `release`, which tags and publishes to PyPI. Requiring it would mean "you cannot merge until the code is released" — and since its `Check if tag exists` step exits 1 whenever the version is already tagged, including it would make `ci` red on every PR that doesn't bump the version, blocking all merges to the default branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `af71a72b27a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.