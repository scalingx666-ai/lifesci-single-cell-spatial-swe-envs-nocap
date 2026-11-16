# Issue

**Title:** refactor(io): make norm_path private and re-home the fold trade-off

## Description

`io::norm_path` was `pub` with no callers outside `io.rs` — and that public name is what let #389's planning mistake it for a stale alias of `collision_key`. It is now module-private, so the compiler enforces what a doc comment previously only suggested.

The case-folding trade-off note moves to `collision_key` in the same change. `norm_path` is a pure `to_ascii_lowercase` of a string, so "may false-positive" was never a property of it — false positives are a property of *deciding output collisions on a folded key*. Without the move, privatization would have deleted the only statement of that trade-off from the rendered docs. `collision_key` also gains the pointer to the case-preserving `path_identity_key`, which is exactly the distinction #389 got wrong.

`pub(crate)` was considered and rejected: `specialty.rs` and `clump_only.rs` both alias `crate::io as naming`, so it would keep the symbol reachable as `naming::norm_path` from precisely the modules whose readers this protects.

Verified with a positive control on this branch — an external caller planted in `tests/` raises `E0603` under `cargo check --all-targets`, while plain `cargo check` passes (it never compiles `tests/`), so the guard is the `--all-targets` run and not `cargo build`. 561 tests green; the fold stays pinned by `test_norm_path_case_folds`.

<details>
<summary>AI-assisted: plan, dual plan review, and what they corrected</summary>

Plan + reviews in `plans/08082026_normpath-visibility/` (committed separately). Both reviewers approved with no Criticals, each having compiled the demotion in an isolated copy with positive controls. They corrected three justifications in the original plan: `dead_code` cannot fire here (`collision_key` calls the function), `cargo build` is not the safety net, and the claim that this repo doesn't changelog internal work was false — it has an `Infrastructure (contributor-facing)` section. The entry is still skipped, on better grounds: the changelog has never named these three helpers across the entire #216/#383/#384/#388/#389/#391 arc.

Follow-up filed: #402 (declare `lib.rs`'s 17 uncurated `pub mod` surface an implementation detail, since the crate publishes to crates.io and every future demotion re-raises the semver question).
</details>

 (manual close needed — dev is not the default branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac08a97025bb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.