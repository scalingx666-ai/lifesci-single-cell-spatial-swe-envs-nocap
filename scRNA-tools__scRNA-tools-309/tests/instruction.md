# Issue

**Title:** Add DotMatch for CRISPR guide-capture assignment

## Description

.

This adds a minimal DotMatch record to the database:

- `database/tools.tsv`: Python tool, Apache-2.0, repository, and a narrow description;
- `database/repositories.tsv`: PyPI, Conda, and GitHub identifiers;
- `database/categories-idx.tsv`: `Perturbations`.

The intended use here is fixed read-window assignment to known CRISPR guides or feature barcodes before downstream single-cell analysis. DotMatch is not being presented as a UMI counter, cell caller, or complete single-cell pipeline.

Public references:
- Documentation: https://dotmatch.readthedocs.io/en/latest/tutorials/scverse-perturb-seq.html
- PyPI: https://pypi.org/project/dotmatch/
- Bioconda: https://anaconda.org/bioconda/dotmatch

Validation: TSV field counts, alphabetical placement, and `git diff --check` pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `44b5cc0e34ac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.