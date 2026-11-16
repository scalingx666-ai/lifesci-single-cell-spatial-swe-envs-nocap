# Issue

**Title:** CheckM 1.2.10: include Prodigal's error output in error messages (results unchanged)

## Description

> [!NOTE]
> **Results are unchanged.** This release only changes the messages CheckM gives when Prodigal fails. On the 128-genome validation set, every output file is identical to CheckM 1.2.9.

## Change
CheckM discarded Prodigal's error output, so a failure was reported only by its exit code:

```
Prodigal failed with '-p meta' (exit code 18) on: bins/x.fna
```

Prodigal writes the cause to stderr even when run with `-q`, for example:
- `Error: no input sequences to analyze.` (exit code 18)
- `Error: can't open input file ...` (exit code 5)

CheckM now captures this, condenses it to a single line of at most 1,000 characters, and includes it in the messages:

```
Prodigal failed with '-p meta' (exit code 18: Error: no input sequences to analyze.) on: bins/x.fna
```

The warning given before retrying with `-p meta` now distinguishes two cases:
- `-p single` failed. The warning includes Prodigal's message.
- `-p single` identified no genes. Previously this case reported a confusing `exit code 0`.

## Testing
- **New unit tests:** they use a fake `prodigal` that fails with a two-line error message, and check that it appears in both the retry warning and the final error, and that CheckM exits with status 1. The tests fail on 1.2.9 and pass with this change.
- **Unit test suite:** all tests pass.
- **128-genome validation:** `lineage_wf` on 128 GlobDB MAGs with `-t 64 --pplacer_threads 64`. All outputs are identical to 1.2.9: `qa` tables, `lineage.ms`, per-genome statistics, gene calls and HMMER hits.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f14f3f841c8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.