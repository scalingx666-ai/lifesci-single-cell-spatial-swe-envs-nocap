# Issue

**Title:** fix(cli): the two #1162 items that #1166 dropped

## Description

Closes the remainder of #1162.

I verified all seven items against a build of `develop` rather than against #1166's description. **Five were done. Two had never been touched** — and neither appears in #1166 at all, as a fix or as a deferral. Groups 4+5 were staged across five parallel agents and I never reconciled the assembled result against the tracking issue's table, which is what you had asked for.

| # | item | status before this PR |
|---|---|---|
| 1 | `-a --gcBias` without `-t` | done in #1166 |
| 2 | FASTQ errors name no file/record | **path** done in #1166; record identifier upstream |
| 3 | `--rad` unwritable `-o` | **never touched** |
| 4 | `-2` without `-1` | done in #1166 |
| 5 | `--decoyThreshold` sketch warning | done in #1166 |
| 6 | single-flag plural verb | **never touched** |
| 7 | `--skipQuant --dumpEq` | done in #1166 |

## Item 3 — `--rad` with an unwritable `-o`

It read the whole RAD and ran the entire EM before failing, with no path in the message. Measured on the 26M-fragment benchmark:

| | elapsed |
|---|---:|
| failing run (unwritable `-o`) | 12.74 s |
| successful run, same command | 12.81 s |

`rad_read` 2.09 s + `em_bias` 10.54 s — so the failure landed after all the work was done and discarded. Now:

```
Error: creating output directory /…/ro3/out (needed before quantification; check that it is writable)
Caused by: Permission denied (os error 13)
```

at **0.00 s**. The reads, alignment and genome-projection drivers already did this; the RAD driver was the only one that did not.

It creates `aux_info` rather than just the output directory. Creating only the parent still succeeds when `-o` exists but is read-only — the likelier way to hit this — and `aux_info` is the write that actually failed. Both cases now fail at 0.00 s; I tested them separately.

## Item 6 — single-flag warnings in the plural

`warn_inert_in_mode` conjugated its *subject* correctly but the reason clause came from callers with a hard-coded "they":

```
before: --decoyThreshold has no effect in RAD-input mode (--rad): they configure salmon's read mapper…
after:  --decoyThreshold has no effect in RAD-input mode (--rad): it configures salmon's read mapper…
after:  --sketch, --decoyThreshold have no effect in …: they configure salmon's read mapper…   (unchanged)
```

Nine call sites, including one carrying the mirror-image defect — a hard-coded *singular* `"it thins a Gibbs chain"`. Agreement now belongs to the helper, which takes the verb as an explicit `(singular, plural)` pair rather than appending an `"s"` to a stem, so an irregular verb cannot be mangled later.

It is deliberately optional (`Option<(&str, &str)>`): two reasons supply their own subject — the mode (`"it writes no intermediate RAD"`) and a noun phrase (`"posterior sampling happens …"`) — and forcing a pronoun onto those would have produced *"it it writes no intermediate RAD"*. Those pass `None` and are used verbatim.

**How it survived:** the helper's own doc comment claimed singular and plural were handled and cited the exact failing example, while only the subject half had been implemented. Every existing test that exercised it happened to pass more than one flag. The message construction is now split into `inert_in_mode_message` so the agreement rules are asserted directly rather than inferred from a log line.

## Correction on item 2

My first report said mid-file FASTQ errors named no file. That was wrong — a grep filter of mine hid the line. #1166 did chain the path, and it works on the mid-file case:

```
Error: deterministic mapping pass failed
Caused by: 0: while reading /…/mid.fq
           1: mapping failed: FASTX error: Invalid FASTQ separator: X, expected '+'
```

Only the **record identifier** is missing, and that is genuinely upstream: paraseq's error carries no record identity. #1162 should stay open for that one item, or be closed with it re-filed against paraseq — your call.

## Tests

Four new, three of them unit tests on the extracted message builder (singular, plural, own-subject verbatim, and silence when nothing was passed), plus an end-to-end test that an unwritable `-o` fails **before** the RAD is read. That last one deliberately uses an invalid RAD: if the check ever moves back after the read, the test fails with a parse error instead of the directory error.

`cargo fmt`, `cargo clippy --workspace --all-targets -D warnings`, and `cargo test --workspace --release` all clean.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1d50be518813`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.