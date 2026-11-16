# Issue

**Title:** Fix paga_pie node_size

## Description

Hi @VolkerBergen ,

I've managed to fix the node sizes/arrow when plotting the pie charts in `scv.pl.paga`, as mentioned in  The idea is simple: just get the bounding boxes around the markers and use correct transformations to get the pie sizes.
Here's a code to reproduce the plots below:
```python
import scvelo as scv
import numpy as np

np.random.seed(42)
adata = scv.datasets.toy_data(100)
scv.pp.neighbors(adata)
scv.tl.velocity_graph(adata)
scv.tl.paga(adata)
x = {i: {"#ff0000": 0.5} for i in range(12)}

scv.pl.paga(adata, node_size_scale=3, dpi=100, node_colors=x)
```
Before:
![old](https://user-images.githubusercontent.com/46717574/83576831-f1afce80-a532-11ea-9087-980182cbb899.png)
After
![new](https://user-images.githubusercontent.com/46717574/83576844-f70d1900-a532-11ea-874c-c6898b99635c.png)

To validate that the sizes are correct, I set `linewidths=1, c='g'` in https://github.com/theislab/scvelo/blob/master/scvelo/plotting/paga.py#L638 and it almost perfectly matches (there's some small border between the arrows and the nodes' border that I don't know where it's coming from).
![validation](https://user-images.githubusercontent.com/46717574/83577061-861a3100-a533-11ea-9848-4cbf3aab757b.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0eafcc15d19a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.