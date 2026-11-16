# Issue

**Title:** Fix native ATAC feature ranking across batches

## Description

Chromatin feature selection broke equal batch-frequency ties by peak ID. Preserve native within-batch feature ranking while retaining the feature cap and intersection threshold.

## Integration and review scope

This is an independently reviewable component already contained in . Review #511 for the complete combined workflow, final WNN repairs and executable documentation. Merge either the combined branch or a deliberately selected component sequence; do not cherry-pick these commits again onto #511. No PR was merged by this organization pass.

The component head is `2e929e0bd742571d14aa77464763acef3f07b8a5` (rechecked 2026-10-16). Current-head hosted checks are pending or not yet all successful; consult the checks panel for the exact result. Descriptions do not substitute previous-head checks for the current revision. All components were synchronized with upstream main at 1b2489cf and the development-loading repair in #513; both startup fixes and their release notes are retained. The workflow-only GSL dependency repair is in #510.

## Validation and documentation

The combined implementation was audited against the [current scop-development skill](https://github.com/hurry060215-tech/scop-development-skill/blob/ce71a6209cab213189aa537fdce348df16ab6fdf/scop-development/SKILL.md). Its Windows acceptance environment ran 1,966 ATAC/related assertions before the startup synchronization, with zero failures/errors, six warnings and four explicit skips. The final combined source then passed 37 WNN/startup assertions with zero failures/errors/skips and three synthetic-assay warnings. Thirteen small help examples executed, covering the small standalone ATAC interfaces listed in #511; the external MACS2 example remains protected. The paired-WNN article executes 80 packaged cells, while the three external-data articles explicitly render without executing their resource-heavy recipes.

These are combined-tree results, not separate test runs on every component head. Current combined-head package-check and hosted-CI status are tracked in #511; its new commit is `07c4147836aed27c6892108b2657bd06c595863a`. Existing native comparisons and chromosome-scoped real-data acceptance are summarized there with their limits.

## Interpretation and limits

This changes feature selection, not the downstream statistical model. The existing small public example and rank regressions remain in scope.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `483e2e569e59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.