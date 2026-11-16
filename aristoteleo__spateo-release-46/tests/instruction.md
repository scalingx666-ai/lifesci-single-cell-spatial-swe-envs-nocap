# Issue

**Title:** Update 3D reconstruction related functions

## Description

- Updated 3D reconstruction related functions：
1. Added the function to create 3D point clouds, surface meshes and volumetric meshes, you can freely create the mesh you want.
2. Added the function to merge multiple meshes.
3. Added another function to merge meshes. Use this function if you need to analyze them separately later.
4. Added the function to save mesh models as ply files.
5. Added the function to slice interactively.
6. Added the function to interactively pick the part of interest in the 3D model or delete the part that is not of interest.
7. Added the function to calculate the volume, surface area, volume / surface area ratio of a surface mesh or volume mesh
8. Added the function to compute point clouds KDE.
9. Added the function of outputting the actual memory size of the mesh.
10. Added two outlier detection functions (KDE-based and EllipticEnvelope algorithm-based) that can be used before reconstructing 3D structures.
11. Added the function of converting mesh format, you can switch between polydata and unstructuredgrid at will.

- Removed 3D drawing functions: the original drawing function is too inflexible, and new 3D drawing tools will be updated later.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4eeb3e9baaad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.