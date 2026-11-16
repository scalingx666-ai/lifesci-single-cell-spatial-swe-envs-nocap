# Issue

**Title:** fix find_mark_gene and update requirements

## Description

1. 为解决因第三方包版本不一致导致结果差异较大的问题，将>=的包更新至py37支持的最新版。find mark
gene的报错行为一致了，但找到的mark
gene仍有区别。由于用到了聚类结果，向前追溯发现Neighbors这一步里有random操作，可以对此检查一下。
2. 增加bokeh包以解决在linux py38环境通过setup安装时会中断一次的问题

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce7cdccfbc06`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.