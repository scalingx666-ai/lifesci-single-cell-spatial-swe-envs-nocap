# Issue

**Title:** Refine reference navigation into 17 task-oriented modules

## Description

Reorganize the existing reference index into the 17 requested task-oriented modules. Separate phenotype/perturbation analysis from differential expression and composition, and split the previous utilities catch-all into visualization, data/object management, and resources/environment.

The six crowded areas now have explicit task boundaries. Integration has workflow, backend-family, mapping and evaluation groups; communication separates general inference, spatial communication, signaling activity, resources and plots; spatial sections follow QC, deconvolution, domains, features, neighborhoods and integration. Method-specific plots sit next to their analyses. RunCSIDE is classified with spatial feature analysis, and Cell2fate remains with velocity.

All 353 existing reference entries have exactly one primary assignment. There are 17 primary sections and 67 subsections; the largest subsection has nine entries. Six two-entry sections represent independent tasks (multiomic regulatory networks, existing ATAC QC/coverage, spatial maps, CNV, GWAS and SCExplorer). Unmerged ATAC interfaces are not introduced by this documentation-only commit.

Validation: exact multiset coverage, zero omissions/duplicates, full local pkgdown reference rendering with examples disabled, English-only headings, preserved index template, and diff whitespace checks. The renderer completed with its existing R .Call stack-imbalance warning; rendered structure and topic links are checked separately. No R implementations, public interfaces, package version or example-execution policy are changed.

Current-head CI must complete before merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `483e2e569e59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.