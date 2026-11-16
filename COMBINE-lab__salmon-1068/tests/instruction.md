# Issue

**Title:** chore(deps): full dependency refresh ahead of 2.4.0

## Description

Complete dependency refresh for 2.4.0, in two passes: the first before the COMBINE-lab upstreams were published, the second after.

## ⚠️ Correction to an earlier claim in this PR

An earlier revision of this description said `sha2` 0.10 → 0.11 was applied and verified output-neutral. **That was wrong.** The bump changed `[workspace.dependencies]`, but `salmon-index` declared `sha2 = "0.10"` *literally* rather than `{ workspace = true }`, so the member declaration shadowed it — the lock stayed on 0.10.9 and the workspace entry was dead. The verification ran, but sha2 was never part of what it tested.

`salmon-index` now inherits from the workspace, sha2 0.11 is genuinely in the lock, and the index-hash check has been re-run against the real thing (unchanged). An audit of all 11 manifests found no other shadowed workspace dependency.

## Semver-compatible

13 direct dependencies, 111 crates including transitives: `anyhow` · `clap` · `crossbeam-channel` · `crossbeam-queue` · `indicatif` · `jiff` · `libradicl` · `paraseq` · `rand` · `serde` · `serde_json` · `thiserror` · `xxhash-rust`

## Semver-incompatible

| dep | | notes |
|---|---|---|
| `libradicl` | 0.14.2 → **0.15** | requirement widened; `^0.14` excludes it |
| `noodles-sam`/`-bam`/`-bgzf` | → **0.87 / 0.92 / 0.49** | see BGZF section |
| `needletail` | 0.6 → **0.7** | |
| `sha2` | 0.10 → **0.11** | see correction above |
| `indicatif` | 0.17 → **0.18** | |
| `scc` | 2 → **3** | |
| `statrs` | 0.18 → **0.19** | |
| `criterion` | 0.5 → **0.8** | benches only |
| `bramble-rs`/`cf1-rs`/`sshash-lib` | → **0.1.7 / 0.5.1 / 0.6.2** | |

Everything is now single-version — the noodles and needletail duplication earlier revisions deferred is resolved, unblocked by publishing bramble-rs 0.1.7, libradicl 0.15.0, cf1-rs 0.5.1 and sshash-lib 0.6.2.

`indicatif` was declared 0.17 while `piscem-rs` already used 0.18, so both were built. Moving to 0.18 unifies them and drops `number_prefix`, clearing RUSTSEC-2025-0119.

## BGZF thread control had to be reimplemented

noodles 0.48 deprecated `MultithreadedReader/Writer::with_worker_count` and made it a **no-op** — the parameter is discarded and block work goes through `rayon::spawn`, i.e. `Registry::current()`. Left alone, compression would land on salmon's global rayon pool (sized to `-p`, already mapping), and both the derived worker count and `--bamCompressThreads` would control nothing, while still compiling and passing every test.

This was not avoidable by declining the bump: `bramble-rs = "0.1.6"` is a caret requirement, so any `cargo update` pulls 0.1.7 → noodles 0.113 → bgzf 0.49.

All four call sites (the `--writeBam` writer plus three `MultithreadedReader` sites in salmon-align) now run inside a dedicated rayon pool via a shared `with_bgzf_pool` helper, which also keeps BGZF work off the mapping threads — something the old API did implicitly.

The pool is sized **`workers + 1`**: `install` runs the driver loop *on* a pool worker while noodles spawns compression into the same pool and its ordering thread blocks awaiting the result, so a pool sized exactly to the worker count has nothing left to compress on. That deadlocked outright at `--bamCompressThreads 1` (26 min wall, 3 s CPU) before the reservation was added.

Both problems reported upstream: **zaeleus/noodles#409**.

### Enforcement verified by measurement

2.4M fragments, `-p 16`, mapping-phase seconds, best of 5, ratios against a no-BAM baseline measured in the same session:

| | this PR (bgzf 0.49) | before (bgzf 0.47) |
|---|---|---|
| baseline | 3.145 s | 2.722 s |
| `--bamCompressThreads 1` | **1.77×** | 2.08× |
| 2 | **1.00×** | ~1.0× |
| 4 | **1.02×** | ~1.0× |
| default (auto → 6) | **1.05×** | ~1.0× |

The C=1 cliff is restored; flat rows would have meant the pool wasn't taking effect. Isolated benchmarking over 1 GiB confirms noodles 0.49 is **not** slower than 0.47 — 169.3 vs 168.6 MiB/s at 1 worker, 1336 vs 1340 at 8, i.e. within 1% throughout.

## Validation

| check | result |
|---|---|
| index provenance (9 hash/param fields) | **unchanged** |
| `quant.sf` `--deterministic` | **byte-identical** |
| `quant.sf` default threaded | max Δ **0** |
| `bootstraps.gz` (12) | **byte-identical** |
| Gibbs samples (12) | **byte-identical** |
| `fld.gz` (`statrs` normal CDF) | **byte-identical** |
| BAM output under noodles 0.49 | valid |
| `cargo test --workspace --release` | 27 binaries, 0 failures |
| fmt / clippy | clean / 9 warnings, same as the pre-existing set |

## Cleanup

`ndarray` and `nalgebra` dropped from `[workspace.dependencies]` — no member crate referenced either (`nalgebra` is in the lock only via `statrs`), so both were dead declarations producing phantom "update available" entries.

## Deferred

`rand_pcg` 0.3 → 0.10 and `rand_distr` 0.4 → 0.6 go in a stacked PR, since they shift Gibbs sampling.

Remaining advisories are all transitive with no fixed version: `bincode` ← libradicl, `derivative` ← **sux 0.14**, `proc-macro-error2` ← impl-tools ← sux. sux 0.15 would clear the latter two but is unpublished.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01R5jNNvJnFRiu2eC1JZAu2T

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49652936fa4f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.