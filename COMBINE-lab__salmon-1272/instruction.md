# Issue

**Title:** fix(quant): write a right orphan's SAM/BAM record on its own strand

## Description

Every orphan keeps its strand in `is_fw` and leaves `r2_fw` false, but the right-orphan branch read `r2_fw`. A forward R2 orphan was written with FLAG 0x10 and a reverse-complemented SEQ at the forward position.

Compile-checked only: this PR has no regression test yet.

## How it was found

Found via [Ponytail](https://github.com/DietrichGebert/ponytail)'s repo audit (`/ponytail-audit`), run with Claude Code over the 2.10.0 code. The audit compared the right-orphan branch of `emit_fragment_records` with the orphan constructors in `mapper.rs` and `sketch.rs`, which all set `r2_fw: false` and keep the strand in `is_fw`. The existing SAM-vs-BAM test could not catch this, because both writers share the code. This one came from reading the code, not from a run. Tracked in #1283 (finding 9).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd36f3b3cfb8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.