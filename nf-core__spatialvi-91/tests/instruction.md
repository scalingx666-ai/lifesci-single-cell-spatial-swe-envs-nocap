# Issue

**Title:** Use spatialdata_io.experimental.to_legacy_anndata

## Description

Replace the internal `to_legacy_anndata` by `spatialdata_io.experimental.to_legacy_anndata` and update to latest `spatialdata`, `spatialdata-io` and `spatialadata-plot` versions.

## PR checklist

- [ ] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/spatialvi/tree/master/.github/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/spatialvi _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [ ] Make sure your code lints (`nf-core lint`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aa3472a7990a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.