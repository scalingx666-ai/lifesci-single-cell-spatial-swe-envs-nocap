# Issue

**Title:** Refactor: Handling Unrecognized Arguments for Prepare

## Description

These are the things I want to do first.  related: #596

From reading through ottjax only the `__call__` functions on solvers absorb kwargs that aren't recognized. And they are because either they are given to create_geometry methods or create_initializer methods:

- https://github.com/ott-jax/ott/blob/458e265a1282d417f87bc0e07a5b6b77ffe9ae50/src/ott/initializers/quadratic/initializers.py#L134-L155
- https://github.com/ott-jax/ott/blob/458e265a1282d417f87bc0e07a5b6b77ffe9ae50/src/ott/initializers/linear/initializers_lr.py#L232-L243

So this is kind of good news because from what I read from moscot, call_fn arguments are filtered before here:
https://github.com/theislab/moscot/blob/e21677e6fbf1e5484b1c69a8ba55587dbf40f009/src/moscot/base/solver.py#L145-L164

Overall this means:
- We can fix the`prepare` methods absorbing kwargs ourselves in moscot, by simply removing the usage of kwargs in concrete classes, so I will dedicate this PR to it
- But for `solve` we will need to refactor things from ottjax. It won't be too hard and I already spotted where they are being ignored. If we refactor ottjax we might not need any changes in moscot since the error will be thrown from there.

Related issues (will be closed after merge):
- 
- 
- 
- 


I separated some issues from this PR so that we can work on them later:
-  : I did this one because when inheriting docstring GW removed the arguments for linear, and this lead to duplicate docstrings
-  : Because although in terms of software, current PR makes sense, there might be some cases where a parent classes argument is ignored/fixed but is not yet discovered. I am not confident about this as I am not completely familiar with the Biology use cases of all classes.
- 


Now that the tests pass these are the things to do:
- [x] clean up code (most likely requires refactoring of `handle_joint_attr`)
- [x] update docstrings
- [x] clean the TODO's and ensure that everyone agrees on the new docs and docstrings
- [x] write tests to ensure it fails (not sure if tests are necessary at this point since the checks are static now, will probably figure out cases to test when working on )

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b8641116a35e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.