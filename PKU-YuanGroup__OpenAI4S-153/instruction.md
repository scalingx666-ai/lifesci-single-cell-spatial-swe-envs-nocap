# Issue

**Title:** chore(deps): update Python image, formatting hooks, and CodeQL action

## Description

## Summary

Update the container and development/CI dependencies together. This PR supersedes #148, #149, and #150.

| Dependency | Previous | Updated |
| --- | --- | --- |
| Python 3.14 slim-bookworm image, both stages | `416f0db…` | `9ab8d9c…` |
| isort | 8.0.1 | 9.0.1 |
| Ruff | 0.16.4 | 0.16.6 |
| CodeQL SARIF upload action | 4.37.8 | 4.37.9 |

The isort upgrade requires import formatting in five Python files. It also exposes an isort/Black loop on two commented alias imports: shorten the worker's inline comments while preserving the trusted-path explanation, and apply a documented, single-import `isort: skip` in the scenario test. All five Python files retain identical ASTs. Frozen dependency identities, the existing E/F lint rule selection, and the Python 3.10 formatting target remain intact.

## Area and Change Type

- [x] CLI / config / packaging
- [x] Tests / harness / CI
- [x] Dependency maintenance and formatter compatibility fix

## Verification

Passed locally:

```text
uv sync --locked
uv run --offline --no-sync pytest -n auto --maxprocesses=4 --dist loadfile
uv run pre-commit run --all-files
uv run mypy
uv run python -m harness.cli run --tier pr --offline
uv run python scripts/check_directory_readmes.py
uv run python scripts/capture_response_contract.py --check
uv run python scripts/source_secret_scan.py
git diff --check origin/main...HEAD
```

Full offline suite: **8,494 passed, 50 skipped, 2 warnings** on Python 3.13.13 (481.99 seconds).

The harness passed all 38 scenarios; the route contract matched all 212 routes. The complete pre-commit gate passed after the compatibility fixes, and the commit hooks passed again. A stdlib AST comparison confirmed no executable change in any of the five Python files.

`bash scripts/container_smoke.sh` was attempted but its preflight stopped because Docker is unavailable on this host. Container runtime, Linux sandbox, browser, and the other Python-version jobs are delegated to this PR's CI; their results are separate from the local checks. A real SARIF upload runs only on the Scorecard workflow's configured triggers.

## Risk and Reviewer Focus

Review `Dockerfile`, `.pre-commit-config.yaml`, `.github/workflows/scorecard.yml`, and the comment-placement changes in `openai4s/kernel/worker.py` and `tests/test_retrosynthesis_scenario_protocols.py`.

Two independent reviews verified the official image digest, unchanged Python series and architecture coverage, the exact upstream hook/action tag-to-SHA mappings, and isort/Ruff compatibility. The formatter loop found during review is fixed. No unresolved actionable findings remain in the reviewed diff. This review does not substitute for the repository's required code-owner approval before merge.

## Checklist

- [x] Full diff reviewed; scope is the requested consolidated dependency update and necessary formatting compatibility.
- [x] No unrelated formatting or broad rewrite. Worker and Store facade edits are limited to imports/comments.
- [x] No frontend source/dist change; vendored assets and captured fixtures were not reformatted.
- [x] Full offline suite and lint run; existing kernel, agent, and gateway tests are included in the suite.
- [x] No tests deleted and no live-resource tests or credentials added.
- [x] No hard third-party core imports or runtime dependencies added.
- [x] No secrets, private data, local paths, or unpublished research information added.
- [x] Documentation and translated behavior claims remain accurate; no user-facing API or security guarantee changed.

## Review follow-up (4 commits)

A max-effort review of the diff found one real defect in the compatibility fix and three structural gaps the bump exposed.

**`6df4911a` — the `isort: skip` workaround was wrong in three ways.**
`# noqa: E402; isort: skip` is not a directive ruff can parse: the `;` makes it reject the whole thing, so it suppressed nothing and printed `warning: Invalid # noqa directive` on every cold-cache run — the only invalid noqa in the tree. It is not merely inert: with the code selected and `--fix` on, ruff *deletes* the line, and `ruff-check` runs with `--fix` and tree-wide write access. Beyond the spelling, `isort: skip` created a section boundary (an appended `import zlib` was pinned under the third-party group at line 82 and `isort --check-only` still exited 0) and only held under isort 9 (isort 8 moved the statement below `yield_benchmark`, out of sorted order — reachable by reverting `657ea805` alone, or from a warm hook cache).

