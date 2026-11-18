# Issue

**Title:** Update _tileplot.py for plotnine >=0.13

## Description

With `plotnine>=0.13` they changed the interface of `facet_grid` (see [Release notes](https://github.com/has2k1/plotnine/releases/tag/v0.13.0)); there's not more argument `facets`  and doing something like [the tutorial](https://liana-py.readthedocs.io/en/latest/notebooks/targeted.html)
```python
li.pl.tileplot(liana_res=lr_res,
               fill = 'expr',
               label='padj',
               label_fun = lambda x: '*' if x < 0.05 else np.nan,
               top_n=15,
               orderby = 'interaction_stat',
               orderby_ascending = False,
               orderby_absolute = False,
               source_title='Ligand',
               target_title='Receptor',
               )
```
will fail with plotnine>=0.13. 

As a simple fix, just remove the named argument in facet_grid solves the issue and is backwards compatible.
Thanks for creating this awesome package!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eeb9cdbf29e9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.