# Issue

**Title:** feat(sandbox): install into the Volume, and keep analysis out of the runtime venv

## Description

A sandbox is recreated often — on restart, after an idle reclaim, and on every agent-image update — and only the Volume survives that. `apt install vim` writes to `/usr`, which is the image, so it is gone by the next day. That is the whole of "I installed it yesterday and today it is missing".

The obvious fix is to photograph the container and restore it. This does the opposite: it points the package managers themselves at the half of the filesystem that already persists. The packages are then just files on the Volume — nothing to snapshot, nothing to replay, no way to drift out of alignment with the base image, and an image upgrade leaves them alone instead of erasing them.

| | rooted at |
|---|---|
| pip | the analysis env, or `PIP_TARGET=<vol>/.local/pylibs` before it exists |
| npm | `npm_config_prefix=<vol>/.local` |
| R | `R_LIBS_USER=<vol>/.local/Rlib` |
| apt | a shim: fetch the `.deb` + deps, `dpkg -x` into `<vol>/.local/opt` |
| conda | `MAMBA_ROOT_PREFIX=<vol>/.local/micromamba` |

## Analysis does not belong in the runtime venv

`/venv` is what keeps the agent alive. Analysis packages were going into it, so a scanpy upgrade could take the sandbox with it, and two projects with incompatible pins had nowhere to go.

They now go to a **conda env on the Volume**. `python` and `pip` mean that env — for the person at the terminal, for anything the agent shells out to, and for the agent's own Python interpreters — while `/venv` goes back to being only what PantheonOS needs to run.

Measured on staging, in a sandbox that had been released and recreated:

```
run_python_code runs in         .../micromamba/envs/analysis
which python / which pip        .../micromamba/envs/analysis/bin/{python,pip}
PANTHEON_RUNTIME_PYTHON         /venv/bin/python        (the agent, unmoved)
pip install cowsay              → env site-packages
/venv/bin/python -c "import cowsay"  → ModuleNotFoundError   ← isolation holds
```

The env is bridged back to the runtime with a `.pth`. loky spawns each interpreter as a fresh process and unpickles the job function there, so an interpreter that cannot import `pantheon` cannot start; and it means the env carries only what the analysis needs. This works because the env pins the **same CPython minor version** as `/venv`, so the ABI matches — pantheon, pydantic 2.12.5, numpy 2.4.2 and pandas 3.0.5 all import from a conda-forge python 3.12.13. The pin is not decoration; a different minor version fails on the first compiled import.

Two ways into that env, and only one needed patching:

- **notebook** — already correct. `AsyncKernelManager` takes a `kernel_name` and jupyter resolves it to whatever python the spec names, so registering a kernelspec is the whole change, and a second env is a second spec. Verified: `analysis → .../envs/analysis/bin/python`, and a kernel started on it reports `sys.prefix` inside the env.
- **python interpreter** — needs `sys.executable` moved, because on POSIX loky builds the child command line from it directly (`cmd_python = [sys.executable]` in `backend/popen_loky_posix.py`) and consults neither its own `spawn.get_executable()` nor any environment variable. Patching that seam — the one that looks designed for exactly this — changes nothing on Linux; measured. The swap must also be held while the workers actually **start**: loky spawns them lazily, so wrapping the constructor alone left every interpreter in `/venv` while appearing to work.

The env is built **in the background** on first boot — ~70 s once per workspace, against a 21 s boot that is not blocked by it. Until it is ready the sandbox runs on `/venv` with the flat prefix, which is a working sandbox. If it cannot be built, or cannot import the runtime, it is left unused rather than half-wired.

## Why conda at all

Debian's `install.packages()` builds R packages from source, so anything with a C dependency needs headers the image does not carry — and the natural fix does not work either:

```
install.packages("XML")    → installation had non-zero exit status
apt install libxml2-dev    → unpacked into <prefix>/opt   (the shim works)
install.packages("XML")    → STILL fails; R's configure does not look there
```

conda-forge ships that package already built: 39 s, and `library(XML)` loads. Bioconda covers command-line tools the same way — samtools in 5 s, and a newer build than Debian has (1.24 vs 1.16.1). micromamba is one 5 MB static binary; `conda` and `mamba` both run it, since those are the names people type.

## Two decisions worth the words

**`--user` does not work.** The runtime is a virtualenv, and a virtualenv disables `--user` outright — *"Can not perform a '--user' install. User site-packages are not visible in this virtualenv."*

**The flat-prefix fallback uses a `.pth`, not `PYTHONPATH`.** `PYTHONPATH` is searched *before* site-packages, so one `pip install --upgrade pydantic` would shadow the agent's own dependency inside the process that has to keep the sandbox alive. `site` processes a `.pth` by *appending*, so the runtime still wins.

`apt` is intercepted only for `install`; `update`, `search`, `show`, `remove` and the rest go to the real binary, and `PANTHEON_APT_PASSTHROUGH=1` disables interception. `dpkg -x` unpacks without touching the dpkg database, which is what lets this work without owning `/usr` — the trade-off being that maintainer scripts do not run, so a package that is more than "put these files here" is not fully configured. CLI tools and libraries are exactly the case it does handle.

## Verified on staging

Installed, then the sandbox **released and recreated**, then checked in the new one with nothing restored:

```
apt install ncdu           → ncdu 1.18                              SURVIVED
pip install cowsay         → /workspace/.local/pylibs/cowsay        SURVIVED
npm install -g left-pad    → /workspace/.local/lib/node_modules     SURVIVED
install.packages(jsonlite) → /workspace/.local/Rlib                 SURVIVED
import pydantic            → /venv/... (runtime not shadowed)       intact
```

`pip install -e .` still works. Build and module caches stay ephemeral — large, write-heavy, and the Volume is network-backed, the same reason the entrypoint already redirects the pip/HF/torch caches. The conda package cache is the exception and stays on the Volume: it is the working set that makes a second env cheap, and micromamba copies rather than hardlinks out of it (`nlink=1`), so an env does not depend on it once built.

## What running it actually caught

Every one of these was invisible from reading and turned up on staging:

- **loky starts workers lazily** — the swap across the constructor did nothing; interpreters ran in `/venv` while the change reported success.
- **The entrypoint launched the agent with a bare `python`** — with the env in front on PATH, the agent would have come up *inside the env it exists to stay out of*, and the bridge would have hidden it.
- **A half-built env is worse than none** — an interrupted unpack leaves a python that dies with `No module named 'encodings'`; testing for an executable file put it first on the user's PATH. There is now a readiness marker, written only after the env proves it starts and imports the runtime.
- **A corrupted prefix was unrecoverable** — `micromamba create` refuses an existing directory, so every boot retried and failed forever. The directory is renamed aside (removing ~11k files over the Volume is slow enough to be interrupted again) and rebuilt.
- **The bridge made the env think it already had ipykernel** — pip correctly said "already satisfied", installed nothing, and the `site-packages/ipykernel` test stayed false, so the kernelspec was never written and notebook could not see the env.
- **The env script has to run every boot** — the kernelspec lives in the ephemeral image, so it must be re-registered each time.

Known and benign: for a few seconds after boot the kernelspec may not be registered yet, since that work is deliberately in the background.

## Also fixes a bug that predates this branch

The Python interpreter's crash-recovery path still referred to `client_id`, a name that went away when interpreters were re-keyed per chat. The moment an interpreter crashed, the handler raised `NameError` instead of restarting it — and `p_id not in self.interpreters` is itself one of the crash conditions, so the session stayed broken from then on.

## Safety

Sourcing is guarded on both sides: an older image may not carry the script, and a failure inside it must cost a package manager, never the sandbox (`set -e` is suspended for the whole of an `||` list, including the sourced body). `PANTHEON_ANALYSIS_PYTHON` unset or stale falls through to `/venv`. The env builder takes a lock, since two micromamba processes unpacking into one prefix is how a half-built env gets made. The apt shim is installed in the *last* image layer, after every build-time `apt-get`, so builds still reach the real one.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01BhPiGNfkhLZ89Sqhoz9ebP

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3af1bbe70fdb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.