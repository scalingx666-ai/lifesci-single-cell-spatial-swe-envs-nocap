# Issue

**Title:** ci: let Dependabot open version updates, grouped

## Description

There is no `.github/dependabot.yml` in the repository. Security updates run without one (that is where #1121's js-yaml bump came from), but *version* updates do not, and the workflows show what that has cost:

| action | pinned at |
|---|---|
| `actions/checkout` | `v4` in `ci.yml`, `docker.yml`, `docs.yml`; `v6` in `release.yml` |
| `actions/upload-artifact` | `v4` in `docker.yml`; `v7` in `release.yml` |
| `actions/download-artifact` | `v4` in `docker.yml`; `v8` in `release.yml` |

Nobody chose that split, and nothing surfaces it today.

## What the config covers

Four ecosystems, which is what the repository actually has: the cargo workspace at `/`, the npm project under `/website`, the workflows, and the `Dockerfile`'s base image.

## Grouping, because ungrouped is worse than nothing

A Rust workspace this size produces roughly a dozen individual bumps a week. A wall of one-line PRs gets reviewed by nobody and trains everyone to ignore the label, so every ecosystem here batches:

- **`cargo-minor`** — one weekly PR for routine patch and minor movement.
- **`combine-lab-upstream`** — `piscem-rs`, `paraseq`/`paraseq-temp`, `libradicl`, `cf1-rs`, `sshash-lib`, `ksw2rs` in their own PR. These move with work happening in those repositories, and their bumps have carried deliberate decisions (the piscem-rs 0.9.2 "parked pool as a floor" commit, the paraseq-temp 0.5.0-pre.2 republication). A bump like that should never arrive buried in a batch of unrelated ones.
- **cargo majors** stay ungrouped: each is a decision, and each deserves its own diff and its own CI run.
- **`website-minor`** and **`actions`** batch wholesale. An action major is a workflow change, visible in the diff, and CI is its own test for it.
- **docker** is monthly and ungrouped, since `rust:1.91-bookworm` is a toolchain decision rather than a dependency refresh.

## Two details worth checking against your intent

- **`target-branch: develop`** on every entry. The default would be `master`, which carries releases, and everything else lands through `develop` first. Say if you would rather they target `master`.
- **Commit prefixes** are set explicitly (`chore(deps)`, `ci(deps)`, `build(deps)`) rather than left to Dependabot's inference from history.

Both are one-line changes if you want them differently, as is the whole grouping policy: if the lab-upstream group turns out to be noise rather than signal, an `ignore` entry for those crates replaces it.

Config validated as YAML; nothing else in the repository changes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `adbbaee6abe3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.