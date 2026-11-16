# Issue

**Title:** Add option to exclude genes as candidate highly variable genes for integration

## Description

It is often preferable to exclude certain genes as candidate genes for integration. Some genes (e.g., heat shock proteins) may be highly variable but are not informative for assigning cell type.

This PR adds an option (--integration_excluded_genes) to input a list of genes (one per line) that will not be considered as candidate highly variable genes.

## PR checklist

- [✓] This comment contains a description of changes (with reason).
- [✓] If you've fixed a bug or added code that should be tested, add tests!
- [N/A] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/scdownstream/tree/master/.github/CONTRIBUTING.md)
- [N/A] If necessary, also make a PR on the nf-core/scdownstream _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [✓] Make sure your code lints (`nf-core pipelines lint`).
- [✓] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [✓] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [N/A] Usage Documentation in `docs/usage.md` is updated.
- [N/A] Output Documentation in `docs/output.md` is updated.
- [N/A] `CHANGELOG.md` is updated.
- [N/A] `README.md` is updated (including new tool citations and authors/contributors).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15776a5e384b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.