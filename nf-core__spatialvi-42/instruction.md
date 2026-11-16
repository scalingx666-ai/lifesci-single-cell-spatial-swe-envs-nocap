# Issue

**Title:** Add tests with nf-test

## Description

<!--
# nf-core/spatialtranscriptomics pull request

Many thanks for contributing to nf-core/spatialtranscriptomics!

Please fill in the appropriate checklist below (delete whatever is not relevant).
These are the most common things requested on pull requests (PRs).

Remember that PRs should be made against the dev branch, unless you're preparing a pipeline release.

Learn more about contributing: [CONTRIBUTING.md](https://github.com/nf-core/spatialtranscriptomics/tree/master/.github/CONTRIBUTING.md)
-->

Close #36 

## PR checklist

- [x] This comment contains a description of changes (with reason).
- [x] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/spatialtranscriptomics/tree/master/.github/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/spatialtranscriptomics _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [x] Make sure your code lints (`nf-core lint`).
- [x] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [x] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).

This PR adds nf-test as a general testing framework. The aim is not to cover everything yet, but to setup CI and add some basic test cases to build upon. 

Tests based on nf-test are quite a new concept as a whole. They are not part of the template yet, but I basically followed what has been done in

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `761a2bcffb34`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.