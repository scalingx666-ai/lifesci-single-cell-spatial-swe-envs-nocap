# Issue

**Title:** fix(agent): stop idle think-only spinning after a task completes

## Description

## Problem
After completing a task the agent burned tokens — observed **249 consecutive `think()` calls** before the run finally ended. Two compounding issues:
1. **`blocked_on_user` semantics were unclear/conflated.** The param controls BOTH whether the run yields AND how the message renders: `true` = an approval/review gate ("Awaiting Review") that waits for the user; `false` = a plain notification ("Completed"/progress) that does **not** block. At completion the agent didn't have a clean "deliver + hand back" signal.
2. **No loop-side backstop** for a think-only idle loop (the existing excessive-tools guard excludes `think` from its count).

## Fix
1. **Docstring** (`task_toolset.py`): reframe `blocked_on_user` around **ASK vs TELL** — `true` only when you genuinely need the user to approve/decide *before* continuing; `false` for progress FYIs **and final completion** (you're delivering, not asking permission, so it reads as "Completed", with deliverables in `paths_to_review`). The run hands control back on its own once idle, so the agent does NOT need `true` to "stop".
2. **Hard idle guard** (`agent.py` run loop): after `IDLE_THINK_ONLY_LIMIT` (3) consecutive turns whose **only** action is `think()` (no other tool, no user-facing message), end the run and return control to the user. `think()` is metacognition, not external progress — repeated think-only turns mean spinning. Caps the waste at ~3 turns regardless of model behaviour.

The guard is the robust backstop (the failure mode is literally "the model ignores ephemeral reminders", so a structural guard, not another reminder, is the safety net); the docstring keeps the **clean "Completed" UX** (a finished task should not look like it needs approval).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6df814bb8843`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.