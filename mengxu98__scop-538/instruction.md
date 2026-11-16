# Issue

**Title:** Make SCENIC+ environments and result imports reproducible

## Description

RunSCENICPlus(backend = "python") discovers standardized tables or extracts official .h5mu and pickle objects in an isolated subprocess. Combine direct and extended results by cell labels, preserve numeric identifiers and AUC precision, reject ambiguous inputs, and publish complete exports with rollback on failure.

Prepare a separate MuData reading environment and preserve an existing full environment when importing results. Repair the affected macOS SciPy wheel during preparation and cache reuse without switching an initialized interpreter. Default KMP_DUPLICATE_LIB_OK to FALSE while preserving explicit caller settings.

The full Linux profile uses Python 3.11.8 and five fixed upstream Git commits, installs native build tools and libraries, and scopes compiler settings and build constraints to installation. Keep source builds in a per-environment cache, activate the selected Conda prefix, and verify Git revisions through uv when preparing an existing full environment. Report installation failures without dropping the pinned dependency specifications. Native Windows supports the C++ workflow and official-result imports; full upstream environment preparation reports that Linux is required.

The targeted suite passes 62 cases with 279 assertions on macOS, Linux and native Windows. Linux and Windows pass source-directory R package installation, installed-code identity checks, strict Python startup, official-result import and complete C++ inference after Python initialization. macOS passes strict startup and imports through the current source snapshot with the matching native binary.

A new independent Linux environment completes all 13 official Snakemake steps from frozen processed GSE274113 inputs: 128 paired cells, 3,700 RNA genes, 106,741 processed ATAC regions and all 640 candidate TFs, including 267 with zero expression. Installation uses verified public PyPI download files and a temporary HTTPS download relay; native source builds use a fresh per-environment cache. Raw-read preprocessing, LDA retraining and motif database downloads are outside this run.

For this fresh official output, Linux and native Windows import all 103 regulons with zero AUC and assay error; macOS has a maximum floating-point difference of 2.78e-17. C++ scoring with the same official gene and region signatures matches the raw Python AUC values exactly. Linux and Windows C++ network values and AUC matrices match exactly after aligning keys and signatures, including before versus after Python initialization.

Independent C++ inference remains an explicit approximation: 43 direct regulons versus 45 from official Python, with 42 shared; triplet Jaccard is 0.8202, and shared-signature gene/region AUC maximum differences are 0.06881/0.17414. These changes do not alter inference formulas, input TFs or thresholds to force agreement. Native Windows full Python inference and WSL are not tested.

Prefer the public Ubuntu HTTPS archives before the Azure fallback in Linux CI. The previous Ubuntu run spent 47 minutes downloading system dependencies on a slow Azure path, while the concurrent pkgdown runner downloaded the same initial package set in 7 seconds. Keep repository signing, dependency requirements, all tests and executable documentation unchanged. The mirror action passes a real signed-index update and cmake/libgraphblas installation in Ubuntu 24.04 on Linux.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `54c938a7d95c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.