Fixed by dropping the trailing comment rather than re-spelling the directive: the statement then collapses to 84 characters and both formatters leave it alone. No suppression is lost — ruff exempts imports following a `sys.path` mutation, so the file is clean with `--select E402`. Verified byte-stable over four isort→black round-trips under isort 9.0.1 **and** 8.0.1.

**`ab7e94fa` — `[tool.isort]`.** `[tool.black]` and `[tool.ruff.lint]` each argue that a formatter's behaviour must be stated, not inherited; isort was the one of the three with no such block, and this is its *major* bump. `src_paths` defaults to `(cwd/"src", cwd)`, so first-party detection was a property of the process:

```
with the block, cwd=repo root ....   0 of 883 files reported unsorted
with the block, cwd=elsewhere ...    0
without,        cwd=repo root ....   0
without,        cwd=elsewhere ...  317   <- `openai4s` demoted to third-party
```

Zero output change, per the precedent that block records.

**`f857e7d8` — dependabot.** `hook-versions` excluded black because "a black bump is a style change that has to be read on its own, not merged as one row of a version table". isort has the same property; it was not excluded, which is how a major arrived batched with a ruff patch.

**`76a53cf9` — corrections to the above.** A sweep pass found the new comments' *explanations* wrong even where the code was right: the formatter trigger is not length alone (with `combine_as_imports` off, only *aliased* imports are collapsed — isolated with two imports of identical 81-character bodies), the two files are not symmetric (the kernel worker's suppressions **are** load-bearing, because its insert sits inside an `if`; the test's are inert), and `[tool.isort]` overclaimed that a bare `isort .` "agrees with the gate" — it still rewrites 318 of 408 pinned `skills/bioskills/` files. One disputed claim was re-measured and stands: the oscillation is unbounded, not a one-pass convergence (six rounds, `isort→b317cd8aabca`, `black→31dc7b2429e1`, never equal).

### Re-verified after the fixes

`pre-commit run --all-files` passes with no file modified · `uv run mypy` · full offline suite **8,494 passed, 50 skipped** · `harness.cli --tier pr --offline` 38/38 · `capture_response_contract.py --check` 212/212 · `check_directory_readmes.py` · `source_secret_scan.py` · 0 invalid-noqa warnings across all 883 checked files · all five reformatted files still AST-identical to `origin/main`.

### Reported, deliberately not applied

`base-image`'s `update-types` filter never matches a digest-only Docker update (proven by `7f45a740`'s trailers, which carry no `update-type:` and no `dependency-group:`) — but the fix is a product decision, since a single docker dependency cannot be batched down. Nothing verifies a `# frozen:` comment against its SHA, nor that the Dockerfile digest belongs to the tag beside it (Docker ignores the tag when a digest is present); `combine_as_imports` would remove 113 duplicated module paths across 63 files but rewrites 67. All are inline comments on the PR.

<!-- CURSOR_SUMMARY -->
---

> [!NOTE]
> **Low Risk**
> Pin bumps and import formatting only; kernel and store edits are comment/import layout with identical AST per PR verification.
>
> **Overview**
> Consolidates dependency maintenance: **Python 3.14 slim-bookworm** digest updates in both **Dockerfile** stages, **isort 9.0.1** and **Ruff 0.16.6** frozen SHAs in **`.pre-commit-config.yaml`**, and **CodeQL `upload-sarif` v4.37.9** in the Scorecard workflow.
>
> **isort 9** only changes how imports are written in five Python files (collapsed multi-line `from … import` blocks). **`worker.py`** keeps the trusted-path comment with shorter `# noqa: E402` lines; **`test_retrosynthesis_scenario_protocols.py`** adds an **`isort: skip`** on one late import to stop an isort/Black reorder loop. No runtime or API behavior is intended to change.
>
> <sup>Reviewed by [Cursor Bugbot](https://cursor.com/bugbot) for commit f8fa1b6bfc6630a12544f884de6b169830950a4b. Configure [here](https://www.cursor.com/dashboard/bugbot).</sup>
<!-- /CURSOR_SUMMARY -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `22546caf438c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.