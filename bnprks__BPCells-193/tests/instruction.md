# Issue

**Title:** [r] Test data functions

## Description

Add functions for getting test data (`get_test_mat()`, `get_test_frags()`) and removal of test data (`remove_test_data()`).
Data was prepared using an internal function named `prepare_test_data()`.  This function is still exposed to maintain reproducibility in the future.  Outputs were stored as a tarball on our cloudflare object store.  

As we discussed, data is being stored in `file.path(tools::R_user_dir("BPcells", which="data"), "test_data")`, and can be easily removed using `remove_test_data()`.  It would be good to note that this feature is specific to R 4.0 and above.  

For versions below R 4.0.  We can probably add in a conditional that checks if a user provided directory exists, otherwise just write to tmp if not given.  Nonetheless, I think it would still be safe to keep BPCells to R 4.0 above.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d848ca44ca0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.