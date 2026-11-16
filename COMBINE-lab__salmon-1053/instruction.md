# Issue

**Title:** chore(cli): tidy help output (hide removed `alevin`, drop "Rust port")

## Description

## What

Two small cosmetic cleanups to the top-level `salmon --help` output:

1. **Hide the removed `alevin` subcommand.** It was listed as a real command whose only description was that it had been removed, which reads as clutter. The variant is now `#[command(hide = true)]`, matching the already-hidden `swim` command, so it no longer appears in the command list.
2. **Drop the `(Rust port)` parenthetical** from the `about` string, so the header reads simply `RNA-seq transcript quantification`.

Also refreshes a stale module doc comment that still described `alevin` as "stubbed for later phases" (it is a permanent redirect).

## Behavior is unchanged

`salmon alevin ...` (and `salmon alevin --help`) still parse and still emit the alevin-fry redirect before logging init, exiting 1. The migration hint for genuinely unknown subcommands is unaffected.

Before / after `salmon --help`:

```
  debug-map   Diagnostic: per-read best-mapping detail (placement, seed coverage, score)
- alevin      Single-cell quantification (removed; redirects to alevin-fry)
  help        Print this message or the help of the given subcommand(s)
```

## Testing

- `cargo build -p salmon-cli`
- `salmon --help` no longer lists `alevin`; header no longer says "(Rust port)"
- `salmon alevin foo` and `salmon alevin --help` both still print the redirect and exit 1
- `salmon bogus` still prints the migration hint

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66f3d3cdaeb9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.