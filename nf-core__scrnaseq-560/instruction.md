# Issue

**Title:** feat(qcatch): nest qcatch_protocol, expose n_partitions, run QCatch for all simpleaf protocols

## Description

## Summary

Refines the simpleaf→QCatch QC integration, following up on review feedback in #558.

### Changes

**1. `protocols.json`: nest QCatch chemistry under `simpleaf`**
QCatch uses different chemistry strings than simpleaf (e.g. `10X_3p_v3` vs `10xv3`), so a mapping is needed. Previously this lived in a top-level `qcatch` key, which read like a separate aligner. It now lives as a `qcatch_protocol` field inside each `simpleaf` protocol entry, alongside `protocol` and `whitelist`:

```json
"10XV3": { "protocol": "10xv3", "whitelist": "...", "qcatch_protocol": "10X_3p_v3" }
```

`workflows/scrnaseq.nf` derives `qcatch_chemistry` from `protocol_config['qcatch_protocol']` (simpleaf-only; `null` otherwise).

**2. Expose `--qcatch_n_partitions`**
New optional param wired into the `QCATCH` `ext.args`, for non-10X / custom assays where QCatch has no chemistry mapping and can't auto-infer the partition range.

**3. Run QCatch for all simpleaf protocols**
Dropped the previous "skip when chemistry is null" guard. The updated module omits `--chemistry` when unmapped (`10XV1`, `dropseq`) and QCatch infers from metadata or uses `--n_partitions`.

**4. Sync `nf-core/qcatch` module → 0.2.12**
Pulls nf-core/modules#12022: conditional `--chemistry`, qcatch `0.2.12`, software versions emitted via the `versions` topic (subworkflow updated accordingly).

## Testing

Validated end-to-end on the pbmc_1k_v3 dataset (`--aligner simpleaf --protocol 10XV3`): QCATCH runs with `--chemistry 10X_3p_v3`, exit 0, produces report + filtered h5ad + metrics. nf-core modules lint on qcatch: 0 failures.

## PR checklist

- [x] Updated `CHANGELOG.md` and `docs/usage.md`
- [x] `nf-core modules lint qcatch` passes
- [x] Tested on a minimal dataset

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `de2c003b695a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.