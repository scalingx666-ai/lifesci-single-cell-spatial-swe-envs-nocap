# Issue

**Title:** Added Support for Reading Unfiltered Cell Ranger Feature Barcode Matrices (MEX Format)

## Description

# Description:
This PR introduces functionality to support the reading and processing of unfiltered Cell Ranger Feature Barcode Matrices (MEX format). Implemented the following:
- Default filtering cutoff at 500
- Implemented `read_header()` and `process_batch()`
- Implemented `_get_valid_barcodes()`
- Assertions for above method
- Implemented `rename_batches()` (to be used in `consume()`)
- Implemented `consume()` as per `_get_valid_barcodes()`

## 1. Header Parsing:
- The `read_header()` method reads the matrix header, extracting essential metadata (`nFeatures`, `nCells`, and `nCounts`) which is necessary for downstream processing.
## 2. Batch Processing
- The `process_batch()` method processes chunks of data in batches, aggregating counts per barcode and filtering out barcodes below a specified cutoff value (default: 500).
## 3. Get Valid Barcode:
- The method uses `pl.scan_csv` to scan the input matrix file (self.matFn), skipping the first three rows (header information) and assuming no header in the data.
- The matrix is divided into chunks based on the `lines_in_mem` parameter, ensuring that only a manageable portion of the data is loaded into memory at a time.
- The total number of chunks is calculated based on the total number of counts (`nCounts`) and the `lines_in_mem` parameter.
- If a chunk’s barcodes exceed the current batch boundary, it processes the accumulated data (`dfs`) and filters out background barcodes using the `process_batch` method.
- The valid barcodes are stored in `valid_idx`, and the method prepares for the next batch.
- Care is taken to handle barcodes that span across multiple chunks. This is managed by checking if the current chunk’s last barcode exceeds the current batch boundary and adjusting accordingly.
- If the chunk is within the batch boundary, it is accumulated in `dfs` for processing in the next iteration or at the end of the loop.
- After iterating through all chunks, any remaining data is processed to ensure all valid barcodes are identified and filtered.
- The method returns a sorted and unique list of valid barcodes after concatenating all valid indices collected across batches.
- An assertion is included to ensure that the total number of processed rows matches the expected count (`nCounts`), ensuring data integrity throughout the operation.
## 4. Rename Batches
Renames barcodes in a batch to a contiguous sequence of indices, starting from 0. This is useful for maintaining consistency when processing large datasets in chunks.
- Concatenates all `polar.DataFrames` in collect into a single `polar.DataFrame`.
- Extracts the `barcode` column and creates a unique list of barcodes and maps each unique barcode to a new index using a dictionary (`count_hash`).
- Replaces the original `barcode` values in the `DataFrame` with these new indices.
- Returns a `NumPy` array of the modified DataFrame with barcodes renamed to sequential indices.

## 5. Consume
Yields sparse matrices in chunks from an MTX file after filtering and processing the data in batches. This function is designed to handle large datasets efficiently.
- Reads the MTX file in batches using Polars, skipping header rows and applying a schema to the columns.
- Filters the data to include only barcodes present in `self.validBarcodeIdx`.
- Accumulates unique barcodes from the current chunk and checks if the accumulated unique barcodes exceed `batch_size`.
- If yes, processes the data, renames the barcodes, converts it to a sparse matrix, and yields it. If no, continues to accumulate chunks.
- Handles the remaining data after the main loop, ensuring all data is processed.
- Yields sparse matrices (`coo_matrix`), each corresponding to a processed batch of data.

# Testing:
- All unit test passed
- Uploaded additional notebook showcasing the correctness on existing and new dataset: [Link](https://github.com/Gautam8387/scarf-pr-exp/tree/main/01-valid-barcode)

# Documentation:
- Added docstrings to all new methods.
- Added comments when necessary
- Additional documentation on [Link](https://github.com/Gautam8387/scarf-pr-exp/tree/main/01-valid-barcode)

# Updates:
- Updated the head reader method to include `comment_prefix` instead of `skip_rows`. Updated other polar readers as well.
- Added test for empty barcodes. Added small dataset for empty barcode test

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ed28f782313`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.