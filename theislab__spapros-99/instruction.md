# Issue

**Title:** [DEPENDABOT]: Bump sphinx from 3.5.4 to 4.0.2

## Description

Bumps [sphinx](https://github.com/sphinx-doc/sphinx) from 3.5.4 to 4.0.2.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/blob/4.x/CHANGES">sphinx's changelog</a>.</em></p>
<blockquote>
<h1>Release 4.0.2 (released May 20, 2021)</h1>
<h2>Dependencies</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9216">#9216</a>: Support jinja2-3.0</li>
</ul>
<h2>Incompatible changes</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9222">#9222</a>: Update Underscore.js to 1.13.1</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9217">#9217</a>: manpage: Stop creating a section directory on build manpage by default
(see :confval:<code>man_make_section_directory</code>)</li>
</ul>
<h2>Bugs fixed</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9210">#9210</a>: viewcode: crashed if non importable modules found on parallel build</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9240">#9240</a>: Unknown node error for pending_xref_condition is raised if an extension
that does not support the node installs a missing-reference handler</li>
</ul>
<h1>Release 4.0.1 (released May 11, 2021)</h1>
<h2>Bugs fixed</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9189">#9189</a>: autodoc: crashed when ValueError is raised on generating signature
from a property of the class</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9188">#9188</a>: autosummary: warning is emitted if list value is set to
autosummary_generate</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8380">#8380</a>: html search: tags for search result are broken</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9198">#9198</a>: i18n: Babel emits errors when running compile_catalog</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9205">#9205</a>: py domain: The :canonical: option causes &quot;more than one target for
cross-reference&quot; warning</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9201">#9201</a>: websupport: UndefinedError is raised: 'css_tag' is undefined</li>
</ul>
<h1>Release 4.0.0 (released May 09, 2021)</h1>
<h2>Dependencies</h2>
<p>4.0.0b1</p>
<ul>
<li>Drop python 3.5 support</li>
<li>Drop docutils 0.12 and 0.13 support</li>
<li>LaTeX: add <code>tex-gyre</code> font dependency</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a55816d</code></a> Bump to 4.0.2 final</li>
<li><a href=""><code>c44140b</code></a> Update CHANGES for PR <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9240">#9240</a></li>
<li><a href=""><code>c015f97</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9251">#9251</a> from tk0miya/9216_support_jinja2-3</li>
<li><a href=""><code>4b8fb68</code></a> Fix type annotations (for jinja2)</li>
<li><a href=""><code>e5c905c</code></a> Support jinja2-3.0</li>
<li><a href=""><code>ca36c9a</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9246">#9246</a> from tk0miya/9240_unknown_node_pending_xref_condition</li>
<li><a href=""><code>bb2c662</code></a> Close <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9216">#9216</a>: Support jinja2-3.0</li>
<li><a href=""><code>2d3d668</code></a> Fix <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9240">#9240</a>: Unknown node error for pending_xref_condition is raised</li>
<li><a href=""><code>630e5bd</code></a> manpage: Stop creating a section directory on build manpage by default</li>
<li><a href=""><code>1ab7e28</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9223">#9223</a> from tk0miya/underscore.js-1.13.1</li>
<li>Additional commits viewable in <a href="https://github.com/sphinx-doc/sphinx/compare/v3.5.4...v4.0.2">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sphinx&package-manager=pip&previous-version=3.5.4&new-version=4.0.2)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1eb97cdf4fc8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.