# Issue

**Title:** Fetch the datasets from exampledata.scverse.org

## Description

Moves every dataset used by liana off the dead figshare links onto https://exampledata.scverse.org/liana, fetched via a `registry.yaml` that `scverse_misc.datasets.fetch` resolves with sha256 verification and figshare/cellxgene fallbacks.
`li.ds` now also exposes `kuppe_2022`, `citeseq_pbmc5k`, `vicari_2024` and `yao_2023`, which the tutorials used to download by URL (scverse/liana-tutorials#2).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9c2246ea7fc8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.