# Issue

**Title:** fix: have ingest no longer truncate to settings.N_PCS

## Description

`Ingest` falls back to a hardcoded `settings.N_PCS` (50) whenever the reference `adata`'s `neighbors` params recorded neither `use_rep` nor `n_pcs` — but that's exactly the state `pp.neighbors` leaves when called with its own defaults, and its default (`n_pcs=None`) uses the *full* stored PCA representation unsliced (`_get_pca_or_small_x`), not 50 components. Whenever more than 50 PCs were computed (e.g. `sc.pp.pca(adata, n_comps=100)` then `sc.pp.neighbors(adata)`), `Ingest` silently builds its KNN index and transforms new data in a different, truncated representation than the one that actually produced the reference neighbor graph — no error, just a quietly wrong embedding/label mapping for `sc.tl.ingest`.

Found via sibling comparison between `Ingest._init_neighbors`'s three branches and `_get_pca_or_small_x` (the function that actually computes `pp.neighbors`' representation) — the first two branches already match the stored params correctly; only the fallback diverged.

<details>
<summary>Repro</summary>

```python
import anndata as ad, numpy as np, scanpy as sc
X = np.random.default_rng(0).normal(size=(300, 200)).astype("float32")
adata_ref = ad.AnnData(X)
sc.pp.pca(adata_ref, n_comps=100)
sc.pp.neighbors(adata_ref)  # default n_pcs=None -> uses all 100 PCs
ing = sc.tl.Ingest(adata_ref)
ing._init_neighbors(adata_ref, None)
print(ing._n_pcs)  # 50 before this fix, should be 100
```

</details>

<details>
<summary>AI assistance</summary>

- Tool: Claude Code
- Role: found the inconsistency by comparing `Ingest`'s three `_init_neighbors` branches against `_get_pca_or_small_x`'s actual default behavior, then wrote the fix and regression test
- Verified locally against a synthetic reproduction (the repo's `pbmc68k_reduced` test fixture hits an unrelated zarr-version incompatibility in this environment, so the new test couldn't be run through the full suite here — logic was verified directly against the same `sc.pp.pca`/`sc.pp.neighbors`/`sc.tl.Ingest` calls the test uses)

</details>

<details>
<summary>Test results</summary>

Added `test_representation_more_than_n_pcs_default` to `tests/test_ingest.py`, covering `n_comps = settings.N_PCS + 20`. Manually verified the underlying fix across `n_comps` of 30, 50, and 100 against a synthetic `AnnData` (below, below+at, and above the `settings.N_PCS` threshold) — all three now correctly match the PCs `pp.neighbors` actually used, whereas 100 previously and incorrectly truncated to 50.

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b92a4dee9ad9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.