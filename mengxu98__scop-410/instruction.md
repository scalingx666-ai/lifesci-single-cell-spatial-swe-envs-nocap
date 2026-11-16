# Issue

**Title:** fix(giotto): stop optional-backend round-trip timeout

## Description

<!-- CURSOR_AGENT_PR_BODY_BEGIN -->
## Cause

`optional (giotto)` on main failed in run [34322458550](https://github.com/mengxu98/scop/actions/runs/34322458550) after the suite filter was pointed at `framework-bridges`. That live test had **never run** under this workflow: the previous filter `giotto` matched no files (`No test files found`).

The 120s `callr` timeout was not a near-miss. Two real stalls stacked:

1. **Isolated runner reloads the whole source tree.** `test_local(load_package = "source")` already spends ~3 minutes on `load_all` in the parent. The live test then `callr::r(..., timeout = 120)` + `pkgload::load_all` again, so the child expires before conversion starts.
2. **`check_r("drieslab/Giotto")` reinstalls Giotto.** Optional CI pins `giotto-suite/Giotto@080d2e…`. `thisutils::check_r()` treats a different GitHub remote as missing and runs `pak::pkg_install("drieslab/Giotto")` inside that 120s window. The bundled Visium object (5000 genes × 1986 spots, full HE raster) is also far larger than a converter smoke test needs; GiottoClass `seuratToGiottoV5()` additionally rasterizes the image through terra.

Other optional suites on the same run (monocle2, tage, cibersort) were unrelated and already passing.

## Change

- Reuse an already-installed **GiottoClass** (`check_r(..., install = FALSE)`). Request `drieslab/Giotto` only when GiottoClass is missing.
- Disable Giotto Python/conda and GitHub version checks for the duration of conversion.
- Replace the `callr` + full Visium live test with a tiny in-process VisiumV1 fixture (3 genes × 3 spots, 8×8 raster) that still calls the real GiottoClass v4/v5 converters.
- Add mocked tests for the GitHub-reinstall vs reuse split.
- Guard the documented `srt_to_giotto` / `giotto_to_srt` examples with `thisutils::check_r("GiottoClass", install = FALSE)` and convert only when GiottoClass is already present, so examples do not reinstall `drieslab/Giotto` over a `giotto-suite` pin.

## Verify

- Workflow: `.github/workflows/optional-backends.yaml`
- Job: `optional (giotto)`
- Test: `srt_to_giotto and giotto_to_srt round-trip with a real GiottoClass` in `tests/testthat/test-framework-bridges.R`
- Trigger: `workflow_dispatch` on `optional-backends` (this workflow is schedule/dispatch only, not pull_request). Mocked bridge tests also run in the regular R CMD check suite.
<!-- CURSOR_AGENT_PR_BODY_END -->

<div><a href="https://cursor.com/agents/bc-8bd6cca3-7812-4448-aebb-ee49a7da8aff?cursor_ref=pr_footer&cursor_cta=open_in_web"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-web-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-web-light.png"><img alt="Open in Web" width="114" height="28" src="https://cursor.com/assets/images/open-in-web-dark.png"></picture></a>&nbsp;<a href="https://cursor.com/background-agent?bcId=bc-8bd6cca3-7812-4448-aebb-ee49a7da8aff&cursor_ref=pr_footer&cursor_cta=open_in_cursor"><picture><source media="(prefers-color-scheme: dark)" srcset="https://cursor.com/assets/images/open-in-cursor-dark.png"><source media="(prefers-color-scheme: light)" srcset="https://cursor.com/assets/images/open-in-cursor-light.png"><img alt="Open in Cursor" width="131" height="28" src="https://cursor.com/assets/images/open-in-cursor-dark.png"></picture></a>&nbsp;</div>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d6f94950ccbe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.