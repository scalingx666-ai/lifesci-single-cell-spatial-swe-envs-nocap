# Issue

**Title:** Resume fix

## Description

Changes to formatting of `meta` so that it doesnt get overwritten and messes up `-resume`. This was giving issues with `isoquant` but I've also fixed it in other locations (umi dedup subworkflow). 

Important to note:
When creating a new meta map, always ensure that first a new map is created. Additionally, using `def x = ...` instead of `x = ...` will make sure that the variable only exists without the closures, resulting in less chance of variables being overwritten.

<!--
# nf-core/scnanoseq pull request

Many thanks for contributing to nf-core/scnanoseq!

Please fill in the appropriate checklist below (delete whatever is not relevant).
These are the most common things requested on pull requests (PRs).

Remember that PRs should be made against the dev branch, unless you're preparing a pipeline release.

Learn more about contributing: [CONTRIBUTING.md](https://github.com/nf-core/scnanoseq/tree/master/.github/CONTRIBUTING.md)
-->

## PR checklist

- [x] This comment contains a description of changes (with reason).
- [x] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/scnanoseq/tree/master/.github/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/scnanoseq _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [ ] Make sure your code lints (`nf-core pipelines lint`).
- [x] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `23b46332d912`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.