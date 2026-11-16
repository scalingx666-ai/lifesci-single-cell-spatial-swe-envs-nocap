# Issue

**Title:** Swap X and Y coords

## Description

## Before 
![image](https://github.com/nf-core/spatialtranscriptomics/assets/7051479/b99f4fc6-d152-406c-8bce-f880dbeb3750)

## After
![image](https://github.com/nf-core/spatialtranscriptomics/assets/7051479/444f74bc-f91e-4b81-9686-2e60fe2b3513)

This fixes a regression introduced in #45. The problem was that the original version overrode the column names manually, 
and swapped x and y columns while doing so, see .

another reason to switch to the IO functions of squidpy/spatialdata instead of this custom code. 

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

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `103a5958970f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.