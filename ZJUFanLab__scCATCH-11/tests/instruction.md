# Issue

**Title:** fix the problem of large sparse matrix of Seurat

## Description

If the Seurat use the very large sparse matrix to store gene expression matrix,  the `as.data.frame` will not work. So, I remove the `as.data.frame` and use Matrix::rowMeans to calculate the means of sparse matrix. Becuase, the rowMeans will still convert the data.frame to matrix, it is not neccessary to convert the orgin matrix to data.frame.

>原来代码中用了as.data.frame去转换Seurat的表达量矩阵，而R语言是无法直接处理非常大的稀疏矩阵，参考[R语言的稀疏矩阵学习记录](http://xuzhougeng.top/archives/R-Sparse-Matrix-Note)，而且后续使用的 rowMeans去计算均值时，R语言会把data.frame转成matrix再计算，因此，源代码中的as.data.frame可以删除. 并且不会影响最终运行结果

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4242642ac1e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.