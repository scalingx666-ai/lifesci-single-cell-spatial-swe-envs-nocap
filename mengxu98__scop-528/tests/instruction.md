# Issue

**Title:** Add capture-specific MACS2 peak calling with persistent execution records

## Description

Add capture/group-specific MACS2 2.x peak calling with native Signac fragment splitting. Keep separate peak sets and preserve actual arguments, process status, logs and source-cell mappings. Nonzero caller exits and malformed output are errors; a successfully empty narrowPeak file remains an empty result.

The current revision resolves an executable path or a command on PATH (default macs2), rejects directories/missing executables, and writes receipt.rds plus groups.rds before splitting/calling. Failed runs retain capture/group membership and resource provenance; commands.rds and receipt.rds record completed process statuses. Existing destinations remain protected.

Only the peak-calling API, export/index entry, generated help and focused tests differ from current main 8811fce70. The MACS2 calling arguments and statistical method are unchanged. #529 includes this head as a tutorial dependency.

Focused caller tests: 29 assertions passed, with native fragment splitting/parsing and mocked subprocess results, including PATH lookup and persistent failure records. Fresh external MACS2 acceptance remains blocked by Docker Desktop failing to initialize its local inference socket. No Docker reset, dependency installation or caller substitution was performed.

Validation on the combined source:
- Full ATAC regression suite: 1,084 assertions passed, 0 failures/errors, 4 explicit skips and 8 warnings. Skips are unavailable variancePartition, Windows symlink coverage, and two CSI-index fixtures requiring tabix.
- Adjacent RNA/integration tests: 128 assertions passed, 0 failures/errors, 2 optional-environment skips.
- Final focused workflow, WNN, caller and dispatcher recheck: 136 assertions passed, 0 failures/errors, 1 unrelated Coralysis skip.
- Real 10x PBMC import and analysis: 15,856 chr1 peaks x 1,000 cells; TF-IDF agrees with native Signac, dimension/depth records are checked, and motif matching, chromVAR, export and reload complete.
- Real paired DAR: 20,950 chr1 intervals x 1,151 cells from eight captures/four donors. Fresh fragment recount agrees with the input counts; 2,245 tested peaks have edgeR logFC, P values and BH results matching direct edgeR calls to 1e-12 tolerance.
- All four articles render; the packaged matrix and WNN examples execute. External-data recipe rendering is not counted as fresh external inference.
- Required current-source pkgload::load_all(..., compile=FALSE) and R CMD check --no-manual --as-cran --no-examples --no-tests completed: process status 0, no timeout, 0 errors, 0 warnings, 4 notes. R-code and example dependency checks are OK. Notes concern existing CRAN metadata/DOI URL style, external clock verification, maintainer-name ordering and spatial_record_cell_identity's unqualified tail. Earlier cross-volume linking and WNN help omissions were resolved before this final check; the retry used a process-local D: temporary directory.
- Public APIs in the installed final package also pass an 80-measured-cell WNN acceptance, including retained scaled RNA, ATAC counts, source reductions, dimension records and joint UMAP.
- MACS2 subprocess execution is mocked in the unit tests. A fresh external MACS2 run is blocked by the local Docker startup failure; historical MACS2 acceptance is not substituted for it.

The data runs are chromosome-scoped software acceptance, not a whole-genome biological validation. No canonical-library dependency installation or package-version change was made. Hosted checks on the updated heads are pending.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f44f8c52c24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.