# Issue

**Title:** add von neumann entropy

## Description

This PR looks huge but really I've just refactored most of the code to allow for the addition of the von_neumann_entropy function, analogue to the `VNE.m` code in matlab. 

VNE requires diff_deg and gs_ker, so I've stored these on the PHATE object. An alternative would be to recompute these (if memory requirements outweigh CPU.) I've also included `fit` and `transform` as separate functions so that a user can run the functions in this order:
```
ph = PHATE(a=10, k=5, t=5)
ph.fit(x)
h = ph.von_neumann_entropy(t_max=50)
plt.plot(h)
# select better choice of t
ph.reset_diffusion(t=30)
y = ph.fit_transform(x) # or ph.fit(x); y=ph.transform()
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d4e7914fd1ee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.