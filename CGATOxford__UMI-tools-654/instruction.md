# Issue

**Title:** Make count_tab compatible with `umi_tools extract`

## Description

Provides a fix for #651.

I've updated the `get_cell_umi_read_string()` function in umi_tools/sam_methods.py so that the UMI and cell barcode are extracted in the same order that `umi_tools extract` creates them. I've also updated the docstring of umi_tools/count_tab.py to reflect this.

Since I had to update the test input file tests/count_tab_cell.tsv, I thought I would also fix the issue where `count_tab` writes out byte-encoded strings for the cell barcode. It was a small change but makes using downstream bash tools much easier.

Let me know what you think!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10c6495ab441`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.