# Issue

**Title:** fix: remove contribution guide and check_r example gates

## Description

<!-- CURSOR_AGENT_PR_BODY_BEGIN -->
## Summary

- Delete top-level `CONTRIBUTING.md` and drop its `.Rbuildignore` entry.
- Replace the `check_r()` gates in the `RunBANKSY` and `GetSpatialResult` roxygen examples with `\dontrun` blocks that call `RunBANKSY`, `SpatialSpotPlot`, and `GetSpatialResult` directly. Data-prep lines stay outside `\dontrun`.
- Regenerate `man/RunBANKSY.Rd` and `man/GetSpatialResult.Rd` to match those examples. Implementation `check_r()` calls are unchanged.

## Test plan

- [ ] Confirm `CONTRIBUTING.md` is gone and `.Rbuildignore` has no `CONTRIBUTING` pattern.
- [ ] Confirm neither `RunBANKSY` nor `GetSpatialResult` examples contain `check_r`, and both use `\dontrun`.
- [ ] Confirm `R/RunBANKSY.R` still calls `check_r()` in the function body.
<!-- CURSOR_AGENT_PR_BODY_END -->

<div><a href="https://cursor.com/agents/bc-8cfa04fa-e41c-5cc8-a32c-f86d4755b1f8?cursor_ref=pr_footer&cursor_cta=open_in_web"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-web-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-web-light.png"><img alt="Open in Web" width="114" height="28" src="https://cursor.com/assets/images/open-in-web-dark.png"></picture></a>&nbsp;<a href="https://cursor.com/background-agent?bcId=bc-8cfa04fa-e41c-5cc8-a32c-f86d4755b1f8&cursor_ref=pr_footer&cursor_cta=open_in_cursor"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-cursor-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-cursor-light.png"><img alt="Open in Cursor" width="131" height="28" src="https://cursor.com/assets/images/open-in-cursor-dark.png"></picture></a>&nbsp;</div>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `de079174f713`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.