# Issue

**Title:** chore(ci): bound the playwright --with-deps install steps

## Description

## Summary

Give every `playwright install --with-deps` step in `ci.yml` its own `timeout-minutes`.

`playwright install --with-deps` runs `apt-get` with no timeout of its own. On PR #190 (CI run 36732175698, chromium), a stalled runner mirror hung "Install the server, scientific browser fixtures, and browser driver" from 14:52 until the job's 45-minute limit, so the job was reported cancelled before any browser test ran. With a step bound, a hung mirror fails well before the job limit, and the job can then be re-run.

Each bound is sized from the step's apt payload at the slowest healthy throughput seen, not from a peak step time: over the last 60 CI runs the same apt fetch ran anywhere from 70.9 kB/s to 10.9 MB/s. The 70.9 kB/s case is this PR's own first run, where Stage 0 fetched `34.9 MB in 8min 12s` and the step took 512s (a 15-run window had put its peak at 41s).

| Job | Step | apt payload | Worst healthy step (60 runs) | Step bound | Job bound |
| --- | --- | --- | --- | --- | --- |
| `browser-smoke` chromium / firefox | Install the server, scientific browser fixtures, and browser driver | ~35 MB / ~49 MB | 107s / 270s | 20 min | 45 min |
| `browser-smoke` webkit | same step | ~130 MB | 683s (~31 min at 70.9 kB/s) | 35 min | 45 min |
| `browser-stage0` | Install the browser driver | ~35 MB | 512s | 15 min | 25 min |
| `browser-team-mode` | Install the zero-dependency server and browser driver | ~35 MB | 229s | 15 min | 20 min |

The browser-smoke bound is one per-engine expression, `${{ matrix.engine == 'webkit' && 35 || 20 }}`. The rest of Stage 0 and team mode has never taken two minutes, so both bounds still fire well inside their job limits. `tests/test_ci_gate_independence.py` verifies every `playwright install --with-deps` step has a positive integer bound strictly below its job's. It accepts integer literals and the explicitly supported per-engine conditional, rejects unverified expression forms, and requires coverage of each of the three browser jobs even if another job contains duplicate installs.

## Area

- [x] Tests / harness / CI

## Change Type

- [x] Bug fix

## Verification

Validated with current `main` integrated into this branch:

- Full offline suite: `uv run pytest -n auto --maxprocesses=4 --dist loadfile` — **10,808 passed, 63 skipped** on macOS / Python 3.12.
- Focused CI, governance, release, platform, crosswalk, and container-deployment tests — passed.
- `pre-commit run --all-files` — passed, including mypy.
- `python scripts/check_directory_readmes.py` — complete bilingual coverage.
- `python -m harness.cli run --tier pr --offline` — all 38 scenarios passed.
- `python scripts/source_secret_scan.py` — passed.
- Added mutation regressions for invalid or unverified timeout values, both conditional branches reaching the job limit, and duplicate installs masking a missing browser job.

Linux [CI run 36989700658](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/36989700658) passed at `2a0ffbd400091bfc8139774eef97602c6d750a78`, including all four Python versions, all three browser engines, Stage 0, team mode, and both response-contract gates. Across all GitHub checks: **34 passed**, three nightly jobs were skipped, and Cursor Bugbot returned neutral because it failed to run. The separate Cursor security and approval checks passed.

## Risk and Reviewer Focus

The remaining risk is an install slower than the slowest healthy rate yet seen: webkit's 35-minute bound admits its ~130 MB at about 64 kB/s or faster, the 15-minute chromium bounds admit ~35 MB at about 42 kB/s or faster. Below that the step fails with a timeout rather than the job being cancelled, and a re-run applies. The step bound still does not retry a stalled mirror by itself.

## Checklist

### Diff Readiness

- [x] I reviewed and understand the full diff.
- [x] This PR is small and single-purpose.
- [x] No unrelated formatting, broad rewrite, or drive-by refactor is included.

### Tests

- [x] Relevant tests or manual checks were run and listed above.
- [x] No new test requires live LLM, network, GPU, SSH, Docker, lab hardware, or secrets in the default offline suite.
- [x] No tests were deleted without tracked replacements.

### Public Disclosure and Security

- [x] No secrets, API keys, tokens, real credentials, private data, model weights, or local absolute paths are included.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a0b9e105d9e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.