# Issue

**Title:** ci: bump astral-sh/setup-uv from 8.3.2 to 9.0.0

## Description

Bumps [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv) from 8.3.2 to 9.0.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/setup-uv/releases">astral-sh/setup-uv's releases</a>.</em></p>
<blockquote>
<h2>v9.0.0 🌈 Change <code>prune-cache</code> default to <code>false</code></h2>
<h2>Changes</h2>
<p>This release disables the default cache cache pruning to ease the load on the PyPi infrastructure.
Since users might experience more GitHub Actions cache usage which might result in higher costs this is marked as a breaking change. To read more on why we did this (now) you can read the detailed analysis and reasoning in <a href="">#967</a></p>
<p>Besides this big breaking change we also have a small bugfix while building caches for linux distributions that behave a big different than the &quot;big ones&quot; and a speed up in version resolution by only reading the version manifest until a matching version is found saving runtime and network bandwith.</p>
<h2>🚨 Breaking changes</h2>
<ul>
<li>Change <code>prune-cache</code> default to <code>false</code> <a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a> (<a href="">#967</a>)</li>
</ul>
<h2>🐛 Bug fixes</h2>
<ul>
<li>fix: fall back to distribution ID when os-release has no version field <a href="https://github.com/cxzhong"><code>@​cxzhong</code></a> (<a href="">#961</a>)</li>
</ul>
<h2>🚀 Enhancements</h2>
<ul>
<li>Speed up version client by partial response reads <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#807</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.11.30 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#968</a>)</li>
<li>chore: update known checksums for 0.11.29 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#960</a>)</li>
</ul>
<h2>📚 Documentation</h2>
<ul>
<li>docs: update version references to v8.3.2 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#949</a>)</li>
</ul>
<h2>⬆️ Dependency updates</h2>
<ul>
<li>chore(deps): roll up Dependabot updates <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#970</a>)</li>
<li>chore(deps): roll up Dependabot updates <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#962</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>c771a70</code></a> chore(deps): roll up Dependabot updates (<a href="">#970</a>)</li>
<li><a href=""><code>2f537ca</code></a> chore: update known checksums for 0.11.30 (<a href="">#968</a>)</li>
<li><a href=""><code>2269552</code></a> Speed up version client by partial response reads (<a href="">#807</a>)</li>
<li><a href=""><code>47a7f4f</code></a> Change <code>prune-cache</code> default to <code>false</code> (<a href="">#967</a>)</li>
<li><a href=""><code>71966ef</code></a> chore(deps): roll up Dependabot updates (<a href="">#962</a>)</li>
<li><a href=""><code>f12b1f0</code></a> fix: fall back to distribution ID when os-release has no version field (<a href="">#961</a>)</li>
<li><a href=""><code>ecd24dd</code></a> chore: update known checksums for 0.11.29 (<a href="">#960</a>)</li>
<li><a href=""><code>6a19136</code></a> docs: update version references to v8.3.2 (<a href="">#949</a>)</li>
<li>See full diff in <a href="https://github.com/astral-sh/setup-uv/compare/v8.3.2...v9.0.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=astral-sh/setup-uv&package-manager=github_actions&previous-version=8.3.2&new-version=9.0.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b195cdbdeaa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.