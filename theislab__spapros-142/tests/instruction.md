# Issue

**Title:** [DEPENDABOT]: Bump sphinx from 4.0.3 to 4.1.1

## Description

Bumps [sphinx](https://github.com/sphinx-doc/sphinx) from 4.0.3 to 4.1.1.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/blob/4.x/CHANGES">sphinx's changelog</a>.</em></p>
<blockquote>
<h1>Release 4.1.1 (released Jul 15, 2021)</h1>
<h2>Dependencies</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9434">#9434</a>: sphinxcontrib-htmlhelp-2.0.0 or above</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9434">#9434</a>: sphinxcontrib-serializinghtml-1.1.5 or above</li>
</ul>
<h2>Bugs fixed</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9438">#9438</a>: html: HTML logo or Favicon specified as file not being found on output</li>
</ul>
<h1>Release 4.1.0 (released Jul 12, 2021)</h1>
<h2>Dependencies</h2>
<ul>
<li>Support jinja2-3.0</li>
</ul>
<h2>Deprecated</h2>
<ul>
<li>The <code>app</code> argument of <code>sphinx.environment.BuildEnvironment</code> becomes
required</li>
<li><code>sphinx.application.Sphinx.html_theme</code></li>
<li><code>sphinx.ext.autosummary._app</code></li>
<li><code>sphinx.util.docstrings.extract_metadata()</code></li>
</ul>
<h2>Features added</h2>
<ul>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8107">#8107</a>: autodoc: Add <code>class-doc-from</code> option to :rst:dir:<code>autoclass</code>
directive to control the content of the specific class like
:confval:<code>autoclass_content</code></li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8588">#8588</a>: autodoc: :confval:<code>autodoc_type_aliases</code> now supports dotted name. It
allows you to define an alias for a class with module name like
<code>foo.bar.BazClass</code></li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9175">#9175</a>: autodoc: Special member is not documented in the module</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9195">#9195</a>: autodoc: The arguments of <code>typing.Literal</code> are wrongly rendered</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9185">#9185</a>: autodoc: :confval:<code>autodoc_typehints</code> allows <code>'both'</code> setting to
allow typehints to be included both in the signature and description</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/4257">#4257</a>: autodoc: Add :confval:<code>autodoc_class_signature</code> to separate the class
entry and the definition of <code>__init__()</code> method</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/8061">#8061</a>, <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9218">#9218</a>: autodoc: Support variable comment for alias classes</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/3014">#3014</a>: autodoc: Add :event:<code>autodoc-process-bases</code> to modify the base classes
of the class definitions</li>
<li><a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9272">#9272</a>: autodoc: Render enum values for the default argument value better</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>564439e</code></a> Bump to 4.1.1 final</li>
<li><a href=""><code>ffa0831</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9448">#9448</a> from tk0miya/9434_update_deps</li>
<li><a href=""><code>5daedcf</code></a> Fix <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9434">#9434</a>: Update dependencies for bundled builders</li>
<li><a href=""><code>f3a3bd2</code></a> Update CHANGES for PR <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9440">#9440</a></li>
<li><a href=""><code>63001f3</code></a> Merge pull request <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9440">#9440</a> from tronical/logo-regression-fix</li>
<li><a href=""><code>3a50abc</code></a> Fix handling of local paths in html_logo/html_favicon directorives in conf.py</li>
<li><a href=""><code>3c3a734</code></a> Bump version</li>
<li><a href=""><code>bdcd161</code></a> Bump to 4.1.0 final</li>
<li><a href=""><code>4a2f5df</code></a> Merge branch '9299' into 4.x</li>
<li><a href=""><code>e6d3adf</code></a> intersphinx: Add testcase for case insensitive term match (refs: <a href="https://github-redirect.dependabot.com/sphinx-doc/sphinx/issues/9299">#9299</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/sphinx-doc/sphinx/compare/v4.0.3...v4.1.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sphinx&package-manager=pip&previous-version=4.0.3&new-version=4.1.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0aabb85e016f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.