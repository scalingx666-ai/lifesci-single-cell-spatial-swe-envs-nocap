# Issue

**Title:** feat(cli): --library presets expand into end clipping

## Description

Implements the five decisions in  .

## What it does

```bash
trim_galore --paired --library emseq R1.fq.gz R2.fq.gz
```

is exactly

```bash
trim_galore --paired --clip_R1 10 --clip_R2 10 --three_prime_clip_R1 10 --three_prime_clip_R2 10 R1.fq.gz R2.fq.gz
```

| `--library` | `--clip_R1` | `--clip_R2` | `--three_prime_clip_R1` | `--three_prime_clip_R2` |
|---|---|---|---|---|
| `emseq` | 10 | 10 | 10 | 10 |
| `accel` (aliases `swift`, `xgen`) | 10 | 15 | 10 | 10 |
| `zymo` | 10 | 10 | 10 | 10 |
| `scbs` (alias `single_cell`) | 6 | 6 | 6 | 6 |
| `pbat` | 8 | 8 | 8 | 8 |

## Against each decision

**Shape.** A `clap::ValueEnum` on `--library`, so two kits at once is unrepresentable rather than rejected by a conflict rule. `--rrbs`, `--clock`, `--implicon` and Tecan/NuGEN Ovation RRBS are absent, per the clip-bundle membership criterion; that reasoning is recorded in the module docs so the next person proposing `taps` finds the rule rather than the outcome.

**Scope.** Four values, nothing else. No adapter, no `--length`.

**Overrides.** Explicit wins, and both numbers reach the log:

```
Library preset 'emseq' selected: --clip_R1 12 --clip_R2 10 --three_prime_clip_R1 10 --three_prime_clip_R2 10
--clip_R1 12 was given on the command line and overrides the emseq preset value 10
```

**Reporting.** Preset name plus all four values in force, in both reports. Text:

```
Library preset: emseq
Clipping in force: --clip_R1 12 --clip_R2 10 --three_prime_clip_R1 10 --three_prime_clip_R2 10
--clip_R1 12 was given on the command line and overrides the emseq preset value 10
```

JSON, under `parameters.library` (`null` when no preset was used), each override carrying both numbers:

```json
"library": {
  "preset": "emseq",
  "clip_r1": 12, "clip_r2": 10,
  "three_prime_clip_r1": 10, "three_prime_clip_r2": 10,
  "overrides": [{"flag": "--clip_R1", "preset_value": 10, "user_value": 12}]
}
```

**Versioning and where the numbers live.** In the binary, in `src/library.rs`. The `CHANGELOG.md` entry states that preset values may change between releases, and the report records the expanded numbers, so an old run stays reproducible from its own record.

## Implementation note worth reviewing

Resolution is one function, `Cli::effective_clips()`, and every clip consumer reads it rather than `cli.clip_*`. That matters for three call sites in particular:

1. the trimmer config (`setup_trimming`),
2. the `--rename` + `--output-format ubam` clip guard, which now trips on a preset exactly as it does on the flags it stands for,
3. the `--rrbs` directional paired-end auto-clip. A preset that supplies `--clip_R2` suppresses it, on the same "already set" rule an explicit `--clip_R2` has always used. So `--rrbs --library pbat --paired` clips R2 by 8, not by 2. `--library` and `--rrbs` are not rejected as a combination, since I did not want to invent a conflict rule you had not asked for, but say the word if you would rather they were.

## Two small liberties, both easy to revert

- Alias `em_seq` on `emseq`, since nf-core/methylseq spells it that way and parity with that pipeline is the rationale for the numbers. Also `em-seq`, `single-cell`.
- `--clump_only` rejects `--library`, matching how it already rejects each of the four clip flags individually.

Specialty modes (`--hardtrim5/3`, `--clock`, `--implicon`) ignore `--library`, which is what they already do with explicit clip flags. I left that alone rather than adding a new refusal.

## Behaviour without `--library`

Trimming is unchanged and the text report is unchanged. The one difference anywhere is the new `"library": null` key in the JSON report (additive, `schema_version` untouched).

## Tests

Unit: the preset table verbatim from the issue, resolver precedence, flag parsing and every alias, unknown-name rejection, `--clump_only` refusal, and both report renderings.

`tests/integration_library.rs` is deliberately differential, because the defect class this feature can hit is "one dispatch path never reads the preset", which no unit test of the resolver catches:

- `--library accel` output is byte-identical to its four flags (paired, both mates)
- a preset is not a no-op (`--library scbs` output differs from no clipping), so the equivalence test above cannot pass vacuously
- an override's bytes follow the user's number, and the log names both
- both reports carry the block; a run without a preset carries neither
- an unknown kit name fails the run rather than trimming with no clipping

`cargo test`, `cargo fmt --all -- --check` and `cargo clippy --all-targets --release -- -D warnings` all clean.

## Docs

New page `guide/library-presets`, a cross-flag bullet in `guide/flags`, sidebar entry, and the `CHANGELOG.md` entry.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1595d5905839`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.