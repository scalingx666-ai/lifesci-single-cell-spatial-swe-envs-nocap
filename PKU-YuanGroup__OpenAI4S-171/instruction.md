# Issue

**Title:** fix(contributors): keep bilingual avatar inventories in sync

## Description

## Summary

Refreshing contributor avatars can add PNG files without updating `.github/contributors/README.md` and `README_zh.md`, causing the directory-documentation gate to fail. The manual inventory-update step was also noted in .

The generator now synchronizes both marked inventory tables from the surviving PNG filenames returned by the avatar refresh. A successful refresh preserves the existing filename spelling when login casing changes, avoiding case-variant duplicates on case-sensitive filesystems. Failed downloads retain existing current-contributor avatars.

Both inventory documents are read and their markers validated before authentication, fetching or writing. Missing or malformed inventories stop the run with a diagnostic and exit code 1. All four READMEs use the same block renderer and writer: every changed document is prepared in a sibling temporary file before any destination is replaced, preserving file permissions and surrounding prose.

Regression fixtures track existing avatars in Git and stage the refresh before running the real directory gate. The bilingual documentation explains that staging is required for the gate to stop listing deleted tracked avatars. The generator itself does not modify the Git index.

## Area and Change Type

- Tests / harness / CI; Docs
- Bug fix; Test / harness; Documentation

## Verification

```text
uv run --no-project --with pytest python -m pytest --noconftest tests/test_update_contributors.py -o addopts= -q
# 28 passed on ordinary Windows NTFS
uvx black --check scripts/update_contributors.py tests/test_update_contributors.py
uvx isort --check-only scripts/update_contributors.py tests/test_update_contributors.py
uvx ruff check scripts/update_contributors.py tests/test_update_contributors.py
git diff --check
```

- The same 28 tests also passed with pytest's temporary directory under a fresh NTFS directory with per-directory case sensitivity enabled. Distinct differently cased filenames were verified both in the parent directory and inside the successful-refresh fixture.
- The new `OSError` and `KeyboardInterrupt` regressions fail on `65e2063` because both root READMEs have already changed when the last inventory staging write fails. They pass with this change: all four originals remain byte-identical and temporary files are removed.
- Preflight tests cover missing, missing-end, reversed and duplicate markers in either language and assert that authentication/fetching is never reached. Refresh tests cover additions, tracked removals, failed downloads, successful and failed casing changes, exact on-disk filenames and repeat-run stability.
- Network and image conversion are stubbed; these are script tests using the real generator, Git enumeration and directory checker.
- After merging `main` at `a6955de` into the PR branch, the 28 contributor tests and the three release-documentation tests changed by the base update passed together: **31 passed**. `git diff --check origin/main...HEAD` also passed on the merged head (`4772ddb`).

Not run locally: the full offline suite, mypy, full-repository directory checks or `pre-commit run --all-files`. Local validation used a Windows sparse checkout and the focused tests bypass the project-wide `conftest.py`. Linux/macOS execution, live GitHub requests and Pillow conversion were not exercised. The CI and Protocol fuzzing workflows for the merged head currently report `action_required`; upstream execution results are not yet available.

## Risk and Reviewer Focus

Review the preflight ordering, preservation of existing avatar spelling and the single preparation batch for all four READMEs. The existing directory-documentation requirements remain in place.

A staging failure leaves every README unchanged. Each `os.replace` is atomic, but replacing multiple paths is not an all-or-nothing transaction: an interruption during the replacement loop can leave a mixture of old and new documents. Avatars are refreshed before document staging, so this is not a transactional rollback of the entire refresh. These limits are documented rather than described as whole-tree atomicity.

## Checklist

- [x] Reviewed the complete diff; changes are limited to this fix.
- [x] Added offline regression coverage without deleting existing tests.
- [x] Kept the affected English and Chinese documentation in sync.
- [x] Added no dependencies, credentials or private data.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a6955de46295`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.