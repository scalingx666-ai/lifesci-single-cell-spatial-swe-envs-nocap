# Issue

**Title:** Print help (exit 0) on bare invocation instead of a required-args error

## Description

## Problem

Running `trim_galore` with no arguments currently fails with clap's terse required-argument error on **stderr** and a **non-zero** exit:

```
$ trim_galore
error: the following required arguments were not provided:
  <INPUT>...

Usage: trim_galore <INPUT>...

For more information, try '--help'.
```

Most modern CLIs (samtools, git, bwa, cargo, docker…) instead print their full help on a bare invocation. This PR makes `trim_galore` do the same.

## Change

- Set `arg_required_else_help = true` so clap resolves the no-args case to a help outcome rather than a missing-argument error.
- Route clap's help/version outcomes (including this one) to **stdout** with **exit 0** via a `try_parse_from` handler in `main`. Genuine usage errors (unknown flag, `--paired` with no input files, etc.) still fail loudly on **stderr** with a **non-zero** exit.

```
$ trim_galore            # now: full help on stdout, exit 0
$ echo $?
0
```

- Also tidied the `--help` text: dropped developer-internal references (legacy Perl `v0.6.x` version notes and internal `PLAN.md` / section pointers) that had leaked into user-facing flag descriptions. No behaviour change.

## Tests

- A clap-layer unit test (`cli.rs`) locks the no-args → help outcome.
- A binary-driven integration test (`tests/integration_no_args_help.rs`) asserts exit 0 + help on stdout + empty stderr end-to-end.
- Full suite green (`cargo test`: 331 unit + integration), `cargo fmt --check` and `cargo clippy -D warnings` clean.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5a5fcb9b142`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.