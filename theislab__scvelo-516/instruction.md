# Issue

**Title:** Fix matplotlib warnings

## Description

Fixes these 3 warnings (tested locally with `matplotlib==3.4.2` and `matplotib==3.3.0` on CellRank's CI).
Changed the min. matplotlib version to `3.3.0` because of the `normalize` in `pie(...)`, alt. would be to have if/else statement based on version (or directly inspect kwargs), but I think version bump is fine (`3.3.0` is ~1 year old):

1. [example code](https://cellrank.readthedocs.io/en/stable/auto_examples/plotting/plot_terminal_states.html)
```pytb
/home/docs/checkouts/readthedocs.org/user_builds/cellrank/envs/stable/lib/python3.8/
site-packages/scvelo/plotting/utils.py:115: MatplotlibDeprecationWarning:
Calling gca() with keyword arguments was deprecated in Matplotlib 3.4.
Starting two minor releases later, gca() will take no keyword arguments.
The gca() function should only be used to get the current axes,
or if no axes exist, create new axes with default keyword arguments.
To create a new axes with non-default arguments, use plt.axes() or plt.subplot().
```

2. [example code](https://cellrank.readthedocs.io/en/stable/auto_examples/plotting/plot_directed_paga.html#sphx-glr-auto-examples-plotting-plot-directed-paga-py)
```
/home/docs/checkouts/readthedocs.org/user_builds/cellrank/envs/stable/lib/python3.8/
site-packages/scvelo/plotting/paga.py:1045: MatplotlibDeprecationWarning:
normalize=None does not normalize if the sum is less than 1 but this 
behavior is deprecated since 3.3 until two minor releases later.
After the deprecation period the default value will be normalize=True.
To prevent normalization pass normalize=False
pie_axs[count].pie(fracs, colors=color_single, wedgeprops=wedgeprops)
```

3. [example code](https://cellrank.readthedocs.io/en/stable/auto_examples/plotting/plot_directed_paga.html#sphx-glr-auto-examples-plotting-plot-directed-paga-py)
```pytb
/home/docs/checkouts/readthedocs.org/user_builds/cellrank/envs/stable/lib/python3.8
/site-packages/scvelo/plotting/paga.py:1090: MatplotlibDeprecationWarning:
The inverse_transformed function was deprecated in Matplotlib 3.3 and will be removed two minor releases later.
Use transformed(transform.inverted()) instead.
bboxes.append(result.inverse_transformed(ax.transData))
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a1a3a7f8e3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.