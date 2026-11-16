# Issue

**Title:** Fix boxplot function KeyError

## Description

### Problem Description
The original `boxplot` function （`experiments/RegInf/utils.py`） was designed to create a box plot with marginal distributions. However, it contained a bug where the input `DataFrame`, `data`, was being overwritten after a `groupby` operation. This resulted in a loss of the original DataFrame structure, leading to a `KeyError` when attempting to group by the `hue` column later in the code. The function was trying to access a column that no longer existed in the modified DataFrame.

### Proposed Changes
To resolve this issue, I have made the following changes to the function:

1. **Separation of Data Manipulation and Plotting**: I introduced a new variable, `plot_data`, as a copy of the input `DataFrame`. This ensures that the original data is not altered during the plotting process. All manipulations are performed on `plot_data` instead.

2. **Categorical Conversion and Type Assertion**: The function now checks and converts the `x` and `hue` columns to categorical data types if they are not already. This ensures that the grouping operations work as expected.

3. **Stacked Bar Plot Calculation**: The calculation for the fractions in the stacked bar plot has been corrected. Instead of modifying the original DataFrame, a new `grouped_data` variable is created. It stores the normalized value counts necessary for the stacked bar plot, preserving the original data.

4. **Legend Handling**: The function has been updated to include a legend only when there is more than one level in the `hue` column, enhancing the clarity of the plot when hue distinctions are present.

These changes correct the error and improve the function's robustness by preventing unintended side effects on the input data.

### Additional Notes
The revised function has been thoroughly tested to ensure that it handles the input data correctly and that the resulting plots are generated as expected.

I believe these improvements will enhance the functionality and user experience for others utilizing this box plot function.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fea85ad175f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.