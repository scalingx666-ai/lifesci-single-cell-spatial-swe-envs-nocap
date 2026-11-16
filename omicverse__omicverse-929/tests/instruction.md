# Issue

**Title:** fix(io): re-export every spatial reader on the ov.io facade

## Description

`ov.io` mirrors its submodules' readers as top-level shortcuts, and the list was maintained by hand. It held **five of the eight** spatial readers:

| on `ov.io` | only on `ov.io.spatial` |
|---|---|
| `read_visium_hd`, `read_visium_hd_bin`, `read_visium_hd_seg`, `read_xenium`, `read_nanostring` | **`read_visium`**, `read_atera`, `read_stereoseq` |

So `ov.io.read_visium_hd` worked while `ov.io.read_visium` — the commonest call of the set — raised `AttributeError`.

Nothing in the namespace distinguished the shortcuts from the rest, so documentation and downstream code read it as uniform and wrote the short form. It fails only when the line runs, and an `AttributeError` on a reader name reads like a version or install problem rather than a missing re-export.

This bit our own agent catalog in three places, one of which instructed readers that `ov.io.read_visium` is the reader "**NOT** `sc.read_visium`" — confidently wrong, and Visium is the most common spatial platform.

All eight are now re-exported, plus `bin_stereoseq` and `write_visium_hd_cellseg` for symmetry.

## The test

`tests/test_io_facade_reexports.py` walks each submodule's own `__all__` rather than a second hand-written list, so adding a reader to a submodule now *requires* the shortcut too — the mirror can no longer drift silently. It also checks the reverse direction (nothing in `ov.io.__all__` is a dead name) and that each shortcut **is** the submodule's object rather than a same-named other one.

Verified by putting the bug back: removing `read_visium` from the facade makes it fail on exactly `test_submodule_export_is_reachable_on_the_facade[spatial-read_visium]`, and restoring it goes green. A test that has never been seen to fail is not yet evidence of anything.

Conversion helpers (`convert_to_pandas`, `wrap_dataframe`, `convert_adata_for_rust`) are deliberately **not** mirrored — the test scopes to readers. Widening the facade to cover them is an API decision, not a drift repair, so I left it alone.

## Two documentation-only fixes in the same pass

**`_geom.py` overstated what the default path needs.** It said the FGW route "needs nothing beyond what omicverse already installs". POT is declared in no extra and is absent from a plain install — `tests/space/test_geom_stereoseq.py` fails with `ModuleNotFoundError: No module named 'ot'` at `_geom.py:189` on a clean environment, which is that claim being wrong in CI right now. The docstring names `pip install POT`, and points at `method='icp'` / `'rigid'` as the genuinely dependency-free routes (scipy only).

**Two mrna regression tests guarded the wrong backend.** They `importorskip("dnachisel")` but `mrna_design` folds the CDS on its way to a design (`_mrna.py:165-167` → `rna_fold`), so on an environment with dnachisel but no ViennaRNA a missing optional backend became a failure instead of a skip.

## Tests

`-k "synbio or io or space"`: **3303 passed, 780 skipped, 10 failed** — the 10 are all `test_geom_stereoseq.py` and all `ModuleNotFoundError: No module named 'ot'`, i.e. pre-existing and exactly the condition the `_geom.py` docstring change now documents. `_geom.py` itself is untouched apart from that docstring.

## Considered and deliberately not done

**De-scanpy-ing `ov.space.niche`.** `_niche.py` uses scanpy only as a kNN+Leiden utility on a plain matrix, which looks like an easy removal. It is not, and I measured why: `sc.pp.neighbors` builds **UMAP fuzzy simplicial connectivities** (weighted), not a plain kNN graph (binary). Swapping in a plain kNN + `leidenalg` on the same synthetic niche input gives **ARI = 0.51** against the current path — 7 clusters versus 12. That is a different answer, not a different labelling of the same answer, and it would move every existing user's niche labels. Removing scanpy honestly would mean reimplementing the fuzzy simplicial set, i.e. depending on `umap-learn` or vendoring it — not obviously better than depending on scanpy, which is a core dependency regardless.

**`mmgbsa`'s frame count.** `md_refine_ns=0` writes ~1000 frames and scores 50 of them; writing fewer would change which frames are scored and therefore shift ΔG on the default path, for an I/O saving. Same reasoning as 2.3.1 left it alone.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4e7938e7c0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.