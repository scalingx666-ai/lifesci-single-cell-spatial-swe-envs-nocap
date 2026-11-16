# Issue

**Title:** Aggregate feature values in scatterplot if multiple genes are selected

## Description

## Summary
### Problem
This PR solves fixes the problem that when selecting multiple genes from the featureList, the coloring of the points in the scatterplot was based only on the value of the first gene.
This is caused by `useExpressionValueGetter` taking `expressionData[0]` while it contains multiple arrays, one for each selected gene.

### Solution
I created a new file `packages/utils/other-utils/src/expr.ts` with function `aggregateFeatureArrays` that aggregates multiple arrays of numbers into a single array using a specified strategy.
I created a separated function because it's likely that we will have to reuse the function also for `SpatialSubscriber` and `ExpressionHistogramSubscriber`.

### Additional effects
This function also what I think is a secondary problem.
`stratifyArrays` runs **after** the normalization of the gene expression values (to the range 0-255), but this can be problematic.
If Gene A has a range of [0, 1000] and Gene B has a range of [0, 10], normalizing them individually maps both max values to 255.
* **Incorrect (Normalize -> Sum):** Gene B contributes equally to the visualization color, despite being 100x less abundant.
* **Correct (Sum -> Normalize):** We calculate `1000 + 10 = 1010` first. Gene A dominates the signal, preserving biological reality.

The data pipeline is now strictly ordered as follows:

1.  **Aggregate (`aggregateFeatureArrays`):** Combines raw float arrays (*N* features -> *1* array).
    * *Note:* This function is strictly optimized for vector operations and returns a standard Array.
2.  **Normalize (`useUint8FeatureSelection`):** Calculates global min/max of the *aggregated* data and scales to Uint8.
3.  **Stratify (`stratifyArrays`):** Groups the optimized Uint8 data into Sample/Cell Set hierarchies for rendering.

## Open questions
- Is `packages/utils/other-utils/src/expr.ts` for that type of function? I couldn't find any better place.
- Is the stratification after normalization a wanted behavior? In that case I can change the code to restore the previous behavior for `stratifyArrays`
- Since `stratifyArrays` takes in input the aggregated values (if multiple genes are selected, the aggregation code inside `stratifyArrays` becomes useless if I am not mistaken. Should I change it?

#### Checklist
 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c9eb6a543ec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.