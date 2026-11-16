# Issue

**Title:** fix: work across anndata 0.11–0.13 and both zarr generations

## Description

omicverse pins `anndata<0.12` and `zarr<3`, which locks out the current releases of both — and already conflicts with an installed dependency: **squidpy 1.8.3 requires `zarr>=3`**. This widens the range to `anndata>=0.10,<0.14` / `zarr>=2.18.7,!=3.0.*` and fixes what actually breaks across it.

## What differs — measured, not read off a changelog

Probed on real installs: anndata 0.11.4 + zarr 2.18.7, 0.12.19 + zarr 3.3.0, 0.13.3 + zarr 3.3.0.

| behaviour | 0.11 | 0.12 | 0.13 |
|---|---|---|---|
| `AnnData(..., dtype=)` | warns | warns | **TypeError** |
| `anndata.read` | present | **removed** | removed |
| `/` in a key when writing | allowed | warns | **ValueError** |
| `anndata.__version__` | fine | fine | **deprecated** |
| zarr 3 | no | yes | **required** |

The last two rows are not in the release notes' breaking-changes list — they only turned up by running the probe.

## What changed

**Most of this needs no version branching.** Casting before construction is what `dtype=` did, and it satisfies every version, so the eleven call sites become `as_dtype(X, dtype)` with no version check anywhere. Those sites already emitted a `FutureWarning` on 0.11.4 — existing debt, not something the upgrade introduces.

| | |
|---|---|
| `omicverse/_anndata_compat.py` | `as_dtype`, `sanitize_key`, `anndata_version` |
| 11 call sites | `AnnData(X, dtype=T)` → `AnnData(as_dtype(X, T))` |
| `samap/samalg` | `anndata.__version__` → `anndata_version()` (deprecated in 0.13) |
| `pl/_scatterplot_backend` | sanitise the `{name}_colors` keys — the one place a user-controlled label reaches a store key |
| `pyproject.toml` | widen both pins |

`as_dtype` routes sparse input through `.astype`: `numpy.asarray` would densify a `csr_matrix`, and one call site (`external/graphvelo`) passes one.

## On the 362 dynamic keys

A scan of every write into `uns`/`obsm`/`layers`/`varm`/`obsp` found 362 with a computed key. Provenance matters more than the count:

- `key + '|X_pca'` — a mode string, pipe not slash;
- `f'X_scfoundation_{method}'` — an internal enum;
- `f'{name}_colors'` — **`name` is an `adata.obs` column, which the user names.**

Only the last kind can carry a slash someone chose, and those are the ones sanitised. The rest fail loudly at write time on 0.13 if they ever do, which is the right failure mode — pre-sanitising 362 sites is not.

## zarr needs nothing

omicverse touches zarr directly in exactly two places — an `isinstance(X, zarr.Array)` check in `pp/_pca.py` and one `zarr.open` on a tifffile store in `external/bin2cell` — and both work unchanged on 3.3.0 (verified in the zarr 3 environments). Everything else goes through anndata, which absorbs the generational difference itself. That is why the floor here is anndata's own constraint and not a separate one.

## Verified

The compat layer and the changed call sites were exercised in all three environments. On 0.13.3 the two behaviours this fixes are confirmed as hard failures without it:

```
anndata 0.13.3.post0 | zarr 3.3.0
  as_dtype(ndarray) → float32  AnnData=(8, 3)      ✓
  as_dtype(csr)     → float32  AnnData=(8, 3)      ✓
  旧写法 AnnData(dtype=):                           ✗ TypeError
  key 'cell/type_colors' 未 sanitize:               ✗ ValueError
  key 'cell_type_colors' sanitize 后:                ✓
```

## Not covered

`anndata<0.10` is untested — the floor is set at 0.10 because that is what the existing code already assumes (`pp/_pca.py` has a `< 0.8.0rc1` branch), not because it was verified.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_0156k5ARWtUbtjbfRypRavEa

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `44d5f49041b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.