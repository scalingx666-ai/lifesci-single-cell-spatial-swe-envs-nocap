# Issue

**Title:** fix(quant): a record with no placement gets MAPQ 0, not 255

## Description

Note 1 from your #1151 review, which merged before I could apply it, so it comes as a follow-up rather than a response commit.

The `nh == 0` arm returned 255. No mapped record reaches it, since a fragment with no placements never enters the record loop, so the arm is only about record kinds that have no placement by construction: an unmapped read, once #1142 or its successor writes them. 255 there claims certainty about a placement that does not exist, and 0 is what samtools convention expects on an unmapped record.

Your reasoning for doing it now rather than then is the part I would underline: whoever adds unmapped output is unlikely to go looking for this function's edge case, and the failure would be a plausible-looking 255 rather than anything that breaks.

One line, its test line, and a row in the docs table so the `MAPQ` section covers the no-placement case rather than only `NH >= 1`.

Note 2 (the `#1150` contract paragraph reconciliation) is yours and I have left it alone.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `adbbaee6abe3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.