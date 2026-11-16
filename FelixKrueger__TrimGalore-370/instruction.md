# Issue

**Title:** fix(cli): honour -a2 with presets and auto-detection

## Description

Fixes the silently-dropped `-a2` reported in #369.

. (Not `Closes` — this targets `dev`, where auto-close does not fire; #369 needs a manual close after merge.)

## The reported defect

```console
$ trim_galore --paired --illumina -a2 AAATCAAAAAAAC R1.fq.gz R2.fq.gz
# R2 trimming report:
#   Command line parameters: … -a AGATCGGAAGAGC R2.fastq.gz     ← not the -a2 sequence
```

`-a2` was only ever applied when `-a` was also given. Adapter resolution is an early-return chain, and only the first branch read `cli.adapter2`; all five presets and the default auto-detect path returned a hardcoded Read 2 adapter and dropped the flag. Read 2 then fell back to Read 1's adapter, which is why `AGATCGGAAGAGC` appears rather than no trimming.

@MathieuUm found this after a 0.6.11 → 2.3.0 upgrade cost ~20% of the mapping rate and properly-paired alignments, and diagnosed it down to the report line.

## Two things the issue understated

**The scope.** Not an `--illumina` quirk — every preset *and* the default auto-detect path. `trim_galore --paired -a2 SEQ R1 R2`, with no adapter flag at all, also discarded it.

**The version.** Not a 2.3.0 regression: the `--illumina` branch is byte-identical at v2.1.0, v2.2.0 and v2.3.0, so downgrading within v2 is not a workaround.

## Design

Restores 0.6.11's contract — `unless (defined $a2) { $a2 = <preset default> }`: a user value wins, the preset only fills a default. The port reproduced the defaults and lost the override.

The override is applied in `setup_trimming`, `resolve_adapter`'s **single caller**, rather than by restructuring its seven branches. ~10 lines, and **no branch's Read 1 computation is in the diff** — so Read 1 cannot move structurally, not merely by test. The first draft of the plan reshaped every branch to fall through to one override point and booked "this touches the Read 1 path incidentally" as its main risk; moving up one frame deleted the risk instead of mitigating it.

Two deliberate exceptions to "`-a2` always wins", both discussed in the plan:

- **`--consider_already_trimmed` keeps precedence.** Trimming R2 while R1 is left alone would be asymmetric under a banner promising quality-trimming-only, so `-a2` is skipped with a warning. Suppression is detected from the R1 adapter being a single empty sequence — the only way it presents, which both reviewers verified by exhausting every producer in `adapter.rs`.
- **`-a` + preset stays permissive.** 0.6.11 rejects that combination, but it is the workaround recommended on #369, so it keeps working. Documented divergence.

## Also in this change

- `-a2` is validated on every path, so a malformed value is rejected rather than silently dropped — **except** in modes that have already announced they will ignore it (`--clock`, `--hardtrim5/3`, `--implicon`, single-end). Failing on an unused value would break pipeline templates that reuse one flag set across paired and single-end samples.
- Displacing a preset's own Read 2 default (`--small_rna`, `--bgiseq`) prints a NOTE naming what was not used.
- Single-end runs stop printing `Adapter 2 (Read 2):` for an adapter they will not use — including `--small_rna`/`--bgiseq` runs with no `-a2`, since those presets set a Read 2 default regardless of pairing.
- `A{N}` expansion, repeated `-a2`, and `-a2 file:adapters.fa` now work on every path. The docs and README described all three as supported since v2; they only ever worked alongside `-a`, which made two documented examples (`guide/adapters.md:31`, presented as "The cleanest (v2.x)") complete no-ops. Those become correct as written — no edit needed beyond a precedence hedge on `--small_rna`/`--bgiseq` in `flags.md` and `--help`.

## Behaviour change worth reviewing

**Trimmed output changes for anyone combining `-a2` with a preset or auto-detection — on both reads.** Read 1's own per-read trimming is untouched, but the joint pair-length filter retains a different set of pairs once Read 2 is trimmed correctly: 139 dropped instead of 4 on the BS-seq fixture. That is also the likeliest explanation for the reporter's mapping-rate drop, rather than R2 mis-trimming alone.

Verified unmoved for every invocation that does **not** pass `-a2`.

## Why the parity gate missed it

No case in the `validation` matrix passed `-a2` — a Perl-parity gate that never exercises a flag cannot notice the flag is ignored. This adds a case covering a preset and auto-detection, and it was run against a **pre-fix binary to confirm it fails there**. A gate that passes before the fix guards nothing.

## Verification

- **Tests 441 → 456**, including a new `tests/integration_adapter2.rs` (15 tests) that asserts the R2 adapter **per resolution branch**. A unit test of the override helper cannot catch this bug class — the defect was never "the helper computes the wrong answer", it was "six branches never called it".
- **The differential oracle**: post-fix `--illumina -a2 SEQ` and auto-detect `-a2 SEQ` are byte-identical to the pre-fix `-a AGATCGGAAGAGC -a2 SEQ` output, both reads. Needs no Perl and pins both reads at once.
- `cargo fmt --all -- --check` and `cargo clippy --all-targets --release -- -D warnings` clean.
- Reviewed by two independent code reviewers and a coverage audit before this PR, all read-only. **Four defects found and fixed**, the most significant being that single-end runs with a preset that has a Read 2 default printed contradictory stderr — a warning that `-a2` was unused followed by a NOTE that it had displaced the default. Two claims in my own notes were also corrected. One reviewer had `cutadapt 5.2` available and ran the new CI step against real Perl 0.6.11 (both legs byte-identical); the auditor rebuilt the pre-fix binary and ran all 25 `validation`-job invocations under both binaries (all identical). Full record in `plans/a2-ignored-with-presets/PLAN.md` §14.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427681058c8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.