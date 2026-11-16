# Issue

**Title:** fix(release): install uv in the windows-package job before its receipt step

## Description

## Summary

The v0.2.0 `pypi_only` dispatch ([run 32831018097](https://github.com/PKU-YuanGroup/OpenAI4S/actions/runs/32831018097)) failed in **Build the Windows package**: its receipt step runs `uv run --locked`, and `windows-package` was the only uv-calling job in `release.yml` with no `setup-uv` step — invisible for as long as the pipeline was unreachable, fatal on the first complete dispatch. Everything before it (guard in the new pypi_only mode, freeze, quality, build, linux-app, macos-app) succeeded, and `!failure()` correctly blocked `pypi`.

One step added: the same pinned `astral-sh/setup-uv` the `linux-app` job uses, placed before the build/receipt steps.

After merging: re-dispatch `release.yml` with `tag=v0.2.0`, `pypi_only=true`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ff442cdc1a5a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.