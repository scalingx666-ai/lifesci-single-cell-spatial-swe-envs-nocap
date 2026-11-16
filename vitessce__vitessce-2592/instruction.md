# Issue

**Title:** NickAkhmetov/Update and optimize GitHub Actions workflows

## Description

#### Background

The GitHub Actions workflows had drifted well behind upstream: every action in use was at least one major version old (`actions/checkout@v4` against v7, `cypress-io/github-action@v4` against v7, and so on), and nothing was watching for that, so the drift would have keptaccumulating.

Auditing the workflows to fix the versions surfaced several cost and reliability problems alongside the stale pins:

- **No dependency caching anywhere.** All nine job-runs per pull request did a cold `pnpm install` of the full monorepo. `pnpm/action-setup` only gained a `cache` input in v5, so the version drift was what blocked the fix.
- **`build:ci` ran eight times per pull request.** It is `pnpm -r --workspace-concurrency 1 build`, deliberately serialized to stay inside the memory ceiling described in `scripts/set-node-options.sh`, and six jobs rebuilt identical output from the same commit.
- **A macOS runner doing nothing that needed macOS.** `test-e2e-playwright-for-create-view-cli` ran on `macos-latest` under a comment about golden screenshots, but `sites/demo/playwright/create-view/` contains no `toHaveScreenshot` call and no snapshot directory. Only `auto-init-coordination/` has goldens, and those are `*-chromium-darwin.png`. macOS runner minutes bill at 10x Linux.
- **No `concurrency` groups.** Three quick pushes to a branch meant 24 job-runs with 21 of them obsolete and none cancelled.
- **No `timeout-minutes` on any job**, so a hung Cypress or Playwright run could hold a runner for the 360-minute default.
- **Playwright browsers re-downloaded on every run**, three times per pull request.
- **ESLint running twice per pull request**, including on the Windows leg where results cannot differ and minutes cost double.

`release.yml` is also the workflow that publishes to NPM via OIDC, and it referenced every action by mutable tag. A compromised tag on any one of them is an NPM supply-chain compromise.

#### Change List

**Action versions**

- Upgraded across all three workflows: `actions/checkout` v4 → v7, `actions/setup-node` v4 → v7, `pnpm/action-setup` v4 → v6, `cypress-io/github-action` v4 → v7, `preactjs/compressed-size-action` 2.6.0 → 2.10.0, `softprops/action-gh-release` v2 → v3, `aws-actions/configure-aws-credentials` v4 → v6.
- Added `actions/upload-artifact@v7`, `actions/download-artifact@v8`, and `actions/cache@v6`.
- **`changesets/action` deliberately stays on v1**, now pinned to v1.9.0. v2 requires `@changesets/cli` v3 and validates the CLI version at runtime, refusing to run against the v2 CLI this repo uses (2.26.1). Upgrading it requires bumping `@changesets/cli` to v3 first, plus the v2 input renames (`version` → `version-script`, `publish` → `publish-script`, `title` → `pr-title`) and setting `create-github-releases: false` so it does not duplicate the existing `softprops/action-gh-release` step. That belongs in its own pull request; the blocker is recorded in a comment above the pin.

**Caching**

- `cache: true` on every `pnpm/action-setup@v6` invocation, keyed on `pnpm-lock.yaml`.
- Playwright browser binaries cached via `actions/cache@v6` with an OS-aware path (`~/Library/Caches/ms-playwright` on macOS, `~/.cache/ms-playwright` on Linux), keyed on `pnpm-lock.yaml`. On a cache hit the job runs `playwright install-deps` rather than `install --with-deps`, because the OS-level libraries the browsers link against are not part of that cache and still have to be installed each run.

**Shared build**

- New `build` job runs `build:ci` once, tars the `dist` and `dist-tsc` trees across `packages/` and `examples/`, and uploads them as a single artifact with `retention-days: 1`. Measured locally: 107 directories, ~3200 files, 326 MB, compressing to roughly 73 MB. Packed as one entry because several thousand individual files upload far more slowly, and left uncompressed so that `upload-artifact`'s own zip is the only compression pass.
- `test-e2e-demo`, `test-e2e-html`, `test-e2e-playwright`, and `test-e2e-playwright-react-19` now declare `needs: build` and unpack that artifact instead of rebuilding.
- Two jobs intentionally still build their own copy, commented in place: `test-unit`, whose purpose is to prove the build works on each OS, and `test-e2e-playwright-for-create-view-cli`, which scaffolds a new package with the create-view CLI before building and therefore needs the modified workspace rather than the shared output.

**Cost and reliability**

- `concurrency` with `cancel-in-progress` on `test.yml` and `bundle-size.yml`. Not added to `release.yml`, where cancelling mid-publish would be harmful.
- `test-e2e-playwright-for-create-view-cli` moved from `macos-latest` to `ubuntu-latest`. The comment on `test-e2e-playwright` now records why that job is the one that genuinely needs macOS.
- `timeout-minutes` on every job (30 for the e2e jobs, 45 for builds, 90 for release).
- `windows-2022` replaced with `windows-latest`; the hard pin was holding the matrix on an image heading for deprecation.
- ESLint now runs on one matrix leg only. `scripts/test.sh` gained a `SKIP_LINT` guard, which `test.yml` sets on the Windows leg.

**Security**

- Every action in `release.yml` pinned to a full commit SHA with a trailing `# vX.Y.Z` comment, so the publishing path cannot be changed by moving a tag.
- Explicit `permissions: contents: read` at the top of `test.yml` and `bundle-size.yml`, with `pull-requests: write` granted only to the two jobs that post comments.

**Maintenance**

- Added `.github/dependabot.yml` with a weekly `github-actions` update schedule, grouped into a single pull request. Dependabot rewrites both the SHA and the version comment on the pinned entries, so this is what stops the drift from recurring.

**Notes for review**

- Node version is still unpinned in `test.yml` and `bundle-size.yml` — only `release.yml` pins 24.15.0, so CI tests on whatever the runner image ships. Left unchanged here to avoid folding a behavior change into an infrastructure pull request, but worth a follow-up.
- The checkout / pnpm-setup / cache block is now repeated across eight jobs. A composite action under `.github/actions/` would collapse it; deferred to keep this diff reviewable.

#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a5df93105e32`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.