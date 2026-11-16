# Issue

**Title:** Switch from leiden to leidenbase

## Description

The Leiden implementation provided by `leiden` is absurdly slow, way more than I'd expect from the overhead of calling reticulate. This switches for the (mostly) equivalent `leidenbase`. Tests pass locally for me, see also the demo below comparing 3 Leiden implementations.

See https://github.com/satijalab/seurat/discussions/6754

```r
library("leidenbase")
library("leidenAlg")
library("leiden")
library("igraph")
library("microbenchmark")

fpath <- system.file('testdata', 'igraph_n1500_edgelist.txt.gz', package='leidenbase')
zfp <- gzfile(fpath)
igraph <- read_graph(file = zfp, format='edgelist')

microbenchmark(
    leidenAlg::leiden.community(igraph),
    leidenbase::leiden_find_partition(igraph),
    leiden::leiden(igraph),
    times = 10
)
# Unit: milliseconds
#                           expr         min          lq        mean      median
#       leiden.community(igraph)    52.98505    55.16530    63.16430    55.95267
#  leiden_find_partition(igraph)    29.22238    30.54163    39.15174    37.57693
#                 leiden(igraph) 17140.52418 20671.12398 21172.11517 21128.94100
#           uq         max neval cld
#     75.38524    80.10432    10  a 
#     40.30238    56.91094    10  a 
#  22268.67866 24597.89747    10   b


r1 <- leiden_find_partition(igraph,
    partition_type = "RBConfigurationVertexPartition",
    seed = 1234,
    resolution_parameter = 1
    
)
r2 <- leiden(igraph,
    partition_type = "RBConfigurationVertexPartition",
    resolution_parameter = 1, 
    seed = 1234
)
table(r1$membership, r2)
#       1   2   3   4   5   6   7   8   9
#   1 295   0   0   0   0   0   0   0   0
#   2   0 209   0   0   0   0   0   0   0
#   3   0   0 201   0   0   0   0   0   0
#   4   0   0   0 191   0   0   0   0   0
#   5   0   0   0   0 175   0   0   0   0
#   6   0   0   0   0   0 170   0   0   0
#   7   0   0   0   0   0   0  93   0   0
#   8   0   0   0   0   0   0   0  85   0
#   9   0   0   0   0   0   0   0   0  81
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ab5374e5621c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.