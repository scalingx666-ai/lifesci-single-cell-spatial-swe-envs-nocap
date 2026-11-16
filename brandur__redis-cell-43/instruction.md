# Issue

**Title:** Fix various Rustfmt problems in the build

## Description

The unstable features I was using are still unstable (they appear to be
permanently so), and the situation's gotten worse in that Rustfmt seems
to not really be available in nightly builds anymore, which was the only
way that unstable features could be used.

For now, stop using those unstable features and stop running Rustfmt in
nightly, preferring only the stable channel instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1c689080ada1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.