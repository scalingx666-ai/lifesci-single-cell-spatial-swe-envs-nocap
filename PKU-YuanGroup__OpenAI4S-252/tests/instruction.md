# Issue

**Title:** fix(deps): update advisory floors and preserve Python 3.10 CI

## Description

## Summary

Updates the locked Python and frontend dependencies from #245 to the advisory floors enforced by the governance tests. Keeps the stdlib-only core on Python 3.10, while matplotlib, RDKit, and pre-commit require Python 3.11+.

Fixes the Python 3.10 CI regression: only the ADMET example-rendering test skips when matplotlib is unavailable; non-plotting ADMET coverage remains active. Contributor documentation now states the tooling floor, and setup reports a missing pre-commit hook instead of silently ignoring it.

Supersedes #245 on a policy-compliant `fix/` branch. Its original commit `6277816bb310050066d681ec15ceb047e59b32e0` is preserved, with current main merged before validation.

## Verification

Passed locally at `d1c441fd`:
- Full offline suite, Python 3.12: **12,256 passed, 43 skipped**.
- Focused ADMET, governance, container, independent-CI, and setup contracts on Python 3.10 and 3.12. The original Python 3.10 ADMET failure was reproduced before the fix.
- `npm test --prefix frontend`: **1,904 passed**.
- `npm run build --prefix frontend`: committed dist unchanged.
- `uv run pre-commit run --all-files`, including strict mypy.
- `uv build` and `scripts/verify_release_artifacts.py`.
- Bilingual directory documentation, source credential scan, and **38** offline PR harness scenarios.
- `node tests/browser_smoke.mjs` against a disposable daemon, including real figure/artifact capture.
- Shell syntax and setup success/failure behavior for hook installation.
- Root and frontend npm audits: zero vulnerabilities reported.

Hosted validation: [CI run](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/42437959856): **all 26 PR jobs passed**; three nightly-only jobs were skipped by design. This includes the full Linux Python 3.10/3.12/3.13/3.14 suites, frozen response shapes, three browser engines, container smoke, and Linux sandbox boundaries. Protocol fuzzing and CodeQL also passed.

Local Python 3.10 limitation: the full macOS run finished with **12,230 passed, 66 skipped, 3 failed**. All three failures are BioProBench tests importing SciPy 1.15.3's native PROPACK library, rejected by the macOS loader with `__DATA/__thread_bss` offset validation. A standalone `import scipy.sparse` reproduces the error. The SciPy wheel URLs/hashes, NumPy lock entries, and BioProBench source/tests are unchanged from main. The hosted Linux Python 3.10 suite passes.

A local independent review found the plotting-test regression, now fixed. GitHub's hosted Cursor Bugbot returned a neutral check because its usage limit was reached; no successful hosted Bugbot review is claimed.

## Risk and Reviewer Focus

Python 3.10 retains the core and numeric science packages, but no longer installs matplotlib, RDKit, or pre-commit. Review the dependency markers, security-floor constraints, and container lock export together.

## Checklist

- [x] Full diff reviewed; no unrelated refactor or formatting.
- [x] Core remains zero-dependency; compatibility facades were not changed.
- [x] Frontend dist rebuilt and unchanged; vendored assets and fixtures not reformatted.
- [x] No tests deleted; default tests require no live services or secrets.
- [x] English and Chinese documentation agree with behavior.
- [x] No secrets, private data, or local absolute paths included.
- [x] Full Python 3.12 offline suite and required hosted checks pass; local Python 3.10 limitation is recorded above.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7155c80c4ef6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.