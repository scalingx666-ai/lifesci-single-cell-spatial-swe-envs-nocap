# Issue

**Title:** Fix schema validation for spaceranger reference

## Description

Needs to be `path` instead of `file-path` because it can be either directory or file. 

Before it failed for me with

```
ERROR ~ ERROR: Validation of pipeline parameters failed!

 -- Check '.nextflow.log' file for details
The following invalid input values have been detected:

* --spaceranger_reference: '/<redacted>/refdata-gex-GRCh38-2020-A' is not a file, but a directory (<redacted>/refdata-gex-GRCh38-2020-A)`
```

<!--
# nf-core/spatialtranscriptomics pull request

Many thanks for contributing to nf-core/spatialtranscriptomics!

Please fill in the appropriate checklist below (delete whatever is not relevant).
These are the most common things requested on pull requests (PRs).

Remember that PRs should be made against the dev branch, unless you're preparing a pipeline release.

Learn more about contributing: [CONTRIBUTING.md](https://github.com/nf-core/spatialtranscriptomics/tree/master/.github/CONTRIBUTING.md)
-->

## PR checklist

- [ ] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/spatialtranscriptomics/tree/master/.github/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/spatialtranscriptomics _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [ ] Make sure your code lints (`nf-core lint`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5db31c455a64`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.