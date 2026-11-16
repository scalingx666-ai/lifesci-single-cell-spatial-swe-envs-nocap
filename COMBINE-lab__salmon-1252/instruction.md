# Issue

**Title:** fix: --noLengthCorrection uses a constant length (#1243); add --noEffectiveLengthCorrection

## Description

## Length-correction flags for 2.9.0: fix `--noLengthCorrection` (#1243), add `--noEffectiveLengthCorrection`

These two commits were meant for #1251 but were pushed after it merged.

### 1. `--noLengthCorrection` takes length out of the model again (#1243)
Since 2.0 the flag gave each transcript its raw length as its effective length. That is C++'s `--noEffectiveLengthCorrection`, so estimates still depended on length. For 3' tagged-end protocols (QuantSeq), the reason the flag exists, this put back the length dependence the flag is meant to remove, and it moved reads between isoforms.

Every transcript now gets effective length 100, as in salmon 1.x. This covers the EM, `quant.sf`'s `EffectiveLength` and TPM, and the online phase's start-position term, in reads, `--sketch`, `--deterministic`, `--rad` and `-a` modes.

### 2. New `--noEffectiveLengthCorrection` (from C++ salmon)
It divides by the raw transcript length, which is exactly what 2.0–2.8's `--noLengthCorrection` did, so anyone who relied on that behavior can get it back.
- `--noLengthCorrection` wins if both flags are given, as in C++.
- Like `--noLengthCorrection`, it is refused together with `--seqBias`, `--gcBias` or `--posBias` (the existing #1140 check, extended to this flag).
- The base effective length now comes from one `salmon_model::LengthCorrection` (Effective / Raw / None), used by all three quant engines.

The deprecated `--online -a` path shares that computation, so both length flags now apply there. Its warning now names only `--noFragLengthDist`.

### Verification
Isoform repro from #1243: a short isoform sharing a long one's 3' kb; 4000 reads in the shared region, 1000 unique to the long isoform.

| | short / long reads | EffectiveLength |
|---|---|---|
| C++ 1.12 `--noLengthCorrection` | 0 / 5000 | 100 / 100 |
| 2.8.0 `--noLengthCorrection` | 3750 / 1250 | 1000 / 5000 |
| this PR `--noLengthCorrection` (SA, sketch, deterministic, `-a`, `--online -a`) | 0 / 5000 | 100 / 100 |
| C++ 1.12 `--noEffectiveLengthCorrection` | 3750 / 1250 | 1000 / 5000 |
| this PR `--noEffectiveLengthCorrection` | 3750 / 1250 (byte-identical to 2.8.0's `--noLengthCorrection` in SA, sketch, `-a`) | 1000 / 5000 |

GEUVADIS ERR188044 (10M pairs), Ensembl cDNA, compared with C++ salmon (NumReads):

| flags | Pearson | Spearman (expressed) | L1 / total |
|---|---|---|---|
| default (reference point) | 0.99982 | 0.957 | 2.4% |
| `--noLengthCorrection`, before this PR | 0.593 | 0.490 | 66% |
| `--noLengthCorrection`, this PR | 0.974 | 0.950 | 4.0% |
| `--noEffectiveLengthCorrection`, this PR | 0.99983 | 0.958 | 2.1% |

The remaining `--noLengthCorrection` gap is a few isoform pairs splitting shared reads differently; family totals agree. With no length term those splits are poorly determined. `--stopRule global` gives the same numbers.

- **Without either flag:** `quant.sf` is byte-identical to develop (SA and `--sketch`, GEUVADIS).
- **Determinism:** `--noEffectiveLengthCorrection` is byte-identical to the previous 2.9 build's `--noLengthCorrection`.
- **New tests:**
  - RAD-level effective-length modes, including precedence.
  - The #1243 isoform split, which fails on the old code.
  - The CLI bias-conflict check for both flags.
- `cargo test --release --workspace --locked`: 383 passed. Clippy `-D warnings` and fmt are clean.

### Also: #1238
#1238 is fixed by #1239, which is already on develop. With the issue's miRNA repro, `--softclip` and `--softclipOverhangs` go from 91.3% to 100% mapped, and all 300 tailed miR-21 reads now map. The release notes now say so.

Release notes, `docs/cli-flag-status.md` and the website CLI reference are updated. #1243 and #1238 will close when the release reaches master.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_016brRcptooQkxWr6TyWnwAE

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0fa58334f203`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.