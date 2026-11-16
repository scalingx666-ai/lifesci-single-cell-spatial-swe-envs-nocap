# Issue

**Title:** Fixing bug of None true_label

## Description

In the current version if `true_label` is not passed in VIA's ctor one get the following exception:

> TypeError                                 Traceback (most recent call last)
~\AppData\Local\Temp/ipykernel_26896/2431515619.py in <module>
      1 v0 = via.VIA(X, knn=k, root_user=root, is_coarse=True, preserve_disconnected=True)
----> 2 v0.run_VIA()
~\anaconda3\envs\ViaEnv\lib\site-packages\pyVIA\core.py in run_VIA(self)
   3494         self.ncomp = self.data.shape[1]
   3495         pop_list = []
-> 3496         for item in set(list(self.true_label)):
   3497             pop_list.append([item, list(self.true_label).count(item)])
   3498         # print("population composition", pop_list)
TypeError: 'NoneType' object is not iterable

This happens because in the `run_VIA` function `self.true_label` is used in line 3615 but is only initialized in line 3618.
In the suggested fix I simply moved the initialization of `self.true_label` to the ctor

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `55cd5d9b4a5d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.