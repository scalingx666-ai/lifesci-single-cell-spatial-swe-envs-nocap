# Issue

**Title:** More 3D plots

## Description

Replace  We would like to enable 3D quiver and scatter plot in dynamo. 

- [x] debug existing 3D scatter, quivers and streamtube.
- [x] enable plot quiver for 3 different genes or data from different layers 
- [x] remove 3d options in cell_wise_vector function and make it a separate function.
- [x] use other methods, including PyVista and Plotly to implement the 3D scatters / quiver plots 
- [x] Implementing 3D animation.

Two functionalities need further improvement. Will describe at details in a GitHub Issue. 

- The 3D vectors (Cone) plot implemented by Plotly doesn't support customized coloring. 
- Plotly animation doesn't move.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e8ffe4a103e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.