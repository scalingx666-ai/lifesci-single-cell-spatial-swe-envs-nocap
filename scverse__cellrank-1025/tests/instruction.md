# Issue

**Title:** allow data and velocity to be read from obsm (as needed for MongeVelo…

## Description

…cities)

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
Changes in `_velocity_kernel.py` so that data can optionally be read from `obsm`. This is needed for MongeVelocities where the dimension of the velocities may differ from the dimension of `adata.X` so that they cannot be stored in `adata.layers` but only in `adata.obsm`. Defaults are set so that the new implementation matches the original implementation.

## How has this been tested?
So far I have only tested that 
```python
import numpy as np
import jax.numpy as jnp
import scanpy as sc
import scvelo as scv
import cellrank as cr
from cellrank.kernels import VelocityKernel
from moscot.datasets import simulate_data

adata = cr.datasets.pancreas_preprocessed()
scv.utils.show_proportions(adata)
vk = VelocityKernel(adata)
vk.compute_transition_matrix()
```
as well as 
```python
import numpy as np
import jax.numpy as jnp
import scanpy as sc
import scvelo as scv
import cellrank as cr
from cellrank.kernels import VelocityKernel
from moscot.datasets import simulate_data

adata = simulate_data(
    n_distributions=2,
    cells_per_distribution=40,
    n_genes=60,
    key="batch",
)

sc.pp.pca(adata, n_comps=30)
sc.pp.neighbors(adata)

from moscot.problems.time import TemporalNeuralProblem
tnp = TemporalNeuralProblem(adata)
tnp = tnp.prepare(time_key="batch", joint_attr = "X_pca")
tnp = tnp.solve(tau_a=1, tau_b=1, iterations=3)
source = jnp.array(adata.obsm["X_pca"].copy())
velocity = tnp[('0', '1')].solution.push(source) - source


tnp.adata.obsm["Monge_velocities"] = velocity

vk = VelocityKernel(adata, xkey="X_pca", vkey="Monge_velocities", attr="obsm")
vk.compute_transition_matrix()
```
run without error. Whether the output is correct has so far not been tested.


This PR replaces a older, separate PR which implemented a separate `MongeKernel`:  We realized that the `MongeKernel` is essentially identical to the `VelocityKernel` if we allow data to be read from `adata.obsm`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e54987b800a2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.