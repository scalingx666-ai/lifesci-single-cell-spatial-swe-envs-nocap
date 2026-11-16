# Issue

**Title:** fix: handle underscores in SCENIC heatmap features

## Description

## 问题

`SCENICPlusPlot(..., plot_type = "rss_heatmap")` 与 `plot_type = "activity_heatmap"` 在 regulon 名含 `_` 时会因 Seurat 对特征名的规范化而报 assay/layer feature overlap 错误。activity assay 还可能因规范化后的重复名称而无法创建。

## 修复

- 为 Seurat assay/热图对象生成规范化且唯一的内部 feature ID。
- RSS/activity 热图将原始 regulon 名保留为显示标签和返回数据。
- violin/dim 路径使用同一 feature ID 映射。
- 添加 RSS 和 activity heatmap 回归测试，覆盖下划线与 RSS 映射冲突。

## 验证

- RSS heatmap 原有测试通过。
- 含下划线及映射冲突的 SCENICPlus RSS heatmap 测试通过。
- 含下划线的 SCENICPlus activity heatmap 测试通过。
- activity heatmap、activity violin、activity dim 和 overlap 相邻测试通过。
- `git diff --check` 通过。

本机完整 `scenic-plot` 文件测试另有依赖问题：已安装的 `thisplot` 未导出 `NetworkPlot`，与本 PR 的热图路径无关。

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0ac5350c98d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.