# Issue

**Title:** [r] Adjust default parameters for `cluster_graph_leiden()`

## Description

Currently, `cluster_graph_leiden()` by default will output a number of clusters that scales approximately linearly with number of cells if the `resolution` parameter is held constant. This is generally not good and leads to problems like  where people get thousands of clusters called on large datasets.

This pull request does the following:
- Changes default `objective_function` from `CPM` to `modularity` sets default `resolution` back to 1.
- Moves clustering-related tests to a new file and makes a basic test to confirm that the clustering functions at least don't crash. I don't know of a good way of validating the clustering is working, so not crashing seems good enough for now.

Here is the benchmarking data to justify this change. Note that Leiden modularity with resolution = 1 gives consistent cluster sizes just like Louvain, but Leiden CPM will give out a ton of clusters for large datasets unless the resolution parameter is adjusted down for large datasets.

![resolution_plot](https://github.com/user-attachments/assets/53a6d1de-b9b4-486c-b9a2-17b8525dc161)

[cluster-resolution.csv](https://github.com/user-attachments/files/17516416/cluster-resolution.csv)

<details>
<summary> Click for plotting code </summary>

```r
data |>
  mutate(alg=case_match(alg, "leiden" ~ "Leiden CPM", "leiden-modularity" ~ "Leiden Modularity", "louvain" ~ "Louvain"),
         resolution=factor(as.numeric(resolution), sort(unique(as.numeric(resolution))))) |>
  ggplot(aes(cells, clusts, color=resolution)) +
  geom_line() +
  geom_point() +
  scale_x_continuous(transform="log10", guide=guide_axis_logticks(), labels=scales::label_log(), breaks=c(1e5, 1e6)) +
  scale_y_continuous(transform="log10", guide=guide_axis_logticks()) +
  scale_color_manual(values=RColorBrewer::brewer.pal(9, "BuPu")[3:9]) +
  facet_wrap("alg") +
  theme_bw() + 
  coord_fixed() +
  labs(title="Cluster counts by resolution", y="Cluster count", x="Dataset size (cells)")
```
</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `334f172ea8e4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.