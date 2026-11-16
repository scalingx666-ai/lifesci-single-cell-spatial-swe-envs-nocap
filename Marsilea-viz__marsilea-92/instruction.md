# Issue

**Title:** ci: replace archived ruff-action, pin ruff version and rule set

## Description

## Problem

`.github/workflows/lint.yaml` used `chartboost/ruff-action@v1`, which was archived in 2024 and pinned no ruff version — it installed whatever ruff was latest at run time.

ruff **0.16.0** widened the *default* rule set. Because `pyproject.toml` had `[tool.ruff.lint.per-file-ignores]` but no `select`, the project inherited that default, so lint results changed under it with no code change:

| ruff | enabled rules | `ruff check ./src` on `4ea122e` |
| --- | --- | --- |
| 0.9.4 (current `uv.lock`) | 59 (`E`, `F`) | All checks passed |
| 0.11.7 (current pre-commit rev) | 59 | All checks passed |
| 0.15.22 | 59 | All checks passed |
| **0.16.0** | **413** (adds `I`, `FA`, `S`, `SIM`, `TRY`, `UP`, `D`, `N`, …) | **157 errors** |

That is why #91 — which touches only `pyproject.toml` and `uv.lock`, no Python files — fails with 157 errors in `src/oncoprinter/preset.py` and friends. It is the first ruff run since 2026-07-08; every PR that passed last ran on 2026-06-13 or earlier. All 157 findings are the rule-set change, not a regression.

## Change

- Switch to the maintained `astral-sh/ruff-action@v3` with an explicit `version: "0.15.22"`.
- Add an explicit `select` to `pyproject.toml`.

The explicit `select` is needed as well as the version pin, for two reasons: `ruff-action@v3`'s `version` input defaults to reading the version from `pyproject.toml`, where the `dev` group lists a bare `"ruff"` and so falls back to `latest`; and a version pin alone means the next intentional ruff bump silently re-widens the rule set. The values are ruff's historic default and reproduce exactly the 59 rules that 0.9.4 through 0.15.x enabled, so the lint contract is unchanged.

## Verification (on this branch, tree identical to `main` apart from these two files)

- `ruff 0.15.22 check ./src` — the action's exact invocation — reports `All checks passed!`, exit 0.
- ruff 0.9.4, 0.11.7, 0.15.22 and 0.16.0 now all enable the same 59 rules and all pass, so the result no longer depends on which ruff runs.
- The pre-commit `ruff --fix` hook (rev `v0.11.7`) produces an empty diff, so this creates no churn for contributors.
- The `uv-lock` pre-commit hook passes — the `pyproject.toml` edit does not stale `uv.lock`.

No source changes were needed, so there is no second commit; the workflow fix stands alone.

## Follow-up, not in this PR

Three ruff versions are still in play: `uv.lock` 0.9.4, pre-commit rev `v0.11.7`, CI 0.15.22. That is now harmless because the rule set is pinned in config rather than inherited, but they could be aligned if you want local and CI byte-for-byte identical.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4ea122ef5f5e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.