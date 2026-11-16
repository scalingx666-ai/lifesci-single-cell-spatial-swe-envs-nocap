# Issue

**Title:** ci: stop running the whole matrix twice on every same-repo PR

## Description

Follow-up from the #1170 / #1174 discussion, and independent of both.

`ci.yml` triggers on `push: branches: ["**"]` *and* `pull_request`. A branch pushed to this repository and then opened as a PR matches both, so the four-way `build-test` matrix runs twice against the same commit.

#1172 is the evidence — two runs, same SHA, same four contexts:

| run | build-test (macos-15-intel) | build-test (ubuntu-22.04) |
|---|---|---|
| [32668385956](https://github.com/COMBINE-lab/salmon/actions/runs/32668385956) | 38m20s | 24m15s |
| [32668407492](https://github.com/COMBINE-lab/salmon/actions/runs/32668407492) | 15m46s | 7m20s |

So one PR was costing roughly an extra hour of macOS runner time for no additional signal. Fork PRs were never affected — a fork's pushes run in the fork — so this only ever doubled the cost of branches pushed here directly, which is to say @rob-p's.

## What changes

Push CI narrows to `master` and `develop`. Those genuinely need it: both receive direct pushes (release bumps, release notes, `master` -> `develop` merge commits) that never appear in a PR, so without a push trigger they would get no CI at all.

`pull_request` and `workflow_dispatch` are unchanged, so every PR still runs the full matrix exactly once.

## The trade, stated

A branch pushed to this repository with no PR open now gets no CI until one is opened. That is intended rather than incidental: CI runs on what is proposed for merge, plus whatever lands on the long-lived branches directly. `workflow_dispatch` is still there if you want a run on a bare branch.

## Checked

- YAML parses; triggers resolve to `push` (master, develop), `pull_request`, `workflow_dispatch`; the `build-test` job is untouched.
- Nothing in the repository chains off this workflow — no `workflow_run` consumers, and `release.yml` / `docker.yml` / `docs.yml` have their own independent triggers.
- The four required-check context names are unchanged, so this does not disturb any future branch-protection configuration.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dcffac62c133`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.