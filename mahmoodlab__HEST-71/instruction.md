# Issue

**Title:** HESTData: provide util to map ensemble ID to gene name

## Description

**This PR**
* Provides util to map genes encoded using the ensemble ID (common for several `Spatial Transcriptomics` samples) to the gene name 
* Addresses #70 

**To dos**

- [ ] Might want to make this bi-directional to have `ensembleID_to_gene` and `gene_to_ensembleID` 
- [ ] There is some redundancy with `get_gene_db()` which is not needed when using the `use_cache` when we query the biomart annotations. Are we good to remove this function @pauldoucet as I don't see it used anywhere? 

**Run instructions**

```python
from hest import iter_hest, ensembleID_to_gene

# three samples with ensemblIDs as var_names
id_list = ['SPA118', 'SPA117', 'SPA116']

for st in iter_hest('/home/iain/kh/ssd/hest_data/', id_list=id_list):
    
    print(any([var_name.startswith("ENSG") for var_name in st.adata.var_names]))
    print(st.adata.var_names[:5])
    
    st_updated = ensembleID_to_gene(st)
    
    print(any([var_name.startswith("ENSG") for var_name in st_updated.adata.var_names]))
    print(st_updated.adata.var_names[:5])
```

Expected output: 

```
True
Index(['ENSG00000000003', 'ENSG00000000005', 'ENSG00000000419',
       'ENSG00000000457', 'ENSG00000000460'],
      dtype='object')
False
Index(['TSPAN6', 'TNMD', 'DPM1', 'SCYL3', 'FIRRM'], dtype='object', name='gene_name')
True
Index(['ENSG00000000003', 'ENSG00000000005', 'ENSG00000000419',
       'ENSG00000000457', 'ENSG00000000460'],
      dtype='object')
False
Index(['TSPAN6', 'TNMD', 'DPM1', 'SCYL3', 'FIRRM'], dtype='object', name='gene_name')
True
Index(['ENSG00000000003', 'ENSG00000000005', 'ENSG00000000419',
       'ENSG00000000457', 'ENSG00000000460'],
      dtype='object')
False
Index(['TSPAN6', 'TNMD', 'DPM1', 'SCYL3', 'FIRRM'], dtype='object', name='gene_name')
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c73e610fb68f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.