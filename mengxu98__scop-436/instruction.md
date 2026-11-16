# Issue

**Title:** fix: Codex leftovers from #435 (Statial dontrun, UMAP2 spread formals)

## Description

<!-- CURSOR_AGENT_PR_BODY_BEGIN -->
Fixes remaining actionable Codex review findings that landed on `main` with merged PR #435 (merge commit `a4d8257de32c0835abe524b7ed9dca855e6a9d28`).

## Context

Codex reviewed #435 and left four P1/P2 comments. Two were already addressed on the merge (and are **not** re-changed here):

- `R/DataConvert.R`: `adata_to_srt` / `srt_to_adata` already gate `PrepareEnv` with `isTRUE(prepare_env)`.
- `R/RunSCENIC.R` `cistarget2()` already normalizes NULL `cores` to `r_workers <- 1L` before the PSOCK worker-state guard.

This PR picks up the two leftovers.

## Changes

### P1 — Keep the Statial example guarded (`R/RunStatialKontextual.R`)

`#435` removed `\\dontrun{}` so `RunStatialKontextual()` / `StatialKontextualPlot()` ran unconditionally. `Statial` is an optional backend (not in Imports or Suggests). The executable example body is wrapped in `\\dontrun{...}` again so clean/offline `R CMD check` / `example()` does not require Statial. No `if` / `requireNamespace` / `check_r` in the example.

### P2 — Append `spread` without shifting positional args (`R/RunUMAP2.R`)

`spread` had been inserted between `min.dist` and `set.op.mix.ratio`, which silently shifted positional callers of `set.op.mix.ratio` and later formals. `spread` is now appended after the existing formals (`seed.use`) on both the Seurat and default methods. Named-arg behavior is unchanged. `n_threads` remains a deprecated alias for `cores`.

A small test asserts the restored formal order.

`man/` is updated to match (`roxygen2::roxygenise()`).

## Out of scope

- Does not touch draft PR #434 or unrelated files.
- Does not re-change DataConvert / RunSCENIC paths Codex already saw as outdated.

<!-- CURSOR_AGENT_PR_BODY_END -->

<div><a href="https://cursor.com/agents/bc-7eaff473-0067-5145-9edc-a75074dea57e?cursor_ref=pr_footer&cursor_cta=open_in_web"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-web-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-web-light.png"><img alt="Open in Web" width="114" height="28" src="https://cursor.com/assets/images/open-in-web-dark.png"></picture></a>&nbsp;<a href="https://cursor.com/background-agent?bcId=bc-7eaff473-0067-5145-9edc-a75074dea57e&cursor_ref=pr_footer&cursor_cta=open_in_cursor"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-cursor-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-cursor-light.png"><img alt="Open in Cursor" width="131" height="28" src="https://cursor.com/assets/images/open-in-cursor-dark.png"></picture></a>&nbsp;</div>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a4d8257de32c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.