# Issue

**Title:** --help/--version should exit with status 0 (and write to stdout)

## Description

This changes both `--help` and `--version` to return an exit code of 0, indicating that nothing went wrong with the command, which is true.

It also sends the output of `--help` to stdout instead of stderr, which is the usual behavior for most command-line programs.

This has a few advantages:
1) You can run `cellsnp-lite --version` in a script with `set -o errexit`, without needing to turn off error-catching or swallow it with `|| true`.
2) Users can more easily send the help to a pager, like `cellsnp-lite -h | less`.
3) Less surprising to *nix users.

For reference, sections 4.8.1 and 4.8.2 of the GNU guidelines echo this advice: https://www.gnu.org/prep/standards/standards.html#g_t_002d_002dversion

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a795cc255b9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.