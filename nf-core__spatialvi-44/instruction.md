# Issue

**Title:** Cleanup custom download scripts

## Description

* The `download_probeset` process wasn't used anymore anyway
 * The `download_reference` can be replaced with the `untar` module from `nf-core/modules`, thereby reducing the amount of custom code required. 

In the future, it could be considered to support custom references with `spaceranger/mkgtf` and `spaceranger/mkref`, but I suppose 99% of use-cases are covered with prebuilt 10x references, and it is definitely not a priority for me. 

<!--
# nf-core/spatialtranscriptomics pull request

Many thanks for contributing to nf-core/spatialtranscriptomics!

Please fill in the appropriate checklist below (delete whatever is not relevant).
These are the most common things requested on pull requests (PRs).

Remember that PRs should be made against the dev branch, unless you're preparing a pipeline release.

Learn more about contributing: [CONTRIBUTING.md](https://github.com/nf-core/spatialtranscriptomics/tree/master/.github/CONTRIBUTING.md)
-->

## PR checklist

- [x] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/spatialtranscriptomics/tree/master/.github/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/spatialtranscriptomics _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [x] Make sure your code lints (`nf-core lint`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [x] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73604a1847db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.