# Issue

**Title:** fix: preserve the Playwright cache in isolated release smoke

## Description

The non-publishing release rehearsal built the Linux bundle, then failed its installed-runtime browser check because Chromium was installed under the runner's HOME while the smoke deliberately uses a fresh HOME ([failed job](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/42552196348/job/128965552389)). The browser process also dropped an explicitly configured Playwright cache path.

Set one job-scoped `PLAYWRIGHT_BROWSERS_PATH` in Playwright’s hermetic installation directory (`0`) for installation and execution, and pass that setting through the browser subprocess allowlist. HOME/data-directory isolation, credential filtering, runtime checks and browser assertions stay in place. This follows [Playwright's documented shared-cache configuration](https://playwright.dev/docs/browsers#managing-browser-binaries).

Validation: 406 tests passed, 3 skipped across installed-runtime smoke, release gates, rehearsal and pipeline tests. The new regression covers both an explicit path containing spaces and the hermetic `0` setting, and checks that HOME remains isolated and caller hooks/credentials remain excluded. Black, isort, Ruff and diff checks passed. The full release rehearsal will be repeated after the merged commit's CI passes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a54446b41a75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.