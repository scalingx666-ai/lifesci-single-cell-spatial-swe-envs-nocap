# Issue

**Title:** chore(deps): bump the workflow-actions group with 2 updates

## Description

Bumps the workflow-actions group with 2 updates: [actions/checkout](https://github.com/actions/checkout) and [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv).

Updates `actions/checkout` from 7.0.0 to 7.0.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/releases">actions/checkout's releases</a>.</em></p>
<blockquote>
<h2>v7.0.1</h2>
<h2>What's Changed</h2>
<ul>
<li>skip running unsafe pr check if input is default by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2518</a></li>
<li>trim only ascii whitespace for branch by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2521</a></li>
<li>escape values passed to --unset by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2530</a></li>
<li>Various dependency updates</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/actions/checkout/compare/v7...v7.0.1">https://github.com/actions/checkout/compare/v7...v7.0.1</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/actions/checkout/blob/main/CHANGELOG.md">actions/checkout's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<h2>v7.0.1</h2>
<ul>
<li>Skip running unsafe pr check if input is default by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2518</a></li>
<li>Trim only ascii whitespace for branch by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2521</a></li>
<li>Escape values passed to --unset by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2530</a></li>
<li>Various dependency updates</li>
</ul>
<h2>v7.0.0</h2>
<ul>
<li>Block checking out fork PR for pull_request_target and workflow_run by <a href="https://github.com/aiqiaoy"><code>@​aiqiaoy</code></a> in <a href="">actions/checkout#2454</a></li>
<li>Various dependency updates</li>
</ul>
<h2>v6.0.3</h2>
<ul>
<li>Fix checkout init for SHA-256 repositories by <a href="https://github.com/yaananth"><code>@​yaananth</code></a> in <a href="">actions/checkout#2439</a></li>
<li>fix: expand merge commit SHA regex and add SHA-256 test cases by <a href="https://github.com/yaananth"><code>@​yaananth</code></a> in <a href="">actions/checkout#2414</a></li>
</ul>
<h2>v6.0.2</h2>
<ul>
<li>Fix tag handling: preserve annotations and explicit fetch-tags by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2356</a></li>
</ul>
<h2>v6.0.1</h2>
<ul>
<li>Add worktree support for persist-credentials includeIf by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2327</a></li>
</ul>
<h2>v6.0.0</h2>
<ul>
<li>Persist creds to a separate file by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2286</a></li>
<li>Update README to include Node.js 24 support details and requirements by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2248</a></li>
</ul>
<h2>v5.0.1</h2>
<ul>
<li>Port v6 cleanup to v5 by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2301</a></li>
</ul>
<h2>v5.0.0</h2>
<ul>
<li>Update actions checkout to use node 24 by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2226</a></li>
</ul>
<h2>v4.3.1</h2>
<ul>
<li>Port v6 cleanup to v4 by <a href="https://github.com/ericsciple"><code>@​ericsciple</code></a> in <a href="">actions/checkout#2305</a></li>
</ul>
<h2>v4.3.0</h2>
<ul>
<li>docs: update README.md by <a href="https://github.com/motss"><code>@​motss</code></a> in <a href="">actions/checkout#1971</a></li>
<li>Add internal repos for checking out multiple repositories by <a href="https://github.com/mouismail"><code>@​mouismail</code></a> in <a href="">actions/checkout#1977</a></li>
<li>Documentation update - add recommended permissions to Readme by <a href="https://github.com/benwells"><code>@​benwells</code></a> in <a href="">actions/checkout#2043</a></li>
<li>Adjust positioning of user email note and permissions heading by <a href="https://github.com/joshmgross"><code>@​joshmgross</code></a> in <a href="">actions/checkout#2044</a></li>
<li>Update README.md by <a href="https://github.com/nebuk89"><code>@​nebuk89</code></a> in <a href="">actions/checkout#2194</a></li>
<li>Update CODEOWNERS for actions by <a href="https://github.com/TingluoHuang"><code>@​TingluoHuang</code></a> in <a href="">actions/checkout#2224</a></li>
<li>Update package dependencies by <a href="https://github.com/salmanmkc"><code>@​salmanmkc</code></a> in <a href="">actions/checkout#2236</a></li>
</ul>
<h2>v4.2.2</h2>
<ul>
<li><code>url-helper.ts</code> now leverages well-known environment variables by <a href="https://github.com/jww3"><code>@​jww3</code></a> in <a href="">actions/checkout#1941</a></li>
<li>Expand unit test coverage for <code>isGhes</code> by <a href="https://github.com/jww3"><code>@​jww3</code></a> in <a href="">actions/checkout#1946</a></li>
</ul>
<h2>v4.2.1</h2>
<ul>
<li>Check out other refs/* by commit if provided, fall back to ref by <a href="https://github.com/orhantoy"><code>@​orhantoy</code></a> in <a href="">actions/checkout#1924</a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/actions/checkout/compare/v7...3d3c42e5aac5ba805825da76410c181273ba90b1">compare view</a></li>
</ul>
</details>
<br />

Updates `astral-sh/setup-uv` from 8.3.2 to 9.0.0
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
<li>See full diff in <a href="https://github.com/astral-sh/setup-uv/compare/v8.3.2...c771a70e6277c0a99b617c7a806ffedaca235ff9">compare view</a></li>
</ul>
</details>
<br />

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
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0dd8f6448572`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.