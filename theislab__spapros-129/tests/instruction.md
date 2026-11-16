# Issue

**Title:** [DEPENDABOT]: Bump leidenalg from 0.8.4 to 0.8.7

## Description

[//]: # (dependabot-start)
⚠️  **Dependabot is rebasing this PR** ⚠️

Rebasing might not happen immediately, so don't worry if this takes some time.

Note: if you make any changes to this PR yourself, they will take precedence over the rebase.

---

[//]: # (dependabot-end)

Bumps [leidenalg](https://github.com/vtraag/leidenalg) from 0.8.4 to 0.8.7.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/vtraag/leidenalg/blob/master/CHANGELOG">leidenalg's changelog</a>.</em></p>
<blockquote>
<p>0.8.7</p>
<ul>
<li>Improved numerical stability</li>
</ul>
<p>0.8.6</p>
<ul>
<li>Removed accidentally left DEBUG statement</li>
</ul>
<p>0.8.5</p>
<ul>
<li>Corrected iterating over nodes (PR <a href="https://github-redirect.dependabot.com/vtraag/leidenalg/issues/70">#70</a>).</li>
<li>Fixed segfault with move_nodes_constrained (issue <a href="https://github-redirect.dependabot.com/vtraag/leidenalg/issues/68">#68</a>)</li>
<li>Fixed problem with initial_membership (issue <a href="https://github-redirect.dependabot.com/vtraag/leidenalg/issues/66">#66</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8491dbd</code></a> Increased stability for current community.</li>
<li><a href=""><code>dc91274</code></a> Update changelog.</li>
<li><a href=""><code>65cf652</code></a> Correct DBL_EPSILON.</li>
<li><a href=""><code>f90113c</code></a> Optimiser: improve numerical stability.</li>
<li><a href=""><code>4746ee2</code></a> Revert &quot;Significance: Remove DEBUG def.&quot;</li>
<li><a href=""><code>350879b</code></a> chore: Updated CHANGELOG.</li>
<li><a href=""><code>ad6c79f</code></a> Significance: Remove DEBUG def.</li>
<li><a href=""><code>ec5366c</code></a> Prepare for release.</li>
<li><a href=""><code>6a77a72</code></a> chore: Update CHANGELOG. [skip ci]</li>
<li><a href=""><code>0b21b01</code></a> README: Change to list.</li>
<li>Additional commits viewable in <a href="https://github.com/vtraag/leidenalg/compare/0.8.4...0.8.7">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=leidenalg&package-manager=pip&previous-version=0.8.4&new-version=0.8.7)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1909fc260586`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.