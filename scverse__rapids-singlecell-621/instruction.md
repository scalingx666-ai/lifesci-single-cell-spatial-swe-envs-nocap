# Issue

**Title:** Fix ForceAtlas2 random cell ordering by sort positions by vertex in draw_graph function

## Description

Hi, I noticed that `tl.draw_graph` was completely scrambling the order of the cells in the FA2 embedding, it seems that this is resolved by adding this line of code!

Tested on 
cugraph: 26.02.00
rapdis_singlecell: 0.15.0rc4

Cheers

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `51817a06ab24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.