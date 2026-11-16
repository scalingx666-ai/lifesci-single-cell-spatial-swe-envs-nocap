# Issue

**Title:** refactor: Import fewer private modules

## Description

partially with a workaround. I have moved everything we import privately to `_compat.py`. If there is a version mismatch it's handled there. This approach is like the `unsafe` block of Rust. At least it encapsulates the possible fragile code in one file.

Another function that we should reconsider is `_create_sparse_df`. It uses lots of protected members of pandas and might cause pandas version mismatch in the future. 

In fact only `ligrec` is using this function which caused reproducibility errors in the past. It wasn't directly caused by it but maybe if there was a safer code written the bug wouldn't surface. Or at least there would be a warning before the pandas behavior changed.
```python
# modified from pandas' source code
def _create_sparse_df(
    data: NDArrayA | spmatrix,
    index: pd.Index | None = None,
    columns: Sequence[Any] | None = None,
    fill_value: float = 0,
) -> pd.DataFrame:
    """
    Create a new DataFrame from a scipy sparse matrix or numpy array.

    This is the original :mod:`pandas` implementation with 2 differences:

        - allow creation also from :class:`numpy.ndarray`
        - expose ``fill_values``

    Parameters
    ----------
    data
        Must be convertible to CSC format.
    index
        Row labels to use.
    columns
        Column labels to use.

    Returns
    -------
    Each column of the DataFrame is stored as a :class:`arrays.SparseArray`.
    """
    from pandas._libs.sparse import IntIndex
    from pandas.core.arrays.sparse.accessor import (
        SparseArray,
        SparseDtype,
        SparseFrameAccessor,
    )

    if not issparse(data):
        pred = (lambda col: ~np.isnan(col)) if np.isnan(fill_value) else (lambda col: ~np.isclose(col, fill_value))
        dtype = SparseDtype(data.dtype, fill_value=fill_value)
        n_rows, n_cols = data.shape
        arrays = []

        for i in range(n_cols):
            mask = pred(data[:, i])
            idx = IntIndex(n_rows, np.where(mask)[0], check_integrity=False)
            arr = SparseArray._simple_new(data[mask, i], idx, dtype)
            arrays.append(arr)

        return pd.DataFrame._from_arrays(arrays, columns=columns, index=index, verify_integrity=False)

    if TYPE_CHECKING:
        assert isinstance(data, spmatrix)
    data = data.tocsc()
    sort_indices = True

    data = data.tocsc()
    index, columns = SparseFrameAccessor._prep_index(data, index, columns)
    n_rows, n_columns = data.shape
    # We need to make sure indices are sorted, as we create
    # IntIndex with no input validation (i.e. check_integrity=False ).
    # Indices may already be sorted in scipy in which case this adds
    # a small overhead.
    if sort_indices:
        data.sort_indices()

    indices = data.indices
    indptr = data.indptr
    array_data = data.data
    dtype = SparseDtype(array_data.dtype, fill_value=fill_value)
    arrays = []

    for i in range(n_columns):
        sl = slice(indptr[i], indptr[i + 1])
        idx = IntIndex(n_rows, indices[sl], check_integrity=False)
        arr = SparseArray._simple_new(array_data[sl], idx, dtype)
        arrays.append(arr)

    return pd.DataFrame._from_arrays(arrays, columns=columns, index=index, verify_integrity=False)


```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `277b1924e7e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.