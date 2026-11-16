# Issue

**Title:** Add plot explanation utilities and enhance visualizations

## Description

- Introduced `set_plot_explanations` and `get_plot_explanations` functions to control the display of plot explanations.
- Added detailed explanations for various plots including Jacobian, Fixed Points, Vector Field Topography, Speed, Curl, and Divergence.
- Updated arrow scale in scatter plots for improved visibility.
- Enhanced the `print_plot_explanation` function for better formatting and clarity of biological interpretations.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `41a6a091d14c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.