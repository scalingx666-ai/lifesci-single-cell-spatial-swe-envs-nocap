# Issue

**Title:** Handle case where fastq_dir is a symlink

## Description

Fixes issue #124 , checking if for a non-null/"file" scheme before attempting to resolve symlinks to avoid breaking cloud storage paths as supported in PR #122.

I manually tested (using `--profile singularity`) the case where a fastq_dir specified in the sample sheet is a symlink---not sure if it's worth adding an explicit test? Also, note that I'm only a "groovy novice", and suggestions containing a more robust or conventional implementation would be appreciated.

## PR checklist

- [X] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/spatialvi/tree/main/.github/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/spatialvi _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [X] Make sure your code lints (`nf-core pipelines lint`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f7010ff491a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.