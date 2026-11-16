# Issue

**Title:** docs: expand RunCell2fate examples with workflow and plots

## Description

<!-- CURSOR_AGENT_PR_BODY_BEGIN -->
`RunCell2fate()` documentation examples now match the actual workflow:

- call `RunStandardWorkflow()` first so `FeatureDimPlot()` has a reduction (`pancreas_sub` has none)
- plot time, time uncertainty, module activation, and module state
- `env_requirements()` shows the standalone Cell2fate Python 3.9 stack

No function behavior changes. `test-cell2fate.R`: 77 passed. Examples still `\dontrun` because they need the isolated Python environment.
<!-- CURSOR_AGENT_PR_BODY_END -->

<div><a href="https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503?cursor_ref=pr_footer&cursor_cta=open_in_web"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-web-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-web-light.png"><img alt="Open in Web" width="114" height="28" src="https://cursor.com/assets/images/open-in-web-dark.png"></picture></a>&nbsp;<a href="https://cursor.com/background-agent?bcId=bc-01a00f3d-19cd-7d32-b63e-ce70fd657503&cursor_ref=pr_footer&cursor_cta=open_in_cursor"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-cursor-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-cursor-light.png"><img alt="Open in Cursor" width="131" height="28" src="https://cursor.com/assets/images/open-in-cursor-dark.png"></picture></a>&nbsp;</div>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2265c19c2553`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.