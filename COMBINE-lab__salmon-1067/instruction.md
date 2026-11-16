# Issue

**Title:** fix(docker): install procps so the image works with Nextflow

## Description

.

Nextflow shells into the task container and calls `ps` to collect task metrics, failing the task outright when it is missing. `debian:bookworm-slim` does not ship `procps`, so `combinelab/salmon` could not be used as a Nextflow process container.

Thanks to @rich7409 for the report — it named the exact package and the exact failure mode, which made this a short investigation.

## What was actually missing

I audited `debian:bookworm-slim` against [Nextflow's container requirements](https://www.nextflow.io/docs/latest/container.html) rather than assuming:

```
bash OK    sed  OK    egrep OK    tail OK    date  OK    touch OK
ps   MISSING          grep  OK    awk   OK    tee  OK    cat   OK    mkdir OK    rm OK
```

`ps` is the only gap, so this one package is the whole fix.

## Verification

Built the runtime stage both ways with the change isolated to it:

| | result |
|---|---|
| without `procps` | `Command 'ps' required by nextflow to collect task metrics cannot be found` — the reported error, verbatim |
| with `procps` | `ps found: /usr/bin/ps`, and Nextflow's `nxf_tree` probe (`ps -e -o pid= -o ppid=`) returns |

Also confirmed nothing else regressed: `docker run <image> --version` and `... quant --help` still work through the `salmon` entrypoint, and a real `salmon index` run completes inside the container.

Cost is **+1,349,175 bytes (~1.3 MB, +1.25%)** — `procps` 2.1 MB plus `libproc2-0` 232 kB installed.

## Build-time guard

`ps` is now checked in the sanity step, not just installed:

```dockerfile
RUN salmon --version     && command -v ps >/dev/null
```

so dropping the package or changing the base image fails the build rather than silently shipping an image that breaks every Nextflow task at runtime. Confirmed the guard bites — removing `procps` fails at that step with exit 127.

## One thing I did *not* change

The `salmon` ENTRYPOINT stays as-is. It is what makes the documented `docker run combinelab/salmon quant ...` usage work, and changing it would break that for existing users. It does mean a workflow manager supplying its own command gets swallowed:

```console
$ docker run --rm combinelab/salmon:latest /bin/bash -ue -c 'echo hi'
error: unrecognized subcommand '/bin/bash'
```

The reporter's error shows their setup already gets past this, but it is an easy adjacent trap, so the install docs now cover it (`docker.entrypointOverride = true` for Nextflow) next to the `procps` note. Happy to revisit the entrypoint separately if you'd rather the image be drop-in for workflow managers.

## Publishing

This only takes effect when the image is rebuilt. `.github/workflows/docker.yml` runs on release tags, but also supports **Actions → "Docker image" → Run workflow** to refresh an already-released version — worth doing for 2.3.4 so @rich7409 doesn't have to wait for the next release.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01R5jNNvJnFRiu2eC1JZAu2T

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6e32be98e9d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.