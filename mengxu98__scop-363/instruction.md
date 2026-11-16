# Issue

**Title:** feat: multi-TF SCENIC network hubs without titles

## Description

<!-- CURSOR_AGENT_PR_BODY_BEGIN -->
`plot_type = "network"` can take several TFs in one figure: one hub per TF (`star` for a single TF, `hub` for several) instead of split panels.

`network`, `network_graph`, and `egrn` no longer add plot titles or subtitles. Cell type still appears in the multi-TF legend as `TF (top cell type)`.

`tests/testthat/test-scenic-plot.R`: 107 passed, 0 warnings.
<!-- CURSOR_AGENT_PR_BODY_END -->

<div><a href="https://cursor.com/agents/bc-01a00f3d-19cd-7d32-b63e-ce70fd657503?cursor_ref=pr_footer&cursor_cta=open_in_web"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-web-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-web-light.png"><img alt="Open in Web" width="114" height="28" src="https://cursor.com/assets/images/open-in-web-dark.png"></picture></a>&nbsp;<a href="https://cursor.com/background-agent?bcId=bc-01a00f3d-19cd-7d32-b63e-ce70fd657503&cursor_ref=pr_footer&cursor_cta=open_in_cursor"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-cursor-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-cursor-light.png"><img alt="Open in Cursor" width="131" height="28" src="https://cursor.com/assets/images/open-in-cursor-dark.png"></picture></a>&nbsp;</div>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f50c60044256`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.