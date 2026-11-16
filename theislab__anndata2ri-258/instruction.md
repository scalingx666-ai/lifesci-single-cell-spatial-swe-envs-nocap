# Issue

**Title:** Update sphinx requirement from <9 to <10

## Description

Updates the requirements on [sphinx](https://github.com/sphinx-doc/sphinx) to permit the latest version.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/releases">sphinx's releases</a>.</em></p>
<blockquote>
<h2>Sphinx 9.0.4</h2>
<p>Changelog: <a href="https://www.sphinx-doc.org/en/master/changes/9.0.html">https://www.sphinx-doc.org/en/master/changes/9.0.html</a></p>
<h2>Bugs fixed</h2>
<ul>
<li><a href="">#14143</a>: Fix spurious build warnings when translators reorder references
in strings, or use translated display text in references.
Patch by Matt Wang.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sphinx-doc/sphinx/blob/v9.0.4/CHANGES.rst">sphinx's changelog</a>.</em></p>
<blockquote>
<h1>Release 9.0.4 (released Dec 04, 2025)</h1>
<h2>Bugs fixed</h2>
<ul>
<li><a href="">#14143</a>: Fix spurious build warnings when translators reorder references
in strings, or use translated display text in references.
Patch by Matt Wang.</li>
</ul>
<h1>Release 9.0.3 (released Dec 04, 2025)</h1>
<h2>Bugs fixed</h2>
<ul>
<li><a href="">#14142</a>: autodoc: Restore some missing exports in :mod:<code>!sphinx.ext.autodoc</code>.
Patch by Adam Turner.</li>
</ul>
<h1>Release 9.0.2 (released Dec 03, 2025)</h1>
<h2>Bugs fixed</h2>
<ul>
<li><a href="">#14142</a>: autodoc: Restore :mod:<code>!sphinx.ext.autodoc.mock</code>.
Patch by Adam Turner.</li>
</ul>
<h1>Release 9.0.1 (released Dec 01, 2025)</h1>
<h2>Bugs fixed</h2>
<ul>
<li><a href="">#13942</a>: autodoc: Restore the mapping interface for options objects.
Patch by Adam Turner.</li>
<li><a href="">#13942</a>: autodoc: Deprecate the mapping interface for options objects.
Patch by Adam Turner.</li>
<li><a href="">#13387</a>: Update translations.</li>
</ul>
<h1>Release 9.0.0 (released Nov 30, 2025)</h1>
<h2>Dependencies</h2>
<ul>
<li>
<p><a href="">#13786</a>: Support <code>Docutils 0.22</code>_. Patch by Adam Turner.</p>
<p>.. _Docutils 0.22: <a href="https://docutils.sourceforge.io/RELEASE-NOTES.html#release-0-22-2026-07-29">https://docutils.sourceforge.io/RELEASE-NOTES.html#release-0-22-2026-07-29</a></p>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8ddba7e</code></a> Bump to 9.0.4 final</li>
<li><a href=""><code>6959633</code></a> [bot]: Update message catalogues (<a href="">#14155</a>)</li>
<li><a href=""><code>88a4a97</code></a> Allow reordered refs and translated display text in pending_xref (<a href="">#14144</a>)</li>
<li><a href=""><code>f666208</code></a> Bump version</li>
<li><a href=""><code>df8a9e7</code></a> Bump to 9.0.3 final</li>
<li><a href=""><code>bd89f96</code></a> Import names from defining module</li>
<li><a href=""><code>7d05936</code></a> autodoc: Restore some missing exports</li>
<li><a href=""><code>b745a11</code></a> Bump version</li>
<li><a href=""><code>1ac581c</code></a> Bump to 9.0.2 final</li>
<li><a href=""><code>1281a83</code></a> autodoc: Restore <code>mock</code> module for compatibility (<a href="">#14152</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/sphinx-doc/sphinx/compare/v0.1.61611...v9.0.4">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0ca7a2342cb2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.