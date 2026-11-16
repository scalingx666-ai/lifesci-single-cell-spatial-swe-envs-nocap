# Issue

**Title:** Fix the IVF-PQ abort on cuVS 26.12 and make CI hangs fail fast

## Description

Fixes what still fails in CI: the nightly abort in `test_mg_bbknn[mg_ivfpq]`, test jobs that hang until the job limit, and a flaky test of ours.

IVF-PQ on small inputs:
- cuVS 26.12 (cuVS PR 2740) no longer trains a k-means codebook with more centroids than training rows. IVF-PQ trains 256 PQ codes on half of the rows, so with the defaults an index under 512 rows is rejected. The single-GPU build raises; the multi-GPU build throws inside an OpenMP region, which ends the process (exit 134). That is the `rapids_prerelease` abort: the bbknn batches of `pbmc68k_reduced` have 501, 182 and 17 cells.
- `ivfpq`, `mg_ivfpq` and `all_neighbors` with `algo="ivf_pq"` now search such inputs by brute force. For batched `all_neighbors` builds the check uses half the average cluster size, a heuristic for the smallest cluster cuVS forms.

CI hangs:
- The stable/dev jobs that ran into the 45-minute limit were all stuck inside an IVF-Flat or IVF-PQ call of cuVS 26.10. That call holds the GIL, so `pytest-timeout` cannot fire. `faulthandler_timeout = 600` with `faulthandler_exit_on_timeout` (pytest 9) runs a watchdog thread that prints the stack of the stuck test and ends the run.
- The "Run tests" steps get a 30-minute limit (a full run takes 12-20).

Tests:
- `test_mask_correctness` drew an unseeded mask that selected fewer than 2 variables for about 1% of `pytest-randomly` seeds; it uses a fixed mask now.
- The test group requires `decoupler>=2.3.1` and `scikit-learn>=1.9.1`, which the GSEA and LDA parity tests need. CI already resolves these versions.
- `dc.waggr` skipped the shuffle for `seed=0` (`if seed:`); it now shuffles as decoupler >= 2.3 does.

Tested on one GPU with cuVS 26.10.0 and the 27.02 nightly: the neighbors, waggr, GSEA, PCA mask and Mixscape LDA tests pass (178 in each env). Without the guards the nightly raises (`ivfpq`) or aborts (`mg_ivfpq`, `all_neighbors`). The full suite did not finish locally (shared box), and nothing ran with two GPUs visible.

Notes:
- A hang in the scverse integration-testing nightly now ends as a failure after about 25 minutes and opens a bot issue here; before, the job was cancelled after 6 hours without one.
- Not in this PR: sharded `mg_ivfpq` is not covered by the guard; the `distribution_mode` docs and the `mg_ivfflat` assert say `'shared'` where cuVS wants `'sharded'`; the default `n_lists` exceeds the row count for 1-7 rows, which aborts `mg_ivfflat`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a1373c63789`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.