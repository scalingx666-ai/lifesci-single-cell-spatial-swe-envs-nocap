# Issue

**Title:** Ban `pyplot.show` in the library

## Description

Bans `matplotlib.pyplot.show` in `src` via the `TID` rules the project already selects, so the class of bug just fixed in `li.pl.annulus` is caught when it is written rather than when a user with a display runs it — CI is headless, where `show` is a no-op. Also switches that function's `plt.tight_layout()` to act on the figure it built rather than on whichever one is current.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e466c5c8177`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.