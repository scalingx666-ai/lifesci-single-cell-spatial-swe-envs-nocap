# Issue

**Title:** docs(cli): mention bundled fastqc-rust in --fastqc / --fastqc_args help

## Description

## Summary

The `--help` text for `--fastqc` and `--fastqc_args` still described the old shell-out behaviour ("Run FastQC on the trimmed output files"). PR #226 landed the bundled fastqc-rust integration but the surface-level docstrings on the two flags weren't refreshed.

This PR brings the rendered `--help` into alignment with what the binary actually does:

- **`--fastqc`** — explicitly states the integration is built in via the bundled fastqc-rust library, no Java / external FastQC binary needed, and that the artifacts are FastQC 0.12.1-compatible HTML/ZIP.
- **`--fastqc_args`** — enumerates the translated flag subset (`--nogroup`, `--expgroup`, `--quiet`, `--svg`, `--nano`, `--nofilter`, `--casava`, `-t/--threads`, `-o/--outdir`) so users see the supported set without reading source. Matches the dispatch table in `src/fastqc.rs:74-87`.

Also picked up two `docs/SUMMARY.md` polish lines that were drafted alongside #226 but missed that merge:
- Architecture-shift paragraph now flags Java + FastQC tarball as part of what the Perl wrapper required, and the static-binary outcome ("No Java, no Python, no Cutadapt, no external FastQC: the runtime is one static binary").
- Parity-table row for `--fastqc / --fastqc_args` annotated "(bundled via fastqc-rust — no external Java/FastQC needed)".

Pure docstring/markdown change. Zero runtime delta.

## Rendered `--help` (after)

```
      --fastqc
          Run FastQC on the trimmed output files (built in via the bundled
          fastqc-rust library; no external Java or FastQC binary needed).
          Produces FastQC 0.12.1-compatible *_fastqc.html / *_fastqc.zip
          artifacts

      --fastqc_args <FASTQC_ARGS>
          Additional arguments to pass to FastQC. Implies --fastqc. Common
          flags are translated to the bundled engine: --nogroup, --expgroup,
          --quiet, --svg, --nano, --nofilter, --casava, -t/--threads,
          -o/--outdir. Unrecognised flags emit a warning and are ignored
```

## Test plan

- [x] `cargo build --release` clean
- [x] `cargo test --release --lib fastqc` — 8/8 pass (translator unit tests)
- [x] Visual spot-check of `./target/release/trim_galore --help` for the two flags
- [x] Translator-flag list in docstring matches `src/fastqc.rs:74-87` exactly
- [ ] CI green (clippy + fmt + full test matrix)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `454d432ba935`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.