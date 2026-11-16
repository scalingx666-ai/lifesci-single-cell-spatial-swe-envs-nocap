# Issue

**Title:** [r] Improve trackplot_combine layout logic

## Description

Add several improvements to the `trackplot_combine` layout logic.

For plots without sideplots, before and after are as follows:
- Preserve vertical margins when stacking scalebars, and make sure they won't remove the x-axis label of the plot above them
- Detect when tracks change the genomic region they are plotting and show a new x-axis appropriately
- Fix the `trackplot_gene()` color legend to always show both + and - strand
- Fix `trackplot_scalebar()` to change the font size as requested (before it just affected track height)
- Switch color legends to vertical layout by default, and only use horizontal layout when a side plot is present
- Shorten the y-axis label for `trackplot_coverage()` to reduce (though not eliminate) the likelihood of the label getting cut off

And, when `side_plot` is present:
- Use horizontal color legend layout
- Pick the first plot that accepts a side-plot rather than the last (some day we might want to add an argument to manually position the side plot)

<details>
<summary>Script used for plotting demo (relies on the `pbmc-3k` vignette data)</summary>

```r
library(BPCells)
# devtools::load_all()

frags_raw <- open_fragments_dir("vignettes/pbmc-3k-data/pbmc_3k_frags")
mat_raw <- open_matrix_dir("vignettes/pbmc-3k-data/pbmc_3k_rna_raw")

blacklist <- read_encode_blacklist("vignettes/pbmc-3k-data/references", genome="hg38")
chrom_sizes <- read_ucsc_chrom_sizes("vignettes/pbmc-3k-data/references", genome="hg38")
transcripts <- read_gencode_transcripts("vignettes/pbmc-3k-data/references", release="42")
genes <- read_gencode_genes("vignettes/pbmc-3k-data/references", release="42")

atac_qc <- qc_scATAC(frags_raw, genes, blacklist)

pass_atac <- atac_qc |>
    dplyr::filter(nFrags > 1000, TSSEnrichment > 10) |>
    dplyr::pull(cellName)
pass_rna <- colnames(mat_raw)[colSums(mat_raw) > 1e3]
keeper_cells <- intersect(pass_atac, pass_rna)

frags <- frags_raw |> select_cells(keeper_cells)
keeper_genes <- rowSums(mat_raw) > 3
mat <- mat_raw[keeper_genes,keeper_cells]


######################################
# RNA-based clustering
######################################
# Normalize by reads-per-cell
mat <- multiply_cols(mat, 1/Matrix::colSums(mat))
# Log normalization
mat <- log1p(mat * 10000)
stats <- matrix_stats(mat, row_stats="variance")

# To keep the example small, we'll do a very naive variable gene selection
variable_genes <- order(stats$row_stats["variance",], decreasing=TRUE) |> 
  head(1000) |> 
  sort()
mat_norm <- mat[variable_genes,]
mat_norm <- mat_norm |> write_matrix_memory(compress=FALSE)
gene_means <- stats$row_stats["mean",variable_genes]
gene_vars <- stats$row_stats["variance", variable_genes]
mat_norm <- (mat_norm - gene_means) / gene_vars

svd <- BPCells::svds(mat_norm, k=50)
pca <- multiply_cols(svd$v, svd$d)

clusts <- knn_hnsw(pca, ef=500) |> # Find approximate nearest neighbors
  knn_to_snn_graph() |> # Convert to a SNN graph
  cluster_graph_louvain() # Perform graph-based clustering

cluster_annotations <- c("1" = "T", "2" = "CD8 T", "3" = "B", "4" = "T", "5" = "NK", "6" = "Mono", "7" = "Mono", "8" = "Mono", "9" = "T", "10" = "DC", "11" = "Mono", "12" = "DC")
cell_types <- cluster_annotations[clusts]


region <- gene_region(genes, "CD19", extend_bp = 1e5)
region_narrow <- list(chr="chr16", start=28931964-100, end=28931964+100)
read_counts <- atac_qc$nFrags[
  match(cellNames(frags), atac_qc$cellName)
]

coverage_plot <- trackplot_coverage(
  frags,
  region = region, 
  groups=cell_types,
  read_counts,
  bins=500
)

gene_plot <- trackplot_gene(transcripts, region)
scalebar_plot <- trackplot_scalebar(region)

fake_peaks <- c(28846253, 28863641, 28925327, 28950995, 28974593)
fake_loops <- tibble::tibble(
  chr = "chr16",
  start = fake_peaks[c(1,1,2,3)],
  end = fake_peaks[c(2,3,4,5)],
  score = c(4,1,3,2)
)
loop_plot <- trackplot_loop(fake_loops, region, color_by="score")


region_narrow <- list(chr="chr16", start=28931964-500, end=28931964+500)
cell_subset <- cellNames(frags)[cell_types %in% c("B", "DC")]
coverage_plot_narrow <- trackplot_coverage(
    frags |> select_cells(cell_subset), region=region_narrow, groups=cell_types[cell_types %in% c("B", "DC")], read_counts[cell_types %in% c("B", "DC")], bins=200, 
)
gene_plot_narrow <- trackplot_gene(transcripts, region_narrow)
scalebar_narrow <- trackplot_scalebar(region_narrow, font_pt=8)

expression <- collect_features(mat, "CD19")
names(expression) <- "gene"
expression_plot <- ggplot2::ggplot(expression, ggplot2::aes(cell_types, gene, fill=cell_types)) +
    ggplot2::geom_boxplot() + 
    ggplot2::guides(y="none", fill="none") + 
    ggplot2::labs(x=NULL, y="RNA") +
    ggplot2::scale_fill_manual(values=discrete_palette("stallion"), drop=FALSE) +
    BPCells:::trackplot_theme()

plot1 <- trackplot_combine(
  list(
    scalebar_plot, 
    coverage_plot, 
    gene_plot,
    loop_plot,
    coverage_plot_narrow,
    gene_plot_narrow,
    scalebar_narrow
  )
)
ggplot2::ggsave(plot=plot1, "pre_trackplot.png", width=8, height=8, units="in")

plot2 <- trackplot_combine(
  list(
    scalebar_plot, 
    coverage_plot, 
    gene_plot,
    loop_plot,
    coverage_plot_narrow,
    gene_plot_narrow,
    scalebar_narrow
  ),
  side_plot = expression_plot
)
ggplot2::ggsave(plot=plot2, "pre_trackplot_with_side.png", width=8, height=8, units="in")

```

</details>

<details>
<summary> Before (no sideplot)</summary>

![pre_trackplot](https://github.com/user-attachments/assets/822d94fc-f019-4a59-a6d0-5474b1a4fa52)

</details>

<details>
<summary> After (no sideplot)</summary>

![trackplot](https://github.com/user-attachments/assets/df01c25d-7949-45c9-8cce-834b27491e7f)

</details>


<details>
<summary> Before (with sideplot)</summary>

![pre_trackplot_with_side](https://github.com/user-attachments/assets/7df80b67-61dd-45b4-888f-d5e0110822d1)

</details>

<details>
<summary> After (with sideplot)</summary>

![trackplot_with_side](https://github.com/user-attachments/assets/3f3507df-48c5-4632-8766-18554945c81b)

</details>

<details>

<summary> After with a low sideplot (see code from comment below) </summary>

![trackplot_with_low_side](https://github.com/user-attachments/assets/a0ce1d2a-2168-4794-8223-7e5a62dfe864)

</details>

(Edited to update plot previews with the later improvements)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f6a84e148522`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.