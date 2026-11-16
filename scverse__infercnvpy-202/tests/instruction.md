# Issue

**Title:** test: fast offline test run, CDN-hosted datasets and heatmap image tests

## Description

Summary: The default test run now takes about 3 minutes instead of 10 and needs no network once the test data is cached. The example datasets are hosted on exampledata.scverse.org and loaded through a scverse-misc registry pinned by sha256, and the chromosome heatmaps have image comparison tests. This PR builds on the logging and docs PR, so it targets that branch.

Changes:
- Datasets
  - `maynard2020_3k` and `oligodendroglioma` are loaded with `scverse_misc.datasets` from `datasets/registry.yaml`. Both files are on exampledata.scverse.org under `infercnvpy/<dataset>/<file>`, and I checked their sha256 through the CDN from two networks. There are no fallback downloads, so the CDN is the single source of truth.
  - `oligodendroglioma.h5ad` is no longer shipped in the wheel, which makes the wheel 4 MB smaller. It is downloaded on first use like `maynard2020_3k`.
  - A small loader keeps the old cache layout, so files that existing users already downloaded are reused. `INFERCNVPY_DATA_DIR` still sets the cache folder, and it is now read when a dataset is loaded instead of at import.
  - The registry comment says how to change a file. You overwrite the key, re-pin the sha256 and purge the CDN cache, because CDN edges keep serving the old bytes for about 24 hours.
- Tests
  - Benchmarks are skipped by default through `--benchmark-skip` in the pytest options, and `--benchmark-only` runs them. They took about 60 % of the run time and asserted nothing.
  - Tests that need the internet (BioMart queries, dataset downloads) have an `internet` marker and only run with `--internet-tests`, as in scanpy. The scheduled CI run also runs them.
  - The infercnv result on the oligodendroglioma data is computed once per session, and pbmc3k is loaded in a fixture, so pytest no longer downloads it while collecting tests. pbmc3k comes from scanpy's copy on the scverse CDN, pinned by scanpy's sha256.
  - A test run writes nothing into the repository, because downloads go to the infercnvpy cache folder and the BioMart cache goes to a temporary folder.
  - `test_layer_parameter` no longer runs three times for an unused fixture, and the mock data uses a local random generator instead of the global seed.
  - `chromosome_heatmap` and `chromosome_heatmap_summary` are compared against small baseline images in `tests/_images`.
- CI caches the data folder, keyed on `registry.yaml` and `tests/conftest.py`, because both pin downloaded files.

Testing: The full suite passes locally (75 passed, 12 skipped), and it also passes with sockets blocked once the data is cached. With an empty cache and `--internet-tests`, all tests pass and every dataset comes from the CDN. prek and mypy pass. The image baselines were made on macOS, so the first Linux CI run shows whether the tolerance is enough.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5ab78f4831b8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.