# Issue

**Title:** Fix interpret colors

## Description

Hi @VolkerBergen ,

apparently, if there's `'x'` and `'y'` in `adata.obs`, `interpret_color` does not work. Culprit: https://github.com/theislab/scvelo/blob/master/scvelo/plotting/scatter.py#L550 + https://github.com/theislab/scvelo/blob/master/scvelo/plotting/utils.py#L680
This PR fixes this.

```python3
import scvelo as scv

adata.obs['foo'] = 'bar'
adata.obs.loc[adata.obs_names[:1000], 'foo'] = 'baz'
adata.obs.loc[adata.obs_names[1000:2000], 'foo'] = np.nan

adata.obs['foo'] = adata.obs['foo'].astype('category')
adata.obs['x'] = 0
adata.obs['y'] = 0
#AnnData object with n_obs × n_vars = 3696 × 27998
#    obs: 'clusters_coarse', 'clusters', 'S_score', 'G2M_score', 'foo', 'x', 'y'
#    var: 'highly_variable_genes'
#    uns: 'clusters_coarse_colors', 'clusters_colors', 'day_colors', 'neighbors', 'pca', 'foo_colors'
#    obsm: 'X_pca', 'X_umap'
#    layers: 'spliced', 'unspliced'
#    obsp: 'distances', 'connectivities'


scv.pl.scatter(adata, color='foo', basis='pca')
```

```pytb
---------------------------------------------------------------------------
KeyError                                  Traceback (most recent call last)
~/miniconda3/envs/cellrank/lib/python3.7/site-packages/pandas/core/indexes/base.py in get_loc(self, key, method, tolerance)
   2890             try:
-> 2891                 return self._engine.get_loc(casted_key)
   2892             except KeyError as err:

pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()

pandas/_libs/index.pyx in pandas._libs.index.IndexEngine.get_loc()

pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()

pandas/_libs/hashtable_class_helper.pxi in pandas._libs.hashtable.PyObjectHashTable.get_item()

KeyError: 'clusters_coarse'

The above exception was the direct cause of the following exception:

KeyError                                  Traceback (most recent call last)
<ipython-input-195-55630d65d6f5> in <module>
----> 1 scv.pl.scatter(adata, color='foo', basis='pca')

~/scvelo/scvelo/plotting/scatter.py in scatter(adata, basis, x, y, vkey, color, use_raw, layer, color_map, colorbar, palette, size, alpha, linewidth, linecolor, perc, groups, sort_order, components, projection, legend_loc, legend_loc_lines, legend_fontsize, legend_fontweight, legend_fontoutline, xlabel, ylabel, title, fontsize, figsize, xlim, ylim, add_density, add_assignments, add_linfit, add_polyfit, add_rug, add_text, add_text_pos, add_outline, outline_width, outline_color, n_convolve, smooth, rescale_color, color_gradients, dpi, frameon, zorder, ncols, nrows, wspace, hspace, show, save, ax, **kwargs)
    550                     color="lightgrey",
    551                     ax=ax,
--> 552                     **scatter_kwargs,
    553                 )
    554                 if groups is not None and len(groups) == 1:

~/scvelo/scvelo/plotting/scatter.py in scatter(adata, basis, x, y, vkey, color, use_raw, layer, color_map, colorbar, palette, size, alpha, linewidth, linecolor, perc, groups, sort_order, components, projection, legend_loc, legend_loc_lines, legend_fontsize, legend_fontweight, legend_fontoutline, xlabel, ylabel, title, fontsize, figsize, xlim, ylim, add_density, add_assignments, add_linfit, add_polyfit, add_rug, add_text, add_text_pos, add_outline, outline_width, outline_color, n_convolve, smooth, rescale_color, color_gradients, dpi, frameon, zorder, ncols, nrows, wspace, hspace, show, save, ax, **kwargs)
    482             else:
    483                 # embedding, gene trend etc.
--> 484                 c = interpret_colorkey(adata, color, layer, perc, use_raw)
    485 
    486             if c is not None and not isinstance(c, str) and not isinstance(c[0], str):

~/scvelo/scvelo/plotting/utils.py in interpret_colorkey(adata, c, layer, perc, use_raw)
    683         elif np.any([obs_key in c for obs_key in adata.obs.keys()]):
    684             obs_keys = [
--> 685                 k for k in adata.obs.keys() if not isinstance(adata.var[k][0], str)
    686             ]
    687             obs = adata.obs[[obs_keys]]

~/scvelo/scvelo/plotting/utils.py in <listcomp>(.0)
    683         elif np.any([obs_key in c for obs_key in adata.obs.keys()]):
    684             obs_keys = [
--> 685                 k for k in adata.obs.keys() if not isinstance(adata.var[k][0], str)
    686             ]
    687             obs = adata.obs[[obs_keys]]

~/miniconda3/envs/cellrank/lib/python3.7/site-packages/pandas/core/frame.py in __getitem__(self, key)
   2900             if self.columns.nlevels > 1:
   2901                 return self._getitem_multilevel(key)
-> 2902             indexer = self.columns.get_loc(key)
   2903             if is_integer(indexer):
   2904                 indexer = [indexer]

~/miniconda3/envs/cellrank/lib/python3.7/site-packages/pandas/core/indexes/base.py in get_loc(self, key, method, tolerance)
   2891                 return self._engine.get_loc(casted_key)
   2892             except KeyError as err:
-> 2893                 raise KeyError(key) from err
   2894 
   2895         if tolerance is not None:

KeyError: 'clusters_coarse'
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ff51ba53f7f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.