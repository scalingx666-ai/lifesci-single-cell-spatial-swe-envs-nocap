# Issue

**Title:** Fix/get df with default args

## Description

Previous error was due to attempting to index on the default argument of  `keys=None`.

## Changes
Changed
```python
keys = [keys] if isinstance(keys, str) else keys
key = keys[0]

...

if keys is None:
   df = data.to_df()
elif key in data.var_names:
   df = obs_df(data, keys, layer=layer)
elif key in data.obs_names:
   df = var_df(data, keys, layer=layer)
else:
   ...
```
to
```python
if keys is None:
   df = data.to_df()
else:
   keys = [keys] if isinstance(keys, str) else keys
   key = keys[0]
   if key in data.var_names:
      df = obs_df(data, keys, layer=layer)
   elif key in data.obs_names:
      df = var_df(data, keys, layer=layer)
   else:
      ...
```

and added accompanying test.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `31226cd2a3a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.