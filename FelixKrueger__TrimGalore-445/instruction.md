# Issue

**Title:** fix(cli): refuse --library where clipping cannot apply, and gate R2 reporting

## Description

`--library` was accepted and then silently ignored by the four specialty modes, and the trimming report's `Clipping in force:` line named Read 2 clipping on single-end runs where none can apply. Both are fixed: the flag is now refused with `--hardtrim5`, `--hardtrim3`, `--clock` and `--implicon`, and the report lists only the values that applied. A run passing no `--library` is byte-identical to before, `--rrbs` is untouched, and the JSON report is unchanged. This lands before `--library` ships, so neither fix is a breaking change.

Closes the two findings both reviewers of #441 agreed on.

<details>
<summary>Verification and follow-ups (AI-assisted detail — keep or bin)</summary>

**Wording.** The messages say "does not honour the clip flags" rather than "does not clip". All four modes do clip — `specialty.rs` calls `clip_5prime`, and its doc comments describe clipping at fixed positions — but none of them reads `--clip_R1` / `--clip_R2` / `--three_prime_clip_*`.

**Tests.** 12 new, 764 passing, `cargo fmt --check` and `clippy -D warnings` clean. Every new test was checked to fail without the code beneath it, via a 12-row mutation matrix. Six seams previously survived the whole suite: a swapped key label inside the JSON `library` block, a swapped label among the top-level clip keys, a swapped override flag label, a deleted `library` key, a block disagreeing with the top level, and a reverted #408 `--rename` guard.

**Byte-identity.** Differential against `872c4ae` across five invocation shapes (24 files compared): every FASTQ output and every `.txt` report identical; JSON identical apart from `command_line`, which records the binary path.

**Reporting asymmetry, deliberate.** The text report lists the values in force for the run; the JSON keeps all four. Gating the JSON would contradict the block/top-level agreement this PR asserts, and the top-level `clip_r2` cannot change without a schema break. Consumers distinguish the cases with the top-level `mode` key.

**Follow-ups, not addressed here:**

- On a single-end run, `--library emseq --clip_R2 5` prints the gated `Clipping in force:` line and then an ungated override line naming `--clip_R2 5`, which reads as though it applied. `cli.rs:1056` already warns for `-a2` on single-end input while `--clip_R2` gets nothing; one `validate()`-time warning for the clip-R2 family would fix the preset and non-preset cases together.
- Only one of the four precedence relations the refusal depends on is pinned by a test.
- The refusal covers `--library` but not the four primitive clip flags it expands into, which remain silent no-ops in the specialty modes (pre-existing).
</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `872c4ae42484`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.