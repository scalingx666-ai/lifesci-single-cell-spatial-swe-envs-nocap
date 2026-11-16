# Issue

**Title:** Sc 50 disk backed operations

## Description

PR fixes issue when spatialdata object is disk-backed, see 

Fix was to do the following, e.g.

```
            if sdata.is_backed():
                sdata.write_element(output_layer)
                sdata_temp = read_zarr(sdata.path, selection=["images"])
                del sdata[output_layer]
                sdata[output_layer] = sdata_temp[output_layer]
                del sdata_temp
```

if spatialdata would support `write_element( reload=True )`, we should adapt our code, and use the `reload` parameter.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9afe814517ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.