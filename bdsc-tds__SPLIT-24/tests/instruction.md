# Issue

**Title:** Validate required fields of RCTD output and halt if not post-processed

## Description

( and #21).
`SPLIT::convert_rctd_result_to_purify_input()` previously accessed `results_df$weight_first_type` and `results_df$weight_second_type` without checking their existence. When called on a non-post-processed RCTD object, these columns are absent, causing weights to be silently recycled via a sparse matrix construction warning rather than throwing an error. This led to most transcripts being incorrectly removed from otherwise normal cells (reported by @veldsla).

**Changes:**

Added sequential validation guards covering: `rctd@results` availability, post-processing status, required columns in `results_df` (`first_type`, `second_type`, `weight_first_type`, `weight_second_type`, `spot_class`), and `cell_type_info` completeness
If `run_post_process_RCTD()` has not been applied, it is now called automatically with an informative warning rather than proceeding silently with missing columns.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b78eb08a446f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.