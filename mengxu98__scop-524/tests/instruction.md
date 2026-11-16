# Issue

**Title:** Fix Conos and MDS workflows in executable documentation

## Description

Executable documentation exposes two workflow failures: Conos still uses the defunct Seurat slot accessor, and classical MDS omits the coordinate standard deviations needed by automatic scree dimension selection. This change restores both workflows while retaining the native numerical algorithms and runnable examples.

Use scoped Conos matrix preparation through SCOP's layer accessor while retaining Conos's native pairwise projections, nearest-neighbor graph construction and parameters. The adapter leaves the Conos namespace and original R6 methods unchanged. It is limited to Conos 1.5.4 and checks the two internal interface signatures; other versions retain their public native buildGraph path.

Remove two unnecessary operations from matrix preparation: scaling all genes when the caller only reads the unchanged normalized data layer, and transposing the full expression matrix before selecting the same analysis genes. The scaled-data path retains the original Seurat scaling.

Classical MDS already computes its eigenvalues. Store `sqrt(eigenvalue / (n - 1))` for the retained coordinates in the reduction standard deviations; embeddings and the existing scree selection rule remain unchanged. Regenerate the RunMDS help page to document the returned statistics.

Validation:

- Reproduced the empty-MDS-standard-deviation failure before the fix. All 97 assertions across 10 dispatch/geometry tests pass without failures, warnings or skips. Coordinates match native cmdscale and standard deviations match both eigenvalue-derived values and empirical coordinate standard deviations at 1e-12 tolerance.
- The complete unmodified RunStandardWorkflow help examples render locally without embedded errors in 54.847 seconds, including the MDS and spatial workflows.
- Previous head 671cb5f52 passed all four package-check jobs and the complete RunIntegration page. Website rendering then stopped at RunStandardWorkflow; the latest commit addresses that next failure. Latest-head CI is pending.

- The complete Seurat fast-path test file passes: 27 test cases, 146 assertions, no failures, errors, warnings or skips. Both new Conos tests run with the real backend. Internal usage checks and diff whitespace checks pass.

- Reproduced the original defunct-slot error with real Conos 1.5.4, Seurat 5.6.0 and SeuratObject 5.4.0.
- On the complete panc8_sub input (12,932 genes, 1,600 cells, five batches), compared all ten batch pairs with the same 2,000 analysis genes. Normalized matrix outputs are identical. The reference only replaces the obsolete slot spelling with layer; it retains the redundant work.
- Three interleaved local matrix-preparation runs, after dependency installation completed: reference 3.146/3.707/2.896 seconds; optimized 0.269/0.286/0.304 seconds. Median 3.146 to 0.286 seconds (11.0x). This measures matrix preparation, not whole-site speed.

- On the same complete input, native pairwise models and graph weights match the compatibility-only reference at 1e-12 tolerance. Single graph timings: 25.121 seconds reference, 24.015 optimized (about 4%); the matrix-stage speedup is not the end-to-end speedup.
- The original RunIntegration call with Conos, 50 input dimensions and UMAP completes in 63.24 seconds, preserving all 1,600 cell names, all 12,932 input genes and finite embeddings.

Current main CI at 85224cf39: all four R checks pass. pkgdown dependency setup takes 35m11s, rendering stops after 77m10s at RunIntegration (22m50s for that page), and deployment is skipped. Those are failing-build timings, not a completed website benchmark. The remaining large costs include other integration methods and RunDoubletCalling; this PR covers the reproduced Conos and MDS failures and redundant Conos preparation work.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `85224cf393d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.