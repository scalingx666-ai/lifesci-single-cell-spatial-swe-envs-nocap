# Issue

**Title:** fix(infer): skip target-less equivalence classes instead of panicking

## Description

Several salmon-infer code paths assumed that a class which isn't multi-target has exactly one target, and read its first target:
- the four M-step kernels (EM and VBEM, sequential and parallel);
- the final truncation step;
- the Gibbs sampler;
- `ambiguity_counts`.

`PackedEqClasses` has public fields, so an external caller can build a class with no targets. piscem-infer did exactly that: a fragment whose every mapping failed its strand filter became an empty class. That made the salmon-infer EM port in COMBINE-lab/piscem-infer#35 panic (index out of bounds in `em_step_par`) on every stranded library.

salmon's own producers are unaffected. The reads, alignment and RAD paths, and the naive seed builder, all drop such fragments before building classes. This change only hardens the library for other callers.

**Fix:** an empty class carries no assignable evidence, so it's now skipped. The truncation step reports its count as dropped mass. The only new code is a length check the kernels already make, so there's no runtime cost.

**Test:** `empty_classes_are_skipped_everywhere` inserts an empty class and checks that the results match the run without it for:
- EM and VBEM;
- no acceleration, SQUAREM, and DAAREM (EM only);
- sequential and parallel.

It also runs `ambiguity_counts`, Gibbs sampling and bootstrap on the same input. Without the guards it panics at `packed.rs:384`. With them, `cargo test -p salmon-infer` passes (32 tests) and clippy is clean.

**Also:** corrects `EmAccel::Squarem`'s docs. The "same fixpoint" promise holds for plain EM, but not under VBEM, whose objective has many optima.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Xg1hUw9i95rJikA6eL2WNH

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e54211e241a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.