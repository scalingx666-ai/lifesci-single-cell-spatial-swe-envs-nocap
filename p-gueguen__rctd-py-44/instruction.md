# Issue

**Title:** feat: rctd.deconvolve writes results into the AnnData

## Description

Adds `rctd.deconvolve(adata, reference, ...)`: runs `run_rctd` unchanged and writes the results into the AnnData, scanpy style (in place, or `copy=True` for a new object). Same keys as `rctd run` writes to its output file: `obsm["rctd_weights"]`, `obs["rctd_first_type"]`, `obs["rctd_spot_class"]`, ... with `"filtered"` / NaN for pixels the UMI filters removed. Needed for the scverse ecosystem listing.

- The CLI's writer moves to `rctd/_anndata.py`; the CLI imports it from there.
- Fix: a second run in another mode (API, or `rctd run` on its own output) left the first mode's `rctd_*` keys behind. Now only the keys rctd-py writes are replaced; other keys, including users' own `rctd_*` ones, are kept.
- Results are built before anything is written, so a failure leaves the input unchanged. Backed AnnData gets a clear error.
- Docs: API page, quickstart, README, CHANGELOG.

Checked:
- CLI output identical to the released 0.4.1 wheel in full, doublet and multi (Xenium, L40S), slot by slot.
- `deconvolve` writes exactly `run_rctd`'s arrays on Xenium (all modes, float64/float32) and Visium HD; h5ad round trip unchanged; CLI output == `deconvolve` output.
- Tests: GPU 201 + 17 slow, CPU 185 + 17 slow. New tests fail when the writer call is removed and on the previous prefix-deleting version.
- Independent code review: no blockers; its should-fix items are in the second commit.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4acf14a381a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.