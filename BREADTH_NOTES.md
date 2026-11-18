# Build notes - Single-cell & Spatial Omics

Repo2RLEnv pr_diff (v0.9.6), Harbor-format output. Domain: single-cell-spatial.

## Funnel

| Stage | Count |
|---|---|
| Domain candidates (deduped) | 497 |
| After active+star+noise filter | 304 |
| Final target list (cap unlimited) | 304 |
| Repos with >=1 task | 203 |
| Repos with 0 tasks | 47 |
| Total tasks (unlimited (no per-repo cap)) | 6909 |

## Generation

- Shared task bank: each repo generated once (pr_diff, limit=3,
  max_files_per_pr=15, min_loc_changed=2), 4-way concurrency,
  rate-limit-aware with .done checkpoint resume.
- Per-domain consolidation: rank by reward_calibration.loc_changed desc,
  keep ALL qualifying tasks (no per-repo cap). Zero-yield repos are NOT fabricated.
- Overlap with the 3 published cancer editions is allowed (user decision);
  domains are independent selections, not a partition of one repo set.

## Zero-yield repos (informational, 47)

- theislab/single-cell-best-practices
- test-time-training/discover
- HazyResearch/aisys-building-blocks
- Graph-RAG/GraphRAG
- 10XGenomics/cellranger
- zezhishao/DailyArXiv
- kpatel427/YouTubeTutorials
- carmonalab/ProjecTILs
- TobaccoDB/iPscDB
- GuangyuWangLab2021/Loki
- CelVoxes/ceLLama
- Lotfollahi-lab/nichecompass
- rezakj/iCellR
- Teichlab/cellhint
- Dragonmasterx87/Interactive-3D-Plotting-in-Seurat-3.0.0
- pachterlab/kallistobustools
- saezlab/visium_heart
- pachterlab/voyager
- fanglu0411/sgs
- QING1105/ezST
- axelalmet/flowsig
- eleozzr/desc
- GfellerLab/EPIC
- YangLabHKUST/SpatialScope
- ma-compbio/SpiceMix
- YangLabHKUST/STitch3D
- chenhcs/SCS
- shangll123/SpatialPCA
- RucDongLab/STAGATE_pyG
- WXlab-NJMU/scrna-recom
- genecell/COSGR
- xiaoyeye/CCST
- greenelab/BioBombe
- LiuLab-Bioelectronics-Harvard/STAgent
- gaolabtools/scNanoGPS
- epigen/scrnaseq_processing_seurat
- VCCRI/Sierra
- ZJUFanLab/scNiche
- PharMolix/SToFM
- epigen/dea_seurat
- epigen/mixscape_seurat
- RucDongLab/STAGATE
- digitalcytometry/spatialecotyper
- BaderLab/scClustViz
- zhoux85/STAligner
- amesch441/iSCALE
- YMa-lab/IRIS

## Caveats

- Static validation only; real grading needs an LLM judge key + Docker.
- inline_dockerfile mode skips image build (no Docker daemon needed to publish).
- Provider secrets in upstream diffs were redacted before public release.
