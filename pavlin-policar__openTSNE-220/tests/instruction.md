# Issue

**Title:** Implement auto early exaggeration

## Description

Implements #218.

First, `early_exaggeration="auto"` is now set to `max(12, exaggeration)`.

Second, the learning rate. We have various functions that currently take `learning_rate="auto"` and set it to `max(200, N/12)`. I did not change this, because those functions usually do not know what the early exaggeration was. So I kept it as is. I only changed the behaviour of the base class: there `learning_rate="auto"` is now set to `max(200, N/early_exaggeration)`.

This works as intended:

```Python
X = np.random.randn(10000,10)

TSNE(verbose=True).fit(X)
# Prints 
# TSNE(early_exaggeration=12, verbose=True)
# Uses lr=833.33

TSNE(verbose=True, exaggeration=5).fit(X)
# Prints
# TSNE(early_exaggeration=12, exaggeration=5, verbose=True)
# Uses lr=833.33

TSNE(verbose=True, exaggeration=20).fit(X)
# Prints
# TSNE(early_exaggeration=20, exaggeration=20, verbose=True)
# Uses lr=500.00
```

(Note that the learning rate is currently not printed by the `repr(self)` because it's kept as "auto" at construction time and only set later. That's also how we had it before.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f79f37ce6752`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.