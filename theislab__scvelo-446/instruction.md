# Issue

**Title:** Generalized dynamics recovery

## Description

## New

* Adds submodule `dynamics`.
* Parameters of different models can be inferred by defining recovery classes. The classes inherit from `DynamiscRecoveryBase`. `SplicingDynamicsRecovery` has been implemented to recover the model parameters of the original 2D splicing model. The generalised dynamics recovery has been compared to the original implementation on simulated data. For this, the if clause [here](https://github.com/theislab/scvelo/blob/e77e01f09bba3e4c6e808ceda149563f47f3d134/scvelo/tools/dynamical_model.py#L270) was commented out and the default tolerance used [here](https://github.com/theislab/scvelo/blob/e77e01f09bba3e4c6e808ceda149563f47f3d134/scvelo/tools/dynamical_model.py#L184), [here](https://github.com/theislab/scvelo/blob/e77e01f09bba3e4c6e808ceda149563f47f3d134/scvelo/tools/dynamical_model.py#L199) and [here](https://github.com/theislab/scvelo/blob/e77e01f09bba3e4c6e808ceda149563f47f3d134/scvelo/tools/dynamical_model.py#L208). The new implementation only stores the information of the data of the gene for which a model is fitted. This reduces memory usage.

## Usage

Recovery classes require the count data `counts` as well as the pre-train `pretrain` and training steps `train` to be specified:
* `counts` has the shape `n_obs x n_variables`, where `n_variables` is the number of variables in the dynamical system. The column order must be the same as returned by the model class, e.g. `SplicingDynamics` [here](https://github.com/theislab/scvelo/blob/e77e01f09bba3e4c6e808ceda149563f47f3d134/scvelo/core/_models.py#L13).
* During pretraining explicit time assignments are used. This generalises the hard coded choices [here](https://github.com/theislab/scvelo/blob/e77e01f09bba3e4c6e808ceda149563f47f3d134/scvelo/tools/dynamical_model.py#L114) in the original implementation.
* During training the actual EM algorithm is performed. This generalises the original implementation [here](https://github.com/theislab/scvelo/blob/e77e01f09bba3e4c6e808ceda149563f47f3d134/scvelo/tools/dynamical_model.py#L120).

The recovery of dynamics 

```python
from scvelo.tools import recover_dynamics

_adata = recover_dynamics(
    adata, var_names="all", return_model=False, copy=True
)
```

is now achieved via

```python
from scvelo.tools._dynamics import recover_dynamics

_adata = recover_dynamics(
    adata,
    modalities=["unspliced", "spliced"],
    dynamics="splicing",
    model_parameters=["alpha", "beta", "gamma"],
    initial_parameter_fit=[
        {"parameter_names": ["scaling", "beta"], "sight": 0.5, "num": 4},
        {"parameter_names": ["scaling", "beta"], "sight": 0.1, "num": 4},
        {"parameter_names": ["alpha"], "sight": 0.1, "num": 5}
    ],
    pretrain=[
        ["t_", "alpha"],
        ["t_", "beta", "scaling"],
        ["alpha", "gamma"],
        ["t_"],
        ["t_", "alpha", "beta", "gamma"]
    ],
    train=[["t_", "alpha", "beta", "gamma"]],
    assignment_mode="projection",
    var_names="all",
    inplace=False,
)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e77e01f09bba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.