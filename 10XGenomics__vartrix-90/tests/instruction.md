# Issue

**Title:** Bump sprs from 0.6.5 to 0.7.1

## Description

Bumps [sprs](https://github.com/sparsemat/sprs) from 0.6.5 to 0.7.1.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sparsemat/sprs/blob/master/changelog.rst">sprs's changelog</a>.</em></p>
<blockquote>
<ul>
<li>0.7.1
<ul>
<li>fix issue when building docs on nightly, which broke on docs.sprs</li>
</ul>
</li>
<li>0.7.0
<ul>
<li>make serde optional <strong>breaking change</strong></li>
<li>make mul_acc_mat_vec_cs{r|c} more generic <strong>breaking change</strong></li>
<li>support having different types for indptr &amp; indices in CsMatBase <strong>breaking change</strong></li>
<li>more careful overflow checking</li>
<li>upgrade dependencies</li>
</ul>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>47ac4e5</code></a> Fix build of docs on nightly</li>
<li><a href=""><code>34db987</code></a> Prepare version 0.7.0 (<a href="">#180</a>)</li>
<li><a href=""><code>e27249b</code></a> Merge branch 'pmarks-pmarks/update-deps'</li>
<li><a href=""><code>3c1be50</code></a> fmt</li>
<li><a href=""><code>8acd552</code></a> update some old deps</li>
<li><a href=""><code>4460870</code></a> Merge branch 'tomtung-generic_mul_acc_mat_vec'</li>
<li><a href=""><code>351495c</code></a> Test that new interface also works on slices</li>
<li><a href=""><code>c7cde30</code></a> Make mul_acc_mat_vec_cs{r|c} more generic</li>
<li><a href=""><code>aa0058a</code></a> Fix nightly warning about unnecessary parenthesis (<a href="">#179</a>)</li>
<li><a href=""><code>e689d7d</code></a> Extend supported ndarray version to 0.13 (<a href="">#175</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/sparsemat/sprs/compare/0.6.5...0.7.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sprs&package-manager=cargo&previous-version=0.6.5&new-version=0.7.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
Dependabot will merge this PR once it's up-to-date and CI passes on it, as requested by @bgianfo.

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef04550c5cb0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.