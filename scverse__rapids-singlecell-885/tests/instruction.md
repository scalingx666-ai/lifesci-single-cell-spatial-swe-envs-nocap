# Issue

**Title:** Bump the actions-deps group with 2 updates

## Description

Bumps the actions-deps group with 2 updates: [astral-sh/setup-uv](https://github.com/astral-sh/setup-uv) and [pypa/cibuildwheel](https://github.com/pypa/cibuildwheel).

Updates `astral-sh/setup-uv` from 10.3.2 to 10.3.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/setup-uv/releases">astral-sh/setup-uv's releases</a>.</em></p>
<blockquote>
<h2>v10.3.3 🌈 Use Astral mirror for version manifests with GitHub fallback</h2>
<h2>Changes</h2>
<p>This release contains something that should have been included a very long time ago. Sorry for sleeping on that.</p>
<p>This action now retrieves the release manifest that contains the available versions, their download links and checksums from the Astral mirror, rather than trying GitHub first. This should present much more stable.
(Known checksums are still checked, so the security impact does not change)</p>
<p>Also a big thank you to <a href="https://github.com/soujasK"><code>@​soujasK</code></a> for a set of bugfixes 👏</p>
<h2>🐛 Bug fixes</h2>
<ul>
<li>Use Astral mirror for version manifests with GitHub fallback <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#1119</a>)</li>
<li>fix: allow whitespace in uv requirement specifiers <a href="https://github.com/soujasK"><code>@​soujasK</code></a> (<a href="">#1112</a>)</li>
<li>fix: resolve ~= specifiers with PEP 440 semantics <a href="https://github.com/soujasK"><code>@​soujasK</code></a> (<a href="">#1111</a>)</li>
<li>fix: only report a saved cache when saving succeeded <a href="https://github.com/soujasK"><code>@​soujasK</code></a> (<a href="">#1110</a>)</li>
</ul>
<h2>🧰 Maintenance</h2>
<ul>
<li>chore: update known checksums for 0.13.6 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1117</a>)</li>
</ul>
<h2>📚 Documentation</h2>
<ul>
<li>docs: use JSDoc for compatible release specifier comment <a href="https://github.com/eifinger"><code>@​eifinger</code></a> (<a href="">#1113</a>)</li>
<li>docs: update version references to v10.3.2 @<a href="https://github.com/apps/github-actions">github-actions[bot]</a> (<a href="">#1104</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>68559e9</code></a> Use Astral mirror for version manifests with GitHub fallback (<a href="">#1119</a>)</li>
<li><a href=""><code>0192b69</code></a> chore: update known checksums for 0.13.6 (<a href="">#1117</a>)</li>
<li><a href=""><code>2f29784</code></a> docs: use JSDoc for compatible release specifier comment (<a href="">#1113</a>)</li>
<li><a href=""><code>9c73321</code></a> fix: allow whitespace in uv requirement specifiers (<a href="">#1112</a>)</li>
<li><a href=""><code>80fbe01</code></a> fix: resolve ~= specifiers with PEP 440 semantics (<a href="">#1111</a>)</li>
<li><a href=""><code>36b7b57</code></a> fix: only report a saved cache when saving succeeded (<a href="">#1110</a>)</li>
<li><a href=""><code>56618ca</code></a> docs: update version references to v10.3.2 (<a href="">#1104</a>)</li>
<li>See full diff in <a href="https://github.com/astral-sh/setup-uv/compare/07a047e608db84b3d8c06cd9a7c7dcc9c355c18e...68559e99cc807c1eb7e9238fd43a15bba460eec2">compare view</a></li>
</ul>
</details>
<br />

Updates `pypa/cibuildwheel` from 4.3.4 to 4.3.5
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pypa/cibuildwheel/releases">pypa/cibuildwheel's releases</a>.</em></p>
<blockquote>
<h2>v4.3.5</h2>
<ul>
<li>🐛 Stops passing the target build environment to the host virtualenv call, regression in v4.3.4 (<a href="">#3023</a>)</li>
<li>🛠 Updates dependencies and constraints (pyodide-build 0.39.3, CPython 3.15.2, etc) (<a href="">#3024</a>, <a href="">#3027</a>)</li>
<li>💼 Updates CI actions (<a href="">#3025</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pypa/cibuildwheel/blob/main/docs/changelog.md">pypa/cibuildwheel's changelog</a>.</em></p>
<blockquote>
<hr />
<h2>title: Changelog
ref: changelog</h2>
<h1>Changelog</h1>
<h3>v4.3.5</h3>
<p><em>27 October 2026</em></p>
<ul>
<li>🐛 Stops passing the target build environment to the host virtualenv call, regression in v4.3.4 (<a href="">#3023</a>)</li>
<li>🛠 Updates dependencies and constraints (pyodide-build 0.39.3, CPython 3.15.2, etc) (<a href="">#3024</a>, <a href="">#3027</a>)</li>
<li>💼 Updates CI actions (<a href="">#3025</a>)</li>
</ul>
<h3>v4.3.4</h3>
<p><em>22 October 2026</em></p>
<ul>
<li>🔐 Warns when a uv build frontend is selected and the host uv is older than 0.13.4, which still trusts the compromised eMudhra CA roots (<a href="">#3021</a>)</li>
<li>🔐 Uses cibuildwheel's CA bundle for pip on Python 3.9, where pip uses its bundled certifi, which still trusts the compromised eMudhra roots (<a href="">#3017</a>)</li>
<li>🔐 Uses cibuildwheel's CA bundle for pip on GraalPy, where truststore is not supported (<a href="">#3019</a>)</li>
<li>🔐 Uses cibuildwheel's CA bundle in Android, iOS, and Pyodide cross venvs, where pip uses the host's OpenSSL CA file (<a href="">#3020</a>)</li>
<li>🐛 Seeds build's isolated environment with the pinned pip on macOS and Windows, fixing GraalPy 25.0 builds (<a href="">#3018</a>)</li>
<li>💼 Stops Azure cache growth from <code>restoreKeys</code> (<a href="">#3022</a>)</li>
</ul>
<h3>v4.3.3</h3>
<p><em>21 October 2026</em></p>
<ul>
<li>🔐 Updates manylinux images and pip to fix vulnerability to <a href="https://emudhra.we-have-a-problem.com/">eMudhra</a>.</li>
</ul>
<h3>v4.3.2</h3>
<p><em>20 October 2026</em></p>
<ul>
<li>🔐 Updates our dependency pins to certifi==2026.10.19, following the <a href="https://emudhra.we-have-a-problem.com/">eMudhra Intermediate CA Compromise</a>. Linux builds may still be vulnerable through manylinux images - a patch release will soon follow if so.</li>
</ul>
<h3>v4.3.1</h3>
<p><em>10 October 2026</em></p>
<ul>
<li>🛠 Updates CPython 3.15 to the final 3.15.0 release (<a href="">#3009</a>)</li>
</ul>
<h3>v4.3.0</h3>
<p><em>5 October 2026</em></p>
<ul>
<li>✨ Extends <a href="https://cibuildwheel.pypa.io/en/stable/configuration/#inherit">option inheritance</a> to every configuration layer, so global and platform-specific settings can append or prepend to existing values, including cibuildwheel's defaults. Environment variables can also extend earlier settings using <code>CIBW_INHERIT</code>. (<a href="">#2928</a>)</li>
<li>✨ Adds PyPy 3.12 support and updates PyPy 3.11 to v8.0.0, available with the <code>pypy</code> <a href="https://cibuildwheel.pypa.io/en/stable/options/#enable"><code>enable</code></a> flag (<a href="">#2998</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>f9b966c</code></a> Bump version: v4.3.5</li>
<li><a href=""><code>7e3caea</code></a> Update constraints (<a href="">#3027</a>)</li>
<li><a href=""><code>dff3913</code></a> chore(deps): bump the actions group with 2 updates (<a href="">#3025</a>)</li>
<li><a href=""><code>2956993</code></a> fix: do not pass target environment to the host virtualenv call (<a href="">#3023</a>)</li>
<li><a href=""><code>5d621c9</code></a> [Bot] Update dependencies (<a href="">#3024</a>)</li>
<li>See full diff in <a href="https://github.com/pypa/cibuildwheel/compare/b9e566a2b284570af229f6c2a33673410d0389a3...f9b966cfadf4109556cadc5bb39ddb72d0ce664e">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b8a075fd631`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.