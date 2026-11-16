# Issue

**Title:** compute graph base on spatialdata regions and add mask graph based on polygon

## Description

**IMPORTANT: Please search among the [Pull requests](../pulls) before creating one.**

## Description
This PR introduces two features:
- compute spatial graph based on regions (shapes, labels) from spatialdata.
- mask the graph base on a shapes element (in spatialdata)

## masking
The idea is, given a graph and a polygon, mask it base on the polygon (either every edge contained inside the polygon, or everything that is outside or partially outside to the polygon). 
e.g. see
**Original**
![image](https://github.com/scverse/squidpy/assets/25887487/0b3647af-5e92-4647-8b42-39ba4773795b)


**Positive mask**

![image](https://github.com/scverse/squidpy/assets/25887487/7404652d-df5e-4af1-b845-f08753012e4f)

**Negative mask**
![image](https://github.com/scverse/squidpy/assets/25887487/37c67df8-a6ab-45a9-9511-4e2d3604db83)




## How has this been tested?

- [x] test for spatial graph building based on spatialdata
- [x] test for mask graph

It would be nice to have feedback on argument names/apis and I should also be adding an example to show how to use it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4a632d6f417c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.