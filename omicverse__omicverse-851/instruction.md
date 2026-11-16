# Issue

**Title:** fix(pyscenic): expose faster binarization options

## Description

## Summary
- Expose the existing pySCENIC BIC thresholding method through `binarize(method="bic")` while keeping the default as HDT.
- Add `use_tqdm` progress reporting for threshold derivation and switch multiprocessing to ordered `imap` over per-regulon arrays.
- Preserve empty-regulon behavior and add coverage for serial BIC, parallel BIC, and empty matrices.

## Context
Issue #826 reports very slow pySCENIC binarization. The bundled implementation already supports BIC inside `derive_threshold()`, but `binarize()` always used the HDT path. This change makes the faster BIC option available without changing default behavior.

## Benchmarks
Synthetic AUC matrices, `OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1`.

BIC with 10,000 cells and increasing regulons:

| Shape | workers=1 | workers=4 | workers=8 | workers=12 |
| --- | ---: | ---: | ---: | ---: |
| 10,000 x 200 | 5.458s | 3.375s | 3.428s | 4.620s |
| 10,000 x 500 | 12.396s | 5.704s | 5.928s | 6.765s |
| 10,000 x 1,000 | 27.763s | 9.237s | 8.700s | 10.361s |
| 10,000 x 2,000 | 62.230s | 17.359s | 14.643s | 14.147s |

BIC with larger cell counts:

| Shape | workers=1 | workers=2 | workers=4 | workers=8 |
| --- | ---: | ---: | ---: | ---: |
| 10,000 x 200 | 4.927s | 4.335s | 3.172s | 3.563s |
| 50,000 x 300 | 35.717s | 17.501s | 10.896s | 8.255s |
| 100,000 x 300 | 73.799s | 32.579s | 18.250s | 14.880s |

HDT remains the default and benefits from multiple workers on larger regulon sets:

| Shape | workers=1 | workers=4 | workers=8 |
| --- | ---: | ---: | ---: |
| 1,000 x 50 | 29.787s | 9.912s | 8.291s |
| 1,000 x 100 | 60.402s | 19.170s | 17.332s |
| 1,000 x 200 | 145.611s | 41.389s | 27.015s |

## Validation
- `uv run --no-sync pytest tests/external/test_pyscenic_binarization.py -q`
- `git diff --cached --check`
- Pre-commit review by subagent; fixed the reported empty-regulon edge case before commit.

References #826.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `509b98432b03`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.