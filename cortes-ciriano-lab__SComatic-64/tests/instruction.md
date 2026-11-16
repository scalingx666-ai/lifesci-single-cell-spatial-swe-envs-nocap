# Issue

**Title:** Add max_depth option for pysam.pileup in BaseCellCounter.py and SingleCellGenotype.py

## Description

- Added a max_dp option in `BaseCellCounter.py` and `SingleCellGenotype.py` as discussed in #63
- For the int(DP) and int(NC) filters in `BaseCellCalling.step1.py`, swapped min_reads and min_cells (from #16)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2be7fdfc3bd8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.