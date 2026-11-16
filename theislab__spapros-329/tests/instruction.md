# Issue

**Title:** [DEPENDABOT]: Bump sphinx from 5.3.0 to 7.2.6

## Description

Bumps [sphinx](https://github.com/sphinx-doc/sphinx) from 5.3.0 to 7.2.6.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/releases">sphinx's releases</a>.</em></p>
<blockquote>
<h2>Sphinx 7.2.6</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>Sphinx 7.2.5</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>Sphinx 7.2.4</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>Sphinx 7.2.3</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>Sphinx 7.2.2</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>Sphinx 7.2.1</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>Sphinx 7.2.0</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>Sphinx 7.1.2</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>Sphinx 7.1.1</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>Sphinx 7.1.0</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v7.0.1</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v7.0.0</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v7.0.0rc1</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v6.2.1</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v6.2.0</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v6.1.3</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<h2>v6.1.2</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes.html">https://www.sphinx-doc.org/en/master/changes.html</a></p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/blob/master/CHANGES.rst">sphinx's changelog</a>.</em></p>
<blockquote>
<h1>Release 7.2.6 (released Sep 13, 2023)</h1>
<h2>Bugs fixed</h2>
<ul>
<li><a href="">#11679</a>: Add the :envvar:<code>!SPHINX_AUTODOC_RELOAD_MODULES</code> environment variable,
which if set reloads modules when using autodoc with <code>TYPE_CHECKING = True</code>.
Patch by Matt Wozniski and Adam Turner.</li>
<li><a href="">#11679</a>: Use :py:func:<code>importlib.reload</code> to reload modules in autodoc.
Patch by Matt Wozniski and Adam Turner.</li>
</ul>
<h1>Release 7.2.5 (released Aug 30, 2023)</h1>
<h2>Bugs fixed</h2>
<ul>
<li><a href="">#11645</a>: Fix a regression preventing autodoc from importing modules within
packages that make use of <code>if typing.TYPE_CHECKING:</code> to guard circular
imports needed by type checkers.
Patch by Matt Wozniski.</li>
<li><a href="">#11634</a>: Fixed inheritance diagram relative link resolution
for sibling files in a subdirectory.
Patch by Albert Shih.</li>
<li><a href="">#11659</a>: Allow <code>?config=...</code> in :confval:<code>mathjax_path</code>.</li>
<li><a href="">#11654</a>: autodoc: Fail with a more descriptive error message
when an object claims to be an instance of <code>type</code>,
but is not a class.
Patch by James Braza.</li>
<li>11620: Cease emitting :event:<code>source-read</code> events for files read via
the :dudir:<code>include</code> directive.</li>
<li>11620: Add a new :event:<code>include-read</code> for observing and transforming
the content of included files via the :dudir:<code>include</code> directive.</li>
<li><a href="">#11627</a>: Restore support for copyright lines of the form <code>YYYY</code>
when <code>SOURCE_DATE_EPOCH</code> is set.</li>
</ul>
<h1>Release 7.2.4 (released Aug 28, 2023)</h1>
<h2>Bugs fixed</h2>
<ul>
<li><a href="">#11618</a>: Fix a regression in the MoveModuleTargets transform,
introduced in <a href="">#10478</a> (<a href="">#9662</a>).</li>
<li><a href="">#11649</a>: linkcheck: Resolve hanging tests for timezones west of London
and incorrect conversion from UTC to offsets from the UNIX epoch.
Patch by Dmitry Shachnev and Adam Turner.</li>
</ul>
<p>Release 7.2.3 (released Aug 23, 2023)</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cf7d275</code></a> Bump to 7.2.6 final</li>
<li><a href=""><code>43d6975</code></a> Leverage <code>importlib.reload</code> for reloading modules (<a href="">#11679</a>)</li>
<li><a href=""><code>13da5d7</code></a> Inline makecmd in make mode</li>
<li><a href=""><code>3d0110a</code></a> Enable test_cython on Python 3.12</li>
<li><a href=""><code>22759fb</code></a> Bump version</li>
<li><a href=""><code>fcc3899</code></a> Bump to 7.2.5 final</li>
<li><a href=""><code>2a631f9</code></a> Restore support for YYYY copyright lines</li>
<li><a href=""><code>2730cc3</code></a> Remove double spaces in CHANGES</li>
<li><a href=""><code>ff18318</code></a> Add an <code>'include-read'</code> event (<a href="">#11657</a>)</li>
<li><a href=""><code>74329d9</code></a> Fail better in <code>ExceptionDocumenter.can_document_member</code> (<a href="">#11660</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/sphinx-doc/sphinx/compare/v5.3.0...v7.2.6">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=sphinx&package-manager=pip&previous-version=5.3.0&new-version=7.2.6)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `47c3ba025c4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.