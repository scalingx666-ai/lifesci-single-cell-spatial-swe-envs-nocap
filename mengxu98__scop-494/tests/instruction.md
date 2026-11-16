# Issue

**Title:** refactor: remove dependency commit pins and validate workflow articles

## Description

The load and analysis environments should accept compatible installed package revisions. Remove handwritten commit constraints while preserving runtime checks and observed provenance. This PR also executes supported workflow articles, repairs enrichment and small spatial benchmark examples, and documents the remaining unevaluated optional extensions.

The article changes incorporate #489 and repair its GSEA mapping inconsistency. Trajectory and pancreatic-development examples use all 1,000 bundled cells; BANKSY uses 10 expression neighbors for the 36-spot simulation. RunSingleR documentation and the README SCENIC link are repaired.

## Dependency policy

Handwritten GitHub package installations follow the repository default branch. Automatically generated renv.lock entries remain unchanged.

- Remove commit suffixes from Harmony, optional-backend workflows, and PrepareEnv's R/Python package specifications. Both article-building workflows install the official unpinned Harmony source. The two integration articles check its repository origin and report the observed revision.
- CHOIR accepts the installed backend revision, retains argument compatibility checks, and records actual revision metadata.
- Cell2fate records the installed Git revision and only reuses completed results from that same revision. Input, parameter, artifact integrity and result ownership checks remain in place.
- COMMOT and SpatialDM record a commit from the execution manifest when available, otherwise an unknown value, instead of attributing every run to an old fixed revision.
- Mouse GO annotation, shadowtext and the official unpinned Monocle3 source are installed by the articles/full-site workflows rather than DESCRIPTION. The reference workflow does not install Monocle3.

## Original article validation

- Ten articles rendered locally, producing 51 figures; inspected the changed workflow figures and repaired the clipped dynamic heatmap. The full differential/enrichment article also passed an actual pkgdown build.
- The simulated BayesSpace, BANKSY and SmoothClust benchmark completed successfully, including a rerun after #486 merged.
- All 12 article sources parse; all 354 Rd files parse as UTF-8. All 348 exported interfaces have help aliases. RunSingleR argument coverage, unchanged function body/signature, checkDocFiles and its pkgdown reference page passed focused validation.
- Audited 366 published pages and 604 referenced image URLs. Pages and site-hosted images were accessible after retries; five external Shields badge requests returned 403.
- pkgload::load_all(..., compile = FALSE) passed. With _R_CHECK_FORCE_SUGGESTS_=false, the required no-manual/as-cran/no-examples/no-tests check completed with 0 errors, 2 warnings and 3 notes after correcting the Windows cross-volume temporary-directory issue. The RunSingleR documentation warning was subsequently repaired and checked separately; a dependency warning remains for the locally installed thisplot::NetworkPlot and thisutils::fit_trends interfaces. Unstated dependencies in examples: OK. The remaining notes concern existing metadata/DOI/Makevars fields.

## Follow-up validation

Head `9d3b4989b289cf5dea095f041896308893821429`:

- 62 focused cases passed 331 assertions with no failures, errors, warnings or skips. The Python runner regression exercises arbitrary observed revisions and invalidates cached results when the current revision changes.
- Real calls to the currently available default-branch Harmony 2.0.4 and CHOIR 0.3.0 passed on 80 synthetic cells; cell order and result provenance were checked. CHOIR returned two clusters and emitted two upstream reduction warnings.
- pak resolved both unpinned GitHub references. actionlint, changed R/vignette/Python parsing, generated help parsing and diff checks passed. Formatting preserved the parsed code. Final shared changes match across both PR branches.
- No handwritten package SHA constraint remains in tracked installation specifications or backend acceptance checks. Source attribution permalinks, observed revision records and renv.lock are retained.

The focused R tests load changed source with the installed native library; C++ was not modified or rebuilt locally. Complete optional-backend installations, Python model training and full article reruns were not repeated. No article/full-site deployment or PR merge was performed. New-head CI is separate from the original validation above. Future default-branch releases still require compatible backend interfaces.

Original rendering and checking preceded the final sync to main; dynamic fitting used thisutils source c158ee4. Python fate/regulatory models and external vendor-data extensions were not executed.

Both branches include main bb076b72d after #495, preserving its SCT changes alongside the dependency policy. Focused tests and native Harmony/CHOIR checks were repeated after this synchronization.

## Monocle3 dependency follow-up

Head `6a8030abc526ebd86c1319be6902645c5de7dc32` moves `github::cole-trapnell-lab/monocle3` from `Config/Needs/website` to the `articles` and `full-site` workflow dependency steps. This update changes only those two workflows and DESCRIPTION.

- pak successfully resolved the official default branch and its hard dependencies; the observed Monocle3 version was 1.4.27. No handwritten SHA constraint was added.
- Both changed workflows passed actionlint. DESCRIPTION and affected Rd files parsed successfully.
- In an isolated library without Monocle3, the PR home page and Monocle3 reference page built successfully with the reference workflow's default example behavior. All three local README image references resolved.
- A temporary integration with current main and the uncommitted CI optimization retained dependency-aware caches, hard-only reference dependencies, two installation workers, article change filtering and disabled reference examples. Its home, Monocle3 and SingleR pages built without warnings. Six incremental scope cases passed for both the PR and integrated workflows, including mixed README/Rd/NEWS changes and image-only changes. SingleR runtime code matched exactly.
- The integration required text conflict resolution in pkgdown, SingleR source/help and NEWS. These resolutions were validated in the temporary checkout; the uncommitted CI work was not included in this PR update. The primary checkout and local CI changes were preserved, and the 12-platform R-hub configuration was unchanged.

The full Monocle3 installation, trajectory analyses and complete package test suite were not repeated for this dependency-placement change. Local validation does not replace new-head GitHub CI. No PR merge or article/full-site deployment was performed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8339f62cdf83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.