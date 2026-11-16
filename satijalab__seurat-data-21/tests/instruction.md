# Issue

**Title:** Add support for no "Description" data

## Description

It seems that some data don't have "Description":

    % curl https://seurat.nygenome.org/src/contrib/PACKAGES | head
    1544
    Package: cbmc.SeuratData
    Version: 3.0.0
    Suggests: Seurat (>= 3.0.0)
    License: CC BY 4.0
    MD5sum: a622946afeb8ce86a8f8361ef350d92e
    NeedsCompilation: no

    Package: hcabm40k.SeuratData
    Version: 3.0.0
    Suggests: Seurat (>= 3.0.0)

It causes install failure:

    > devtools::install_github("satijalab/seurat-data")
    ...
    ** testing if installed package can be loaded from temporary location
    Error: package or namespace load failed for 'SeuratData':
     .onAttach failed in attachNamespace() for 'SeuratData', details:
      call: x[[2]]
      error: subscript out of bounds
    Error: loading failed
    Execution halted
    ERROR: loading failed
    ...
    > traceback()
    8: stop(remote_install_error(remotes[[i]], e))
    7: value[[3L]](cond)
    6: tryCatchOne(expr, names, parentenv, handlers[[1L]])
    5: tryCatchList(expr, classes, parentenv, handlers)
    4: tryCatch(res[[i]] <- install_remote(remotes[[i]], ...), error = function(e) {
           stop(remote_install_error(remotes[[i]], e))
       })
    3: install_remotes(remotes, auth_token = auth_token, host = host,
           dependencies = dependencies, upgrade = upgrade, force = force,
           quiet = quiet, build = build, build_opts = build_opts, build_manual = build_manual,
           build_vignettes = build_vignettes, repos = repos, type = type,
           ...)
    2: pkgbuild::with_build_tools({
           ellipsis::check_dots_used(action = getOption("devtools.ellipsis_action",
               rlang::warn))
           {
               remotes <- lapply(repo, github_remote, ref = ref, subdir = subdir,
                   auth_token = auth_token, host = host)
               install_remotes(remotes, auth_token = auth_token, host = host,
                   dependencies = dependencies, upgrade = upgrade, force = force,
                   quiet = quiet, build = build, build_opts = build_opts,
                   build_manual = build_manual, build_vignettes = build_vignettes,
                   repos = repos, type = type, ...)
           }
       }, required = FALSE)
    1: devtools::install_github("satijalab/seurat-data")

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `12c77a87df8d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.