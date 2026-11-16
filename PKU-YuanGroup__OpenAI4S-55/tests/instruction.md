# Issue

**Title:** chore(lint): move ruff to astral-sh v0.16.0 and pin the rule set explicitly

## Description

Replaces #47, which bumped the pin alone and left `Lint (pre-commit)` — a **required** check — red with 1081 findings.

## The bump was never the problem

This repository has no `[tool.ruff]` section at all, so the rule set is silently whatever the pinned ruff calls its *default*. Verified in an isolated empty directory with no repo config and no user config (`~/.config/ruff` does not exist):

| ruff | rules enabled by default |
|---|---|
| 0.0.274 (current pin) | 59 — effectively `E` + `F` |
| 0.16.0 | **413** |

So moving the pin was not a version bump. It was an unreviewed adoption of ~350 rules across families this codebase has never been checked against — `S` (bandit), `UP`, `RUF`, `BLE`, `ISC`, `PIE`, `TRY`, `FURB`, `PLW`, `PYI` and more. Reproduced locally with the hook's exact arguments:

```
164  S110    try-except-pass
116  UP035   deprecated-import
108  RUF100  unused-noqa
 82  RUF012  mutable-class-default
 66  RUF059  unused-unpacked-variable
 61  BLE001  blind-except
 ...
```

1081 findings, of which `--fix` would have rewritten 502 in place and 579 had no automatic fix at all.

## The fix: state the rule set instead of inheriting it

`[tool.ruff.lint] select = ["E", "F"]` reproduces the rule set this codebase was actually written against, and

```
ruff 0.16.0 check --select=E,F --ignore=E501,F401,E722,E402,E741 .
```

returns `All checks passed!` on this tree.

This is the load-bearing part of the change, and the comment in `pyproject.toml` plus the note in `CLAUDE.md` both say why — because the failure mode is silent. Without a `select`, the *next* ruff bump re-runs this whole experiment on whatever that version decides its defaults are.

Adopting further families is real work with real value. It is also a lint-policy decision that deserves its own PR, one family at a time, where the diff can be read — not a side effect of Dependabot moving a pin.

## Two corrections to the pin itself

- **Repo → `astral-sh/ruff-pre-commit`.** `charliermarsh` is a redirect: `gh api repos/charliermarsh/ruff-pre-commit` reports `full_name=astral-sh/ruff-pre-commit`, `archived=false`. The canonical name should be what is written down.
- **Hook id `ruff` → `ruff-check`**, which is what the manifest provides now that `ruff format` exists and a bare `ruff` is ambiguous.

`E402` and `E741` stay in the ignore list and are genuinely still doing work — both are inside the `E` family that `select` now enables. (Worth stating explicitly because it is easy to assume otherwise.)

## Verification

- `uv run pre-commit run --all-files` — every hook passes, with the ruff hook resolving as `ruff check`.
- The 59-vs-413 counts come from `ruff check --show-settings` in a scratch directory containing only a one-line `a.py`, so neither this repo's config nor a user-level config can be involved.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c50590a1368d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.