# Issue

**Title:** Color shapes column

## Description

At the moment manually tested using the following code for both points and shapes columns:

```
from napari_spatialdata import Interactive
import pandas as pd
import spatialdata
import numpy as np
from spatialdata.models import PointsModel, ShapesModel

data=spatialdata.read_zarr('./merfish.zarr')
a = data["anatomical"]
a["extra_numerical"] = np.random.randint(0,200, size=len(data["anatomical"]))
a["extra_categorical"] = np.random.choice(["a", "b", "c"], size=len(data["anatomical"]))


b=data["single_molecule"]
index=b.index
extra= pd.DataFrame({"extra": np.random.randint(0,200, size=len(data["single_molecule"]))})
extra.reset_index(inplace=True)
d = np.array(b[['y', 'x']])

# As I understand numerical is not possible for Pointsmodel, is this correct?
news = PointsModel.parse(d, annotation=extra, feature_key="extra")
new = ShapesModel.parse(a)
data['new_anatomy'] = new
data["new_molecule"] = news
Interactive(data)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `adbd7a4bec76`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.