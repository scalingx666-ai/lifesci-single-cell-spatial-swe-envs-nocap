# Issue

**Title:** Fix quarto cache issues on singularity

## Description

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
- [ ] Make sure your code lints (`nf-core lint`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).


When running the workflow with `singularity` I have been getting errors because quarto tries to write to `$HOME/.cache` which is not writeable inside the container. This PR sets two envs vars that force quarto to write the tempoary files into the current work directory. 

These variable now apply to all processes. Alternatively, these variables could also be set in the bash script for `quarto render` as
```bash
export XDG_CACHE_HOME="./.quarto_cache_home"
export XDG_DATA_HOME="./.quarto_data_home"
```

As every notebook currently has their own process I didn't go for this variant because of redundencies. An alternative would be to make a generic quarto module similar to the `jupyternotebook` module: https://github.com/nf-core/modules/tree/master/modules/nf-core/jupyternotebook

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f78e242f8506`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.