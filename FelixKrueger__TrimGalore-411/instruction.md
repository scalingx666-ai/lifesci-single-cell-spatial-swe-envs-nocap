# Issue

**Title:** chore: housekeeping batch — rustdoc, help text, lib.rs surface, changelog (#401 #402 #405 #407)

## Description

Four accumulated documentation/hygiene items in one round. No behaviour change; `cargo doc` goes from **12 errors to 0**.

- **#405** — ten of the twelve rustdoc errors were invisible to users (the six `[Deprecated]` links all carry `hide = true`; plus `R1[i]`, `match_len`, and `alignment.rs`'s link to the private `myers_proves_no_match`). **Two were not:** the hardtrim help renders `.<N>bp_5prime.fq(.gz)` literally, and `<N>` is exactly what rustdoc reads as an unclosed HTML tag — so those are now backticked, matching the convention the rest of `cli.rs`'s help already uses. **This is the one user-visible change in the PR; say if you'd rather drop the angle brackets instead.**
- **#407** — `--preserve-tags`' help said only "Ignored for FASTQ input" while the flag is a hard *error* combined with `--output-format ubam`. Clause added.
- **#402** — `lib.rs` gained a module doc stating its surface is an implementation detail with no semver guarantee.
- **#401** — the CHANGELOG's "All four now use the same key as the pre-flight" was stale (D13 split the key; #389 refined the `--passthrough` half). Corrected to describe both keys and why they differ.

561 tests green, rustdoc clean, fmt + clippy clean.

<details>
<summary>AI-assisted: why #401's unit guard is Linux-gated, and how it was verified without Linux</summary>

**The four-line test specified in `CODE_REVIEW_D13` — and copied verbatim into #401 — cannot run.** `validate()` checks input existence, so the nonexistent paths never reach the identity check; it fails with "Input file not found". A real-file version cannot run on macOS either: `Sample_R1.fastq.gz` and `SAMPLE_R1.fastq.gz` are **one file** on APFS (verified — the second write silently overwrote the first), so the four distinct files this needs cannot exist here at all.

So the guard is `#[cfg(target_os = "linux")]`, creates four real files, and **asserts the filesystem actually kept them distinct before trusting its own assertion** — otherwise it would pass vacuously on any case-insensitive volume.

Since it is `cfg`'d out locally it had never compiled, and I wasn't willing to push an unverified test: I temporarily retargeted it to `macos`, where it compiled and failed on exactly that premise check (`expected 4 distinct files, filesystem gave 2`), then restored the Linux gate. So the test is known to compile and known not to be vacuous; its final assertion runs first on CI's ubuntu leg.

No `cargo doc` CI gate is added here. Without one the next broken link accumulates silently — which is how these twelve arrived. Worth its own issue if wanted.
</details>

 (manual closes needed — dev is not the default branch).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `90dda11c1f58`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.