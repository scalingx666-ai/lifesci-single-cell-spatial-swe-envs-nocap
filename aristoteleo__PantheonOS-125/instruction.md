# Issue

**Title:** feat(cli): headless one-shot (-i) + resume (-r) + autonomous no-ask mode

## Description

## What

Makes `pantheon cli` fully scriptable (benchmarks, automation, cron) and ensures it never blocks on a non-existent user.

### Flags
- **`-i "<prompt>"` ⇒ headless one-shot**: run the prompt to completion, print, exit; skips the setup wizard. No separate `--once` flag. `--once` is still accepted as a **deprecated no-op** so the benchmark harness / older images keep working. Omit `-i` for the interactive REPL.
- **`-r` / `--resume [id]`**: resume a previous chat — most recent if no id, or `-r=<id>` / by number / name-prefix. Combine with `-i` to continue that chat's **context** in one shot.

### Headless = autonomous (no asking)
With no user present, the agent must not ask, request approval, or offer choices. The once path sets `PANTHEON_HEADLESS`, which:
- makes `notify_user` never hand control back — `interrupt` is forced off and the result tells the agent to choose a default and proceed;
- suppresses the `CONFIRM_OPEN_CHOICES` ephemeral nudge and the first-execution decision-point gate (both layered on top of, **not** reverting, the current EM);
- injects a `HEADLESS_AUTONOMOUS_REMINDER` so the agent proactively decides for itself.

## Files
`pantheon/__main__.py` (flag normalization), `pantheon/repl/__main__.py` (`-i`⇒once, `-r`), `pantheon/repl/core.py` (once mode + `PANTHEON_HEADLESS`), `pantheon/toolsets/task/ephemeral.py` + `task_toolset.py` (headless no-ask).

## Testing
Validated end-to-end via the docker agent image with this source mounted:
- `pantheon cli -i "..."` runs one-shot and exits (no `--once`).
- `pantheon cli -r -i "..."` resumed the most-recent session and **recalled context** from the prior run.
- An deliberately under-specified task ("start a single-cell analysis", no dataset named) **completed autonomously** — the agent chose a sensible dataset and finished instead of stopping to ask.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0fcf4f3b8f59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.