# Issue

**Title:** Organize existing reference documentation by analysis task

## Description

The reference index mixes analysis tasks, plotting, data access and environment helpers at the same navigation level. Reorganize the existing main-branch documentation into 14 task-oriented sections and 62 subsections, keeping all 353 existing entries exactly once.

The index is English-only and starts directly at Overview and Workflows. A reference-index-only template omits the redundant page heading and keeps the sidebar at the primary-section level while preserving secondary headings in the body. ATAC and Multiome Analysis and Spatial Omics Analysis appear immediately before Genomic Variation and Trait Association.

Only APIs already present on main are included. The 11 additional interfaces from the open ATAC feature branches are intentionally excluded; no ATAC implementation, public API, version or example-execution policy changes are included.

Validation:
- Exact entry multiset comparison against main: 353 retained, zero omissions, zero duplicate assignments.
- Full local pkgdown reference build with examples = FALSE completed successfully. It emitted one R .Call stack-imbalance warning at completion; the final index rebuild and content/link validation passed.
- Rendered index checks: 14 sections, 62 secondary headings excluded from the sidebar, requested ordering, English-only content, no introductory page heading, and all local help links resolve.
- git diff --check passed. This documentation-only change does not rerun analysis tests or numerical examples.

Hosted checks for the new head are pending; local rendering is not a claim that all CI has passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bbc36068e591`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.