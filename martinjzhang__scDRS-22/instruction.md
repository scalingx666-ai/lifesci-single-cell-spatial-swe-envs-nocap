# Issue

**Title:** cope with categorical covariates

## Description

To address #21 

Example: 
```python
df = pd.DataFrame({"number": [1,2,3], "sex": [np.nan, 'male', 'female'], 'age': ['6m', '12m', '18m']})
print(df)
df = category2dummy(df, verbose=True)
print(df)
```

Gives:
```
   number     sex  age
0       1     NaN   6m
1       2    male  12m
2       3  female  18m

scdrs.pp.category2dummy:  Detected categorical columns: sex,age, and added dummy variable columns: sex_male,age_18m,age_6m

   number  sex_male  age_18m  age_6m
0       1       NaN      0.0     1.0
1       2       1.0      0.0     0.0
2       3       0.0      1.0     0.0
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83fda44ac3c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.