# Issue

**Title:** Add guide_point_size as an arg in vis_clus

## Description

Adding `guide_point_size` allows users to easily change the size of points in the guide for `vis_clus()` plots. Typically to make the larger and more read-able, even when `point_size` gets quite small. 

Example without `guide_point_size`
![vis_clus_test_no_change](https://github.com/user-attachments/assets/3a5adaf2-6401-44f9-ab56-32583663dc4e)

Setting `guide_point_size = 5`
![vis_clus_test_guide_point_size](https://github.com/user-attachments/assets/9c8696b8-3156-4df3-9e90-ca7ce03445d6)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `35fe720741b0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.