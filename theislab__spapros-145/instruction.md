# Issue

**Title:** [DEPENDABOT]: Bump numpy from 1.21.0 to 1.21.1

## Description

Bumps [numpy](https://github.com/numpy/numpy) from 1.21.0 to 1.21.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/numpy/numpy/releases">numpy's releases</a>.</em></p>
<blockquote>
<h2>v1.21.1</h2>
<h1>NumPy 1.21.1 Release Notes</h1>
<p>The NumPy 1.21.1 is maintenance release that fixes bugs discovered after
the 1.21.0 release and updates OpenBLAS to v0.3.17 to deal with problems
on arm64.</p>
<p>The Python versions supported for this release are 3.7-3.9. The 1.21.x
series is compatible with development Python 3.10. Python 3.10 will be
officially supported after it is released.</p>
<p>:warning: There are unresolved problems compiling NumPy 1.20.0 with gcc-11.1.</p>
<ul>
<li>Optimization level -O3 results in many incorrect
warnings when running the tests.</li>
<li>On some hardware NumPY will hang in an infinite loop.</li>
</ul>
<h2>Contributors</h2>
<p>A total of 11 people contributed to this release. People with a &quot;+&quot; by
their names contributed a patch for the first time.</p>
<ul>
<li>Bas van Beek</li>
<li>Charles Harris</li>
<li>Ganesh Kathiresan</li>
<li>Gregory R. Lee</li>
<li>Hugo Defois +</li>
<li>Kevin Sheppard</li>
<li>Matti Picus</li>
<li>Ralf Gommers</li>
<li>Sayed Adel</li>
<li>Sebastian Berg</li>
<li>Thomas J. Fan</li>
</ul>
<h2>Pull requests merged</h2>
<p>A total of 26 pull requests were merged for this release.</p>
<ul>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/19311">#19311</a>: REV,BUG: Replace <code>NotImplemented</code> with <code>typing.Any</code></li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/19324">#19324</a>: MAINT: Fixed the return-dtype of <code>ndarray.real</code> and <code>imag</code></li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/19330">#19330</a>: MAINT: Replace <code>&quot;dtype[Any]&quot;</code> with <code>dtype</code> in the definiton of...</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/19342">#19342</a>: DOC: Fix some docstrings that crash pdf generation.</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/19343">#19343</a>: MAINT: bump scipy-mathjax</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/19347">#19347</a>: BUG: Fix arr.flat.index for large arrays and big-endian machines</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/19348">#19348</a>: ENH: add <code>numpy.f2py.get_include</code> function</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/19349">#19349</a>: BUG: Fix reference count leak in ufunc dtype handling</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>df6d260</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/19510">#19510</a> from charris/prepare-1.21.1-release</li>
<li><a href=""><code>7031a82</code></a> REL: Prepare for NumPy 1.21.1 release.</li>
<li><a href=""><code>7b27ba9</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/19503">#19503</a> from charris/backport-19468</li>
<li><a href=""><code>cadd4ba</code></a> DOC: Document that <code>size_t</code> is not guaranteed to map to <code>np.intp</code> under rare ...</li>
<li><a href=""><code>374440e</code></a> TST: Update the <code>dtype</code> typing tests</li>
<li><a href=""><code>648110f</code></a> MAINT: Add a missing <code>object</code> overload to <code>np.dtype</code></li>
<li><a href=""><code>8cd3546</code></a> MAINT: Add <code>ctypes</code> overloads to <code>np.dtype</code></li>
<li><a href=""><code>8f07655</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/19502">#19502</a> from charris/backport-19446</li>
<li><a href=""><code>4c80d18</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/19501">#19501</a> from charris/backport-19456</li>
<li><a href=""><code>74f82c9</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/19500">#19500</a> from charris/backport-19396</li>
<li>Additional commits viewable in <a href="https://github.com/numpy/numpy/compare/v1.21.0...v1.21.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=numpy&package-manager=pip&previous-version=1.21.0&new-version=1.21.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4e812f170713`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.