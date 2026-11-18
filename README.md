# scalingX/lifesci-single-cell-spatial-swe-envs-nocap

A domain-specific SWE-style RL environment dataset built from merged pull
requests of active, high-star Single-cell & Spatial Omics open-source repositories,
generated with the Repo2RLEnv pr_diff pipeline (Harbor task format).

Part of the lifesci-* multi-domain series. Published in parallel:
- Hugging Face: https://huggingface.co/datasets/scalingX/lifesci-single-cell-spatial-swe-envs-nocap
- GitHub: https://github.com/scalingx666-ai/lifesci-single-cell-spatial-swe-envs-nocap

## At a glance

- Build: expansion (no per-repo cap expansion)
- Target repositories: 250
- Repositories with tasks: 203
- Total tasks: 6909
- Max tasks per repository: 204 (unlimited (no per-repo cap))
- Repositories with zero yield: 47 (kept in list, never faked)
- All targets: stars >= 50, pushed since 2023-01-01, not archived, noise-filtered

## Selection

Candidates came from domain GitHub topic/name/readme searches
(see selection_stats.json). Filter: active + stars >= 50 + non-archived +
non-fork + noise removed (awesome-lists / tutorials / courses / demos / etc.).
Top repositories by stars:
- K-Dense-AI/scientific-agent-skills (57129 stars)
- FreedomIntelligence/OpenClaw-Medical-Skills (3107 stars)
- zhoushengisnoob/DeepClustering (3060 stars)
- satijalab/seurat (2817 stars)
- scverse/scanpy (2615 stars)
- hexo-ai/sia (2170 stars)
- aipoch/medical-research-skills (2055 stars)
- scverse/scvi-tools (1727 stars)
- bowang-lab/scGPT (1666 stars)
- pavlin-policar/openTSNE (1625 stars)

Star buckets: {">=1000": 17, "500-999": 38, "200-499": 104, "100-199": 71, "50-99": 74}

## What a task is

Each task rewinds a merged PR to its base commit; the agent gets the PR title/
description (leak-stripped) and must edit the repo. A weighted diff-similarity
verifier compares its patch to the merged diff. Tasks ship a self-contained
python:3.12-slim inline Dockerfile. manifest.json / registry.json are added on
Hugging Face by repo2rlenv push.

## Files

- README.md, BREADTH_NOTES.md - card + build notes
- repo_list.txt - the domain target list
- dataset_stats.json - per-repo task counts
- selection_stats.json - selection funnel + star buckets
- zero_repos.txt - informational zero-yield list

## Caveats

- validate --deep --oracle = static structure + oracle integrity only, NOT
  a real graded Harbor reward (that needs an LLM judge key).
- Running tasks needs Docker (harbor run --env docker); generation/validation/
  publishing need neither Docker nor an LLM key.
- Hardcoded provider keys found in upstream PR diffs were redacted for public
  release. Licenses follow each source repository; generated with Repo2RLEnv.
