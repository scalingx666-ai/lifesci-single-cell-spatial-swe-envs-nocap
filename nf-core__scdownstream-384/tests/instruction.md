# Issue

**Title:** feat: accept custom CellTypist model files in --celltypist_model

## Description

Entries ending in .pkl (local paths or URLs) are staged and loaded directly; other entries are downloaded by name as before. Fail on duplicate model names.

<!--
# nf-core/scdownstream pull request

Many thanks for contributing to nf-core/scdownstream!

Please fill in the appropriate checklist below (delete whatever is not relevant).
These are the most common things requested on pull requests (PRs).

Remember that PRs should be made against the dev branch, unless you're preparing a pipeline release.

Learn more about contributing: [CONTRIBUTING.md](https://github.com/nf-core/scdownstream/tree/master/docs/CONTRIBUTING.md)
-->

## PR checklist

- [x] This comment contains a description of changes (with reason).
- [x] If you've fixed a bug or added code that should be tested, add tests!
- [x] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/scdownstream/tree/master/docs/CONTRIBUTING.md) — N/A, no new tool; existing CellTypist module extended
- [x] If necessary, also make a PR on the nf-core/scdownstream _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository. — N/A, test uses a public CellTypist model URL
- [ ] Make sure your code lints (`nf-core pipelines lint`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [x] Usage Documentation in `docs/usage.md` is updated. — parameter help text in `nextflow_schema.json` updated (rendered on the parameters page)
- [x] Output Documentation in `docs/output.md` is updated. — N/A, outputs unchanged
- [x] `CHANGELOG.md` is updated.
- [x] `README.md` is updated (including new tool citations and authors/contributors). — N/A, no new tool

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `004856758924`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.