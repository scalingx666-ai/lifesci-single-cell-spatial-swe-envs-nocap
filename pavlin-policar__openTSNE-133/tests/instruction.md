# Issue

**Title:** max update norm parameter

## Description

.

I tested it on MNIST with default parameters and the default `max_step_norm=5` (same as in FIt-SNE) does not affect the embedding (I think it's never triggered). If one sets it to a much smaller number, it produces a funny effect:

![tmp-opentsne-step001](https://user-images.githubusercontent.com/8970231/81945522-82635080-95fe-11ea-9f89-4b241b163c9a.png)

Here with `max_step_norm=0.01` no point can be further than 7.5 from zero (with 750 iterations).

@jnboehm tested it on one case where we had some points shooting off (with strong exaggeration factor), and the default `max_step_norm=5` resolved the problem.

For `transform()` I set the default to `None` because there you have nonzero `max_grad_norm` by default so I thought it might be enough. You are also limiting the interpolation grid there, I think.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b47a3c594e49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.