# Issue

**Title:** ✨ feat: Added ability to use .tar files instead of just .tar.gz files…

## Description

<!--
# nf-core/spatialvi pull request

Many thanks for contributing to nf-core/spatialvi!

Please fill in the appropriate checklist below (delete whatever is not relevant).
These are the most common things requested on pull requests (PRs).

Remember that PRs should be made against the dev branch, unless you're preparing a pipeline release.

Learn more about contributing: [CONTRIBUTING.md](https://github.com/nf-core/spatialvi/tree/main/.github/CONTRIBUTING.md)
-->

# Summary

 This change improves pipeline usability by accepting both compressed and uncompressed tar archives without breaking existing functionality. 10x Genomics hosts a lot of their VISIUM HD data in `.tar` format and this PR will unlock the ability to use these https hosted files directly. Users can now provide FASTQ files in either .tar or .tar.gz format.

  - Extended pipeline support from .tar.gz files to include both .tar and .tar.gz formats for FASTQ input files (which is already supported by UNTAR)
  - Updated documentation to reflect the expanded tar format support with examples

  🤖 Generated with https://claude.ai/code

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `729c2c1eb39d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.