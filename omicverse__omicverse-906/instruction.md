# Issue

**Title:** feat(io): ov.io.read_fcs — a general Flow Cytometry Standard reader

## Description

Moves FCS reading out of the EV module and into `ov.io`, where format I/O belongs.

## The problem

The only FCS reader was `ov.single.ev.read_fcs`, inside the single-extracellular-vesicle module. Reading an FCS file is I/O, not an assay — and the EV framing was **lossy**. It took whatever DataFrame the backend returned and dropped the FCS metadata, discarding the two things a cytometry file exists to carry:

- **`$PnN` vs `$PnS`** — the DETECTOR name (`FITC-A`) versus the MARKER on it (`CD3`). Confusing these is *the* classic FCS mistake: the same antibody sits on a different detector between panels, and the same detector carries a different antibody between experiments.
- **`$SPILLOVER`** — the acquisition-time spillover matrix. Without it compensation cannot be applied later, and uncompensated fluorescence is not wrong-*looking*, just wrong.

## `ov.io.read_fcs`

```python
adata = ov.io.read_fcs('sample.fcs')
adata.var[['channel', 'marker']]      # FITC-A -> CD3
adata.uns['fcs']['spillover']         # parsed, labelled, square DataFrame
```

A plain AnnData: events × channels, `channel`/`marker` as separate var columns, indexed by marker where one exists, full keyword dict in `uns['fcs']['keywords']`, and `$SPILLOVER` **parsed** into a labelled matrix rather than left as the raw comma-delimited string that both pytometry and FlowKit hand back. Conventional flow, spectral flow and mass cytometry alike; knows nothing about any assay.

Parsing is **flowio** (BSD-3) — the parser underneath both pytometry and FlowKit — so the output contract is stable regardless of which higher-level cytometry package is installed.

## Interop with pytometry is verified, not assumed

omicverse is GPL-3.0; flowio/flowutils/flowkit are BSD-3 and [pytometry](https://github.com/scverse/pytometry) (scverse) is Apache-2.0 — all clean to depend on.

The var schema is **byte-identical** to `pytometry.io.read_fcs`: same index rule, same `n / channel / marker / PnB / PnE / PnG / PnR`. That alone was **not sufficient** — `pytometry.pp.compensate` does `adata.uns["meta"]["spill"]` and calls `.columns` on it, so the key must exist and hold the *parsed* matrix. Two interop runs failed before that surfaced; both halves are now pinned by tests.

| | |
|---|---|
| `pm.pp.compensate` | ✅ |
| `pm.tl.normalize_logicle` / `normalize_biexp` / `normalize_arcsinh` | ✅ |
| `pm.pp.split_signal` | ✅ |
| `compensated=True` vs `pm.pp.compensate` | **bit-identical** (max abs diff 0) |

## Compensation is off by default, on purpose

The acquisition matrix is frequently wrong, most labs recompute it from single-stain controls, and applying it silently would leave no way to tell whether it had been. When on: only the detectors the matrix names are touched (scatter and time pass through), and **subsetting happens after compensation** — the matrix is defined over the full detector set, so subsetting first would silently compensate against a different matrix than the instrument recorded.

## Backward compatibility

`ov.single.ev.read_fcs` delegates here and keeps its own conventions (`event%06d` row names, intensity `value_type`, `uns['ev']`), so existing callers are unaffected — and it now **gains** the spillover matrix and the channel/marker split it used to discard. Its CSV path still forwards to `read_nanofcm`, which is genuinely EV-specific.

## Tests

24 tests. The FCS fixture is **written by the test** with `flowio.create_fcs` rather than shipping a binary or depending on a vendor sample, so CI actually exercises `$PnS` and `$SPILLOVER` instead of skipping.

All five load-bearing behaviours were **mutation-checked** — index rule, `uns['meta']['spill']`, scatter exclusion, compensate-before-subset, EV metadata passthrough. Reverting each one turns the suite red; restoring turns it green.

## Not in this PR

**Gating.** pytometry has none either (verified: no gating symbol in `pm.io`/`pp`/`tl`/`pl`), and it is the real remaining gap for flow cytometry — sequential polygon/quadrant gates, a population hierarchy, and Gating-ML interop. That is a design question, not a reader change.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `97728b50f3f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.