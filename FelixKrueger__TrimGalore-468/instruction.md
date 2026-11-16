# Issue

**Title:** fix(clump): report the encoding the clumping banners write, not the configured level

## Description

Settles the remaining half of #453 — the messaging. The flag question was decided separately and is not changed here: **`--clumpify --dont_gzip` stays refused, `--clump_only --dont_gzip` stays supported.**

**Two banners claimed a compression they were not applying.**

`--clumpify` on a plain input — output encoding follows the input's, so this run writes plain text:

```
clumpify: 16 bins × 22 MiB; predicted peak ≈ 930 of 1024 MiB budget (gzip level 1)   ← before
clumpify: 16 bins × 22 MiB; predicted peak ≈ 930 of 1024 MiB budget (plain output)   ← after
WARNING: the output is not compressed, so --clumpify's reordering gains nothing here — output
encoding follows the input's. Supply gzipped input, or drop --clumpify to skip the memory reservation.
```

`--clump_only --dont_gzip` — the level and the flag disabling it, side by side, while its own report printed `1926073 bytes -> 1926073 bytes` two lines later:

```
(16 bins × 26 MiB each; predicted peak ≈ 930 of 1024 MiB budget, gzip level 1, --dont_gzip)  ← before
(16 bins × 26 MiB each; predicted peak ≈ 930 of 1024 MiB budget, plain output)               ← after
```

The `--clumpify` case is a warning rather than a refusal because, unlike the flag combination, it is reachable without asking for it: the bin pool's reservation has been paid for output that differs from the input only in record order.

**Not cosmetic.** Peak-RSS measurements during #439 were taken against the `--clumpify` banner rather than the output filenames, and the readings had to be retracted once a plain-output run turned out to have been misread as gzipped.

**The structural half matters more than the strings.** `io::output_is_gzipped` is now the single source for "will this run write gzip", read by both the banner and the writers at `main.rs:424`; `clump_only::banner_encoding` does the same for the two `--clump_only` sites. Duplicating those decisions is what let the messages and the behaviour disagree.

**The gzipped banners are byte-unchanged**, so the `clumpify-memory` CI job's parse and the tripwire's `predicted peak ≈ 930 of 1024 MiB budget` assertion are untouched.

**Guards, each proven able to fail.** The existing `se_trim_clumpify` tripwire case turned out to run on a plain input already, so it had been exercising the false banner silently for as long as it existed; it now pins `(plain output)`, the absence of `gzip level`, and the warning. A new `dont_gzip_banner_does_not_name_a_compression_level` covers the `--clump_only` side. Reverting either banner to report the configured level turns the respective test red — checked, not assumed. Plus a unit test on `output_is_gzipped` across all four flag/extension combinations.

504 lib tests, all suites green, fmt and clippy clean, docs build clean.

`--clump_only --dont_gzip` is documented as deliberately supported in `modes/clump-only.md` — reordering is the whole job there, and clumped plain output still compresses better under whatever tool runs next — so the asymmetry with `--clumpify` reads as intentional rather than as an oversight to "fix".

Rebased over #464, keeping both `### Unreleased` bullets.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f98261d38b67`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.