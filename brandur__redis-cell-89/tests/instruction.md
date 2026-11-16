# Issue

**Title:** Upgrade to various GitHub Actions

## Description

Turns out a whole bunch of Actions are either deprecated or already
fully archived. Try to upgrade some of the obvious ones.

Get rid of cache steps as the new GitHub Actions toolchain command in
use now has that built in.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a55a2a10a3f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.