# Issue

**Title:** docs: clarify six full-input workflows and article navigation

## Description

## Summary

- Reorganize the article navigation around starting with data, comparing batches and transferring labels, interpreting cell states, and extending spatial analyses. All 12 article names remain represented exactly once.
- Make the single-cell, annotation, integration, integration-benchmark, spatial-framework bridge, and spatial-platform articles follow explicit input, analysis, interpretation, export, and reload steps.
- Keep the complete bundled inputs: 1,000 pancreas cells; 1,600 integration cells; 200 annotation query cells plus 1,400 reference cells; and 1,986 spatial spots by 5,000 genes.
- Record dependency preflights, source/session provenance, completed versus optional `not_run` stages, and preservation assertions. Integration uses the documented official Harmony revision `df19af23ae0639bd6ea2da63898f973f08c85862`.

## Scope

The documentation commit is based directly on upstream main `79148fe2e25ed681bbf0f91e00460dda9741765a`. The diff contains `_pkgdown.yml`, the six article sources above, and one small `.github/workflows/articles.yaml` follow-up: request the exact official Harmony GitHub revision in the existing dependency-install step, then verify `RemoteUsername` and `RemoteSha` before building. No implementation, analysis algorithm, Python setup, RunSpatialDM help, or PR #486 changes are included.

## Validation

- All six article sources completed standalone HTML renders in separate fresh R processes using the prepared R 4.5.0 / SCOP 0.9.2 environment.
- The rendered source MD5 values match the six files in this PR exactly.
- CSV/RDS exports and reload/preservation assertions completed. Figures were visually inspected, including the corrected integration-panel overlap.
- Git whitespace checks and static named-argument checks passed. The remote tree matches the isolated local tree; the follow-up changes only `articles.yaml` (13 added lines, 1 removed).
- Both integration articles also completed real `pkgdown::build_article()` builds from the isolated PR source, with all 1,600 cells and export/reload assertions. Harmony was installed from the exact official SHA into a fresh dedicated library using `remotes::install_github`; the actual loaded-library path and provenance fields were verified. Other R dependencies came from the prepared environment.

## Validation limits

- The original six standalone renders used an existing prepared environment, not a clean dependency installation or a full hosted pkgdown build. The source files are byte-identical after isolation from the working checkout. Separate trajectory changes in that earlier checkout are excluded from this PR and are not invoked by these six articles.
- The two additional integration pkgdown builds used a fresh Harmony library plus prepared other R dependencies. This is not a full clean-OS/environment rebuild. The workflow's explicit GitHub package reference was checked against the official setup-r-dependencies/pak contract; the local pak probe was interrupted after no progress and is not used as success evidence, so these results do not claim an end-to-end run of the GitHub action. Non-blocking missing-alt-text warnings remain.
- Optional Giotto/vendor-method recipes are explicitly reported as `not_run`; they are not claimed as validated backend executions.
- The installed Harmony package must come from the documented official GitHub revision. A CRAN-origin Harmony package does not satisfy SCOP's source check and can trigger an implicit install; the article preflight stops before that.
- The existing articles workflow has no pull-request trigger. PR package/reference CI does not establish that the full article suite or hosted article deployment passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `79148fe2e25e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.