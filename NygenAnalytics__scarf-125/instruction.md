# Issue

**Title:** Added Support For Merging Multiple DataStore and Handling Different Assay Types

## Description

# Description:
This PR introduces functionality to merge multiple datastores, handling different assay types and generating missing assays on the fly. Implemented the following:
- `merge.py` file contains all merge functionality
    - `DatasetMerge` class for merging datasets.
    - Renamed `ZarrMerge` to `AssayMerge` for better understanding.
- `permute_in_chunks()` inside `utils.py` to generate random index for cells (in chuks)
-  `to_polars_dataframe()` method for `MetaData` class for polars support.
- `get_assay()` method for `DataStore` class to easily access the assay.
- `test_merger.py` unit tests added

## 1. `merge.py`
### 1.1 `AssayMerge()` Class
- The `ZarrMerge` class has been renamed to `AssayMerge` to better represent the functionality of merging assay objects into a Zarr file. Alias is added for backward compatibility
- Added a new method, `perfrom_randomization_rows`, to randomize assay rows using chunk sizes and permutation logic. This method generates chunk-level permutations, which are later applied to ensure cells and features are merged in a randomized, yet controlled, order across assays.
- Introduced methods `_merge_cell_table` and `_merge_order_feats` to efficiently merge cell metadata and feature data using the `polars` library.
- Added multiple assertions and error-handling mechanisms to check for data consistency, including checking the order of cells and features in merged datasets.
### 1.2 `DatasetMerge()` 
- Introduced `DatasetMerge`, which handles merging multiple datastores (each containing different assays). This class creates merge objects for each unique assay in the provided datastores.
- For assays not present in certain datasets, a dummy assay is generated using `generate_dummy_assay()` method.
- Doc Strings added.
## 2. `permute_in_chunks()`
- The function divides the array into chunks, shuffles each chunk independently, and returns a list of permuted arrays (chunks). If the array size is not evenly divisible by the chunk size, the remaining elements are also shuffled and added as the last chunk.
<img src="https://github.com/user-attachments/assets/436af498-8804-4401-b032-980668b8a5bd" width="400">

## 3. `to_polars_dataframe()`
- Polar implementation of `to_pandas_dataframe()` method of `DataStore`. The function checks if the requested columns exist in the object's data, retrieves and stores them in a Polars DataFrame, and optionally sorts the DataFrame based on the provided key.

## 4. `get_assay ()`
If the specified assay is not found in the object's list of assay names, it raises a `ValueError`. Otherwise, it returns the corresponding assay object from the object's attributes.

## 5. `test_merger.py`
These unit tests evaluate the merging functionality of assays and datasets using the Zarr storage format. They verify the correctness of merged data by checking the shape and sum of the data after merging, ensuring that the output is as expected.
### 5.1 `test_assay_merge()`
- This test verifies the merging of `RNA` assays within the same datastore.
- It uses the `AssayMerge` class to merge two identical `RNA` assays.
- After merging, the test checks that the shape of the data reflects double the number of original cells and confirms that the sum of values in the merged data is twice the sum of the original `RNA` data.
### 5.2 `test_dataset_merge_2()`
- This test validates the merging of two identical datasets using the `DatasetMerge` class.
- It checks two assays (`RNA` and `assay2`) after merging, ensuring the shape of the merged data correctly reflects double the number of cells in the original dataset for each assay.
- It also verifies that the sum of the merged data matches twice the sum of the original data for both assays.
### 5.3 `test_dataset_merge_3()`
- This test extends the dataset merging validation to three identical datasets using `DatasetMerge`.
- It performs similar checks as the previous test, ensuring that the shape of the merged data is three times the original number of cells for both `RNA` and `assay2`.
- The test also verifies that the sum of the merged data is three times the sum of the original data for each assay.

# Testing:
- All unit test passed
- Uploaded additional notebook showcasing the correctness on existing and new dataset: [Link](https://github.com/Gautam8387/scarf-pr-exp/tree/main/02-zarr-merge)

# Documentation:
- Added docstrings to all new methods.
- Added comments when necessary.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6ed28f782313`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.