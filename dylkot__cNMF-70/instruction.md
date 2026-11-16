# Issue

**Title:** Set stability to 0 if n_clusters == n_spectra

## Description

silhouette sometimes throws an error in n_clusters == n_spectra.
```pytb
  File "/home/runner/work/immunaISR/immunaISR/immunaisr/methods/methods/consensus_nmf.py", line 126, in _consensus
    self.cnmf_op.consensus(
  File "/opt/hostedtoolcache/Python/3.8.17/x64/lib/python3.8/site-packages/cnmf/cnmf.py", line 791, in consensus
    stability = silhouette_score(l2_spectra.values, kmeans_cluster_labels, metric='euclidean')
  File "/opt/hostedtoolcache/Python/3.8.17/x64/lib/python3.8/site-packages/sklearn/metrics/cluster/_unsupervised.py", line 117, in silhouette_score
    return np.mean(silhouette_samples(X, labels, metric=metric, **kwds))
  File "/opt/hostedtoolcache/Python/3.8.17/x64/lib/python3.8/site-packages/sklearn/metrics/cluster/_unsupervised.py", line 231, in silhouette_samples
    check_number_of_labels(len(le.classes_), n_samples)
  File "/opt/hostedtoolcache/Python/3.8.17/x64/lib/python3.8/site-packages/sklearn/metrics/cluster/_unsupervised.py", line 33, in check_number_of_labels
    raise ValueError(
ValueError: Number of labels is 64. Valid values are 2 to n_samples - 1 (inclusive)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f04db6bc797d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.