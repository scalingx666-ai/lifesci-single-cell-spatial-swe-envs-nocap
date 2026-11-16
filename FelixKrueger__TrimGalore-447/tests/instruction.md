# Issue

**Title:** fix(cli): warn when a clip flag cannot be honoured, and stop announcing it

## Description

A clip flag a run cannot honour was accepted and dropped in silence, and the trimming report still announced a Read 2 override on single-end runs even after #445 stopped it listing Read 2 values as in force. Both are fixed: an inert clip flag now warns with a reason true for that mode, and neither the log nor the text report announces a Read 2 clip the run did not perform. Paired output is byte-identical and the JSON report is unchanged.

Closes the two findings from the review of #445, and the user-visible half of a third.

<details>
<summary>Verification and one open item (AI-assisted detail — keep or bin)</summary>

**Why the previous fix was incomplete, in the words of the convention it copied.** `tests/integration_adapter2.rs:414-422` records an earlier version of the `-a2` fix which "gated the `Adapter 2 (Read 2):` line but not the NOTE, so a single-end run warned that `-a2` was unused and then announced that `-a2` had displaced the preset default." Substituting the clip vocabulary describes #445 exactly. `-a2` treats that as the bug and fixes it by gating both.

**The two inert sets differ**, which is why a single `!paired` predicate can't express this: the specialty modes read no clip flag at all, so all four are inert there, while a single-end run honours the Read 1 pair. A bare `!paired` test told a two-file `--clock` run "this is a single-end run" — which sends the user to add `--paired`, silencing the warning without making the flag work. The reason comes from a ladder in `-a2`'s order, specialty modes first.

**Wording.** The messages say the modes *do not honour the clip flags* rather than that they do no clipping, because they clip at fixed positions of their own (`specialty.rs` calls `clip_5prime`).

**`ClipOverride` carries which read it belongs to**, set at its construction sites rather than parsed from the flag name — a string-matched name is invisible to a label swap. A test uses the name as an independent oracle so the two lists cannot drift.

**Tests.** 13 new, 781 passing, `cargo fmt --check` and `clippy --all-targets --release -D warnings` clean. Each new test was verified to fail without the code beneath it, including **each gate reverted separately**, so neither surface can regress silently. Two branches that initially shipped green — the Read 1 narrowing, and the `--three_prime_clip_R1` entry — are now covered; the mode table carries both flags of each inert set rather than one representative.

**Byte-identity.** Differential against `fdade7e` over five shapes: every FASTQ and every `.txt` identical on all paired shapes, JSON identical apart from `command_line`. The only behavioural output change anywhere is one line, on single-end runs that override a Read 2 flag.

**Reporting asymmetry, deliberate.** The text report lists what applied; the JSON records what was requested, with the top-level `mode` key to discriminate. Gating the JSON would break the block/top-level agreement invariant #445 introduced.

**Open, not addressed here:** a single-end `--rename --output-format ubam --clip_R2 5` run warns that `--clip_R2` is ignored and is then refused *because* `--clip_R2` is set — the #408 guard at `main.rs:398` counts an inert Read 2 flag. The over-refusal is pre-existing; this PR's invariant is what makes it read as a contradiction. Narrowing that guard changes a data-safety refusal, so it wants its own decision.
</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fdade7efb8b5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.