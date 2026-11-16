# Issue

**Title:** fix(cli): accept non-UTF-8 arguments instead of panicking

## Description

## Problem

`main()` read its arguments with `std::env::args()` in four places (`src/main.rs` argument parsing, the `command_line` for `@PG CL:`, and the single-end and paired report writers). `std::env::args()` panics on any argument that is not valid UTF-8. A Unix file name can be arbitrary bytes, so:

```
$ trim_galore $'\xff.fq'
thread 'main' panicked at library/std/src/env.rs:...
$ echo $?
101
```

## Fix

- `main()` reads the arguments once with `std::env::args_os()`.
- `rewrite_perl_short_flags` (`src/cli.rs`) now takes and returns `OsString`. It only rewrites tokens that are UTF-8 (`-r1`, `-r2`, `-a2` are ASCII, so a non-UTF-8 token can never be one of them) and passes the rest through to clap. clap already handles `OsString`: a non-UTF-8 value for a `String` option is a normal usage error, and `PathBuf` inputs accept it.
- `command_line` is built once from those arguments with `to_string_lossy` and passed down to `run_single_file`, `run_paired`, `run_paired_ubam_single_file` and `write_paired_reports`, which used to re-collect `std::env::args()` themselves.

After the fix:

```
$ trim_galore $'\xff.fq'
Error: Input file not found: �.fq
$ echo $?
1
```

## Testing

- New integration test `tests/integration_non_utf8_args.rs` (`#[cfg(unix)]`): `non_utf8_file_name_gets_a_normal_error_not_a_panic` runs the binary with the file name `b"\xff.fq"` and asserts exit code 1, no panic, and the lossy name in the error. Without the fix it fails with exit 101 and a panic in `std::env`.
- The existing `test_rewrite_*` unit tests for the Perl short-flag rewrite still pass (helper changed to build `OsString`).
- `cargo test`: all pass. `cargo clippy --all-targets --release -- -D warnings`: clean. `cargo fmt --all -- --check`: clean.

Not tested: a run on an existing file with a non-UTF-8 name (macOS APFS refuses to create one). Other code paths that call `to_str()` on such a path were not audited.

## Byte-identity

No output change for UTF-8 command lines: `command_line` is the same space-joined string as before. For a non-UTF-8 argument the report shows U+FFFD in its place (previously the program panicked).

## Suggested CHANGELOG entry

- **A non-UTF-8 argument no longer crashes Trim Galore.** Arguments were read with
  `std::env::args()`, which panics on bytes that are not UTF-8, so a file name such as
  `$'\xff.fq'` ended in a Rust panic and exit 101. Arguments are now read as OS strings and the
  report's `command_line` shows any invalid bytes as U+FFFD.

Part of #546 (finding 12 of the ponytail audit).

🤖 Generated with [Claude Code](https://claude.com/claude-code) using [ponytail](https://github.com/DietrichGebert/ponytail)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7e7a19e1e37`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.