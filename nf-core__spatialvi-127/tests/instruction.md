# Issue

**Title:** Replace `erikfas/spatialvi` with Seqera image

## Description

Replace the old `erikfas/spatialvi` Docker image with one created with Seqera containers instead. The old image was at one point required, partly due to issues with Quarto and Conda, partly due to problems with the required Python environment in general.

The old image also used a multi-stage build for Quarto, but the new Seqera image install Quarto using Conda instead, which now works.

This update does not change any versions of the environment itself, opting to stay with the exact versions of the old environment, even though more up to date packages are available. The newer versions should also be tested at some point.

<!--
# nf-core/spatialvi pull request

Many thanks for contributing to nf-core/spatialvi!

Please fill in the appropriate checklist below (delete whatever is not relevant).
These are the most common things requested on pull requests (PRs).

Remember that PRs should be made against the dev branch, unless you're preparing a pipeline release.

Learn more about contributing: [CONTRIBUTING.md](https://github.com/nf-core/spatialvi/tree/main/.github/CONTRIBUTING.md)
-->

## PR checklist

- [ ] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/spatialvi/tree/main/.github/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/spatialvi _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [ ] Make sure your code lints (`nf-core pipelines lint`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f7010ff491a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.