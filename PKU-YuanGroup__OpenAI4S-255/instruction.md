# Issue

**Title:** ci: move release and sandbox jobs to supported macOS runners

## Description

The release rehearsal cannot schedule its macOS sandbox gate because GitHub retired all macOS 14 runners on 2026-11-02. Run 42548338956 reports `The configuration 'macos-14-arm64-us-default' is not supported` before any step starts.

Use the supported `macos-15` arm64 runner for the CI sandbox job, release sandbox gate and optional DMG build. Publication settings, permissions, sandbox requirements and macOS signing policy are unchanged.

Official retirement notice: https://github.blog/changelog/2026-10-01-github-actions-macos-14-runner-image-retirement/

Validation: release gate, rehearsal and documentation checks passed locally. A new non-publishing release rehearsal will run after merge and green main CI.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `512b443786cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.