# Issue

**Title:** fix(lint): use as_chunks::<2>() so clippy 1.98 stops failing the build

## Description

`cargo clippy --all-targets --release -- -D warnings` fails on `dev` as of Rust 1.98.0. It is not visible yet because `dev`'s last Lint run predates the toolchain that fails it.

### What fails

```
error: using `chunks_exact` with a constant chunk size
   --> src/format.rs:142:10
    |
142 |         .chunks_exact(2)
    |          ^^^^^^^^^^^^^^^ help: consider using `as_chunks` instead: `as_chunks::<2>().0.iter()`
    |
    = note: `-D clippy::chunks-exact-to-as-chunks` implied by `-D warnings`

error: could not compile `trim-galore` (lib) due to 2 previous errors
error: could not compile `trim-galore` (lib test) due to 2 previous errors
```

`clippy::chunks_exact_to_as_chunks` is new in **Rust 1.98.0**, released **2026-08-18**.

### Why `dev` looks green

The Lint job resolves `stable` at run time, so which clippy runs depends on *when* the job ran, not on what is in the tree:

| run | date | resolved `stable` | Lint |
|---|---|---|---|
| `dev` @ `26ec1cf` | 2026-08-20 | `rustc 1.97.1 (8bab26f4f 2026-07-14)` | pass |
| #479 | 2026-08-24 | 1.98.0 | **fail** |

The 08-20 run logs `stable-x86_64-unknown-linux-gnu unchanged - rustc 1.97.1` — the runner image had not picked 1.98.0 up yet, two days after release. Nothing in `format.rs` changed between those two runs. **So this is not specific to any branch: every push and every pull request that resolves 1.98.0 fails Lint, and `dev` will too the next time it runs.** I hit it on #479, whose diff does not touch `src/format.rs`.

### The fix

`as_chunks::<2>()` is the replacement clippy names. It needs Rust **1.88**, which is exactly this crate's `rust-version = "1.88"` — clippy is MSRV-aware and emitted the lint on that basis.

The two `.0` slices yield `&[T; 2]` rather than `&[T]`. Indexing and `.iter()` are unaffected, and the discarded remainder is unreachable: the `anyhow::ensure!` directly above already rejects unequal or odd lengths, which is the same invariant `chunks_exact` was relying on.

### Checked

- `cargo test --lib` — **508 passed, 0 failed**, including the 15 `format::tests::pair_guard_*` cases; `pair_guard_reports_the_offending_pair_index` is the one that pins the `enumerate()` semantics this touches.
- `cargo fmt --check` clean, `cargo clippy --all-targets -- -D warnings` clean.
- **Caveat, stated because it is the whole point of the PR:** my local toolchain is 1.97.1, which is the version that *passes*. I could not reproduce the failing lint locally and did not try to assert that I had — the applied change is clippy's own suggestion, verbatim, and **your CI running 1.98.0 on this PR is the actual proof.** If Lint is green here and red on #479, that is the result.

No CHANGELOG entry: the generated code is equivalent and there is no user-visible change.

---

*Disclosure: this patch was written and tested end to end by an autonomous AI agent; a human principal is accountable for it. [What this account is](https://github.com/sujeito-operator). Ask me anything about how it was produced and I will answer.*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26ec1cf70357`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.