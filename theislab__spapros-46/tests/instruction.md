# Issue

**Title:** [DEPENDABOT]: Bump numpy from 1.20.1 to 1.20.2

## Description

Bumps [numpy](https://github.com/numpy/numpy) from 1.20.1 to 1.20.2.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/numpy/numpy/releases">numpy's releases</a>.</em></p>
<blockquote>
<h2>v1.20.2</h2>
<h1>NumPy 1.20.2 Release Notes</h1>
<p>NumPy 1,20.2 is a bugfix release containing several fixes merged to the
main branch after the NumPy 1.20.1 release.</p>
<h2>Contributors</h2>
<p>A total of 7 people contributed to this release. People with a &quot;+&quot; by
their names contributed a patch for the first time.</p>
<ul>
<li>Allan Haldane</li>
<li>Bas van Beek</li>
<li>Charles Harris</li>
<li>Christoph Gohlke</li>
<li>Mateusz Sokół +</li>
<li>Michael Lamparski</li>
<li>Sebastian Berg</li>
</ul>
<h2>Pull requests merged</h2>
<p>A total of 20 pull requests were merged for this release.</p>
<ul>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18382">#18382</a>: MAINT: Update f2py from master.</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18459">#18459</a>: BUG: <code>diagflat</code> could overflow on windows or 32-bit platforms</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18460">#18460</a>: BUG: Fix refcount leak in f2py <code>complex_double_from_pyobj</code>.</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18461">#18461</a>: BUG: Fix tiny memory leaks when <code>like=</code> overrides are used</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18462">#18462</a>: BUG: Remove temporary change of descr/flags in VOID functions</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18469">#18469</a>: BUG: Segfault in nditer buffer dealloc for Object arrays</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18485">#18485</a>: BUG: Remove suspicious type casting</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18486">#18486</a>: BUG: remove nonsensical comparison of pointer &lt; 0</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18487">#18487</a>: BUG: verify pointer against NULL before using it</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18488">#18488</a>: BUG: check if PyArray_malloc succeeded</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18546">#18546</a>: BUG: incorrect error fallthrough in nditer</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18559">#18559</a>: CI: Backport CI fixes from main.</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18599">#18599</a>: MAINT: Add annotations for <code>__getitem__</code>, <code>__mul__</code> and...</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18611">#18611</a>: BUG: NameError in numpy.distutils.fcompiler.compaq</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18612">#18612</a>: BUG: Fixed <code>where</code> keyword for <code>np.mean</code> &amp; <code>np.var</code> methods</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18617">#18617</a>: CI: Update apt package list before Python install</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18636">#18636</a>: MAINT: Ensure that re-exported sub-modules are properly annotated</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18638">#18638</a>: BUG: Fix ma coercion list-of-ma-arrays if they do not cast to...</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18661">#18661</a>: BUG: Fix small valgrind-found issues</li>
<li><a href="https://github-redirect.dependabot.com/numpy/numpy/pull/18671">#18671</a>: BUG: Fix small issues found with pytest-leaks</li>
</ul>
<h2>Checksums</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b19ad5b</code></a> REL: NumPy 1.20.2 release.</li>
<li><a href=""><code>7025ddc</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/18681">#18681</a> from charris/prepare-1.20.2-release</li>
<li><a href=""><code>5dc057c</code></a> REL: Prepare for the NumPy 1.20.2 release.</li>
<li><a href=""><code>e687165</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/18671">#18671</a> from seberg/backport-small-pytest-leaks-fixes</li>
<li><a href=""><code>afc861e</code></a> BUG: Fix small issues found with pytest-leaks</li>
<li><a href=""><code>c4fd82f</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/18661">#18661</a> from charris/backport-18651</li>
<li><a href=""><code>b9edc25</code></a> BUG: Fix small valgrind-found issues (<a href="https://github-redirect.dependabot.com/numpy/numpy/issues/18651">#18651</a>)</li>
<li><a href=""><code>59c99e4</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/numpy/numpy/issues/18638">#18638</a> from charris/backport-18605</li>
<li><a href=""><code>fb44ee2</code></a> Update numpy/ma/tests/test_core.py</li>
<li><a href=""><code>9719ac5</code></a> Apply suggestions from code review</li>
<li>Additional commits viewable in <a href="https://github.com/numpy/numpy/compare/v1.20.1...v1.20.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=numpy&package-manager=pip&previous-version=1.20.1&new-version=1.20.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f9e80ca70f5d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.