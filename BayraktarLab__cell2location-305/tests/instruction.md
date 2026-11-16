# Issue

**Title:** Compatibility with scvi-tools 1.0.0+, lightning and pytorch 2.0 + signal gene and cell abundance quantification around candidate target cells

## Description

Code examples.

1. Computing average RNA abundance of signalling genes:

```python
distance_bins = [
    [5, 50],
    [50, 100],
    [100, 150],
    [150, 200],
    [200, 250],
    [300, 350],
    [350, 400],
    [400, 450],
    [450, 500],
    [500, 550],
    [550, 600],
    [600, 650],
    [650, 700],
]
weighted_avg_dict = dict()

normalisation_key = 'detection_y_s'
adata_vis.obsm[normalisation_key] = adata_vis.uns['mod']['post_sample_q05'][normalisation_key]

from tqdm.auto import tqdm
for distance_bin in tqdm(distance_bins):

    weighted_avg = compute_weighted_average_around_target(
        adata_vis,
        target_cell_type_quantile=0.995,
        source_cell_type_quantile=0.80,
        normalisation_quantile=0.999,
        normalisation_key=normalisation_key,
        genes_to_use_as_source=selected_symbols_,
        gene_symbols='SYMBOL',
        distance_bin=distance_bin,
    )
    weighted_avg_dict[str(distance_bin)] = weighted_avg

    from cell2location.plt.plot_heatmap import clustermap, dotplot
    clustermap(
        weighted_avg_dict[str(distance_bin)] + np.random.gamma(shape=10, scale=1e-5, size=weighted_avg.shape), 
        figure_size=[20, 20], vmin=0.0,
    )
    plt.show()
    
import pickle
pickle_file = open(f'{scvi_run_name}/weighted_avg_only_signal_distance_profiles.p', 'wb')
pickle.dump(weighted_avg_dict, pickle_file)
pickle_file.close()
weighted_avg_dict
```

2. Plotting distance functions

```python
# make an array and plot line plots with colour according to source       
source_var_1 = melt_signal_target_data_frame(weighted_avg_dict, distance_bins)
source_var_1.to_csv(f'{scvi_run_name}/weighted_avg_only_signal_distance_profiles.csv')

# manual annotation of non-mapped cell types
not_mapped = ['Cardiomyocytes_1_SEACell-93', 'Blood progenitors 2 SEACell-87', 'Caudal epiblast_SEACell-115', 'doublets SEACell-21', 'doublets SEACell-100', 'doublets SEACell-108', 'Erythroid1_SEACell-46', 'ExE ectoderm SEACell-26', 'ExE ectoderm SEACell-118', 'ExE endoderm SEACell-44', 'ExE endoderm SEACell-45', 'ExE endoderm SEACell-60', 'ExE endoderm SEACell-73', 'ExE endoderm SEACell-76', 'ExE endoderm SEACell-96', 'ExE endoderm SEACell-106', 'Gut 3 SEACell-28', 'Gut DefEndoderm 4 SEACell-13', 'Gut DefEndoderm 4 SEACell-70', 'Gut DefEndoderm 4 SEACell-74', 'Haematoendothelial progenitors SEACell-56', 'Intermediate mesoderm SEACell-58', 'Mesenchyme 1 SEACell-47', 'Mesenchyme 2 SEACell-63', 'Mesenchyme 4 SEACell-110', 'Nascent mesoderm SEACell-94', 'Nascent mesoderm SEACell-117', 'Neuroectoderm 1 SEACell-18', 'Paraxial mesoderm 1 SEACell-102', 'Parietal endoderm SEACell-59', 'Pharyngeal mesoderm SEACell-19', 'Rostral neurectoderm SEACell-29', 'Rostral neurectoderm SEACell-69', 'Somitic mesoderm SEACell-41', 'Spinal cord SEACell-78', 'Surface ectoderm 1 SEACell-109', 'Surface ectoderm 3 SEACell-12', 'Surface ectoderm 4 SEACell-68', 'Visceral endoderm SEACell-62']
from re import sub
not_mapped = [sub(' ', '_', i) for i in not_mapped]
not_mapped = [f'target {i}' for i in not_mapped]

sns.relplot(
    data=source_var_1.loc[~source_var_1.index.isin(not_mapped), :], 
    x='Distance bin', y='Abundance', 
    col='Target',
    hue='Signal', 
    col_wrap=10,
    kind="line",
    palette=sc.pl.palettes.default_102 + sc.pl.palettes.zeileis_28 + sc.pl.palettes.vega_20_scanpy,
    height=3.5, aspect=0.9,
);
plt.show()
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a583a836b3a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.