# Issue

**Title:** [DEPENDABOT]: Bump leidenalg from 0.8.3 to 0.8.4

## Description

Bumps [leidenalg](https://github.com/vtraag/leidenalg) from 0.8.3 to 0.8.4.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/vtraag/leidenalg/blob/master/CHANGELOG">leidenalg's changelog</a>.</em></p>
<blockquote>
<p>0.8.4</p>
<ul>
<li>Update C core to 0.9.1</li>
<li>Fixed caching problem (issue <a href="https://github-redirect.dependabot.com/vtraag/leidenalg/issues/62">#62</a>)</li>
<li>Fixed missing node_sizes for modularity (issue <a href="https://github-redirect.dependabot.com/vtraag/leidenalg/issues/60">#60</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0658758</code></a> chore: update CHANGELOG.</li>
<li><a href=""><code>31eb716</code></a> Skip test PyPI, will not accept local versions anyway.</li>
<li><a href=""><code>606aefa</code></a> Only trigger push on master branch.</li>
<li><a href=""><code>65ec36a</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/vtraag/leidenalg/issues/63">#63</a> from vtraag/update/igraph-0.9</li>
<li><a href=""><code>41c7d46</code></a> Upload to PyPI on tag.</li>
<li><a href=""><code>1517995</code></a> Corrected integer comparisons.</li>
<li><a href=""><code>8dd31c0</code></a> Correct catch warning.</li>
<li><a href=""><code>e264188</code></a> Corrected trailing #endif warning.</li>
<li><a href=""><code>b2c62a7</code></a> Corrected char* warning.</li>
<li><a href=""><code>bf4e99c</code></a> Corrected warnings on char*.</li>
<li>Additional commits viewable in <a href="https://github.com/vtraag/leidenalg/compare/0.8.3...0.8.4">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=leidenalg&package-manager=pip&previous-version=0.8.3&new-version=0.8.4)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `377c64db0e24`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.