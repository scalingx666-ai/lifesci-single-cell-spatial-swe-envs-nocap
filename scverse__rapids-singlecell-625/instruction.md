# Issue

**Title:** Implement Harmony2 paper improvements for preventing overintegration

## Description

Implements three algorithmic improvements from the Harmony2 paper (Patikas et al., 2026; doi:10.64898/2026.03.16.711825) to prevent overintegration in biologically heterogeneous     
  datasets:                                                                                                                                                                           
                                                                                                                                                                                        
  - Stabilized diversity penalty: Changes the penalty formula from (E+1)/(O+1) to (E+1)/(O+E+1), which prevents the diversity term from diverging when a batch is absent from a cluster.
   The old formula could dominate the objective and force overintegrated clusters. Controlled via stabilized_penalty (default True), templated as a compile-time bool in CUDA kernels.
  - Dynamic per-cluster-per-batch ridge regularization: Replaces the fixed scalar ridge_lambda=1.0 with lambda_kb = alpha * E_kb, scaling regularization proportionally to the expected 
  batch representation in each cluster. Well-represented batches get strong correction; rare/absent batches get weak correction. Controlled via dynamic_lambda (default True) and alpha 
  (default 0.2).
  - Batch pruning: Batches with O_kb / N_b < threshold are pruned from the correction for that cluster (their correction factors are set to zero). Implemented as a special case of     
  dynamic lambda — pruned entries get lambda_kb = 1e30, which drives the correction to zero without any kernel changes. Controlled via batch_prune_threshold (default 1e-5).            
  
  All three features default to Harmony2 behavior. To recover the original Harmony1 behavior, pass stabilized_penalty=False, dynamic_lambda=False.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e67e3c36e386`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.