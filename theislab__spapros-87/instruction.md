# Issue

**Title:** [DEPENDABOT]: Bump numpy from 1.20.2 to 1.20.3

## Description

Bumps [numpy](https://github.com/numpy/numpy) from 1.20.2 to 1.20.3.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/numpy/numpy/releases">numpy's releases</a>.</em></p>
<blockquote>
<h2>v1.20.3</h2>
<h1>NumPy 1.20.3 Release Notes</h1>
<p>NumPy 1.20.3 is a bugfix release containing several fixes merged to the
main branch after the NumPy 1.20.2 release.</p>
<h2>Contributors</h2>
<p>A total of 7 people contributed to this release. People with a &quot;+&quot; by
their names contributed a patch for the first time.</p>
<ul>
<li>Anne Archibald</li>
<li>Bas van Beek</li>
<li>Charles Harris</li>
<li>Dong Keun Oh +</li>
<li>Kamil Choudhury +</li>
<li>Sayed Adel</li>
<li>Sebastian Berg</li>
</ul>
<h2>Pull requests merged</h2>
<p>A total of 15 pull requests were merged for this release.</p>
<ul>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18763">#18763</a>: BUG: Correct <code>datetime64</code> missing type overload for <code>datetime.date</code>...</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18764">#18764</a>: MAINT: Remove <code>__all__</code> in favor of explicit re-exports</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18768">#18768</a>: BLD: Strip extra newline when dumping gfortran version on MacOS</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18769">#18769</a>: BUG: fix segfault in object/longdouble operations</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18794">#18794</a>: MAINT: Use towncrier build explicitly</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18887">#18887</a>: MAINT: Relax certain integer-type constraints</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18915">#18915</a>: MAINT: Remove unsafe unions and ABCs from return-annotations</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18921">#18921</a>: MAINT: Allow more recursion depth for scalar tests.</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18922">#18922</a>: BUG: Initialize the full nditer buffer in case of error</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18923">#18923</a>: BLD: remove unnecessary flag <code>-faltivec</code> on macOS</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18924">#18924</a>: MAINT, CI: treats _SIMD module build warnings as errors through...</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18925">#18925</a>: BUG: for MINGW, threads.h existence test requires GLIBC &gt; 2.12</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18941">#18941</a>: BUG: Make changelog recognize gh- as a PR number prefix.</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18948">#18948</a>: REL, DOC: Prepare for the NumPy 1.20.3 release.</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18953">#18953</a>: BUG: Fix failing mypy test in 1.20.x.</li>
</ul>
<h2>Checksums</h2>
<h3>MD5</h3>
<pre><code>702d0185042f1ff9a5d7e72a29f4e1c0  numpy-1.20.3-cp37-cp37m-macosx_10_9_x86_64.whl
3d0284b39b20c243b74f6690ad5ae27f  numpy-1.20.3-cp37-cp37m-manylinux_2_12_i686.manylinux2010_i686.whl
d1b42dd67dc228088cf822eaab86d424  numpy-1.20.3-cp37-cp37m-manylinux_2_12_x86_64.manylinux2010_x86_64.whl
</code></pre>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>27b98cb</code></a> REL: NumPy 1.20.3 release.</li>
<li><a href=""><code>a438741</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/18953">#18953</a> from charris/fix-mypy-test</li>
<li><a href=""><code>8639821</code></a> BUG: Fix failing mypy test in 1.20.x.</li>
<li><a href=""><code>0eedcd1</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/18948">#18948</a> from charris/prepare-1.20.3-release</li>
<li><a href=""><code>1863519</code></a> REL, DOC: Prepare for the NumPy 1.20.3 release.</li>
<li><a href=""><code>b5cfe76</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/18941">#18941</a> from charris/fix-changelog-script</li>
<li><a href=""><code>59414b6</code></a> DOC: Update 1.17.0-changelog.rst.</li>
<li><a href=""><code>ce397de</code></a> DOC: Update 1.18.0-changelog.rst.</li>
<li><a href=""><code>608c893</code></a> DOC: Update 1.19.0-changelog.rst.</li>
<li><a href=""><code>51f5b83</code></a> DOC: Update 1.20.0-changelog.rst.</li>
<li>Additional commits viewable in <a href="https://github.com/numpy/numpy/compare/v1.20.2...v1.20.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=numpy&package-manager=pip&previous-version=1.20.2&new-version=1.20.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `819c1bd59454`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.