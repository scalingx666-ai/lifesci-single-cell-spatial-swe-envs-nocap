# Issue

**Title:** build(deps): bump memchr from 2.8.2 to 2.8.3 in the cargo-patch-minor group

## Description

Bumps the cargo-patch-minor group with 1 update: [memchr](https://github.com/BurntSushi/memchr).

Updates `memchr` from 2.8.2 to 2.8.3
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5fdb40c</code></a> 2.8.3</li>
<li><a href=""><code>922c7b5</code></a> memchr: let compiler know that indexes returned by memchr fns are in bounds</li>
<li><a href=""><code>e21e9fb</code></a> arch: add <code>unsafe</code> to internal routines</li>
<li><a href=""><code>581faf0</code></a> rebar: update memchr version</li>
<li>See full diff in <a href="https://github.com/BurntSushi/memchr/compare/2.8.2...2.8.3">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=memchr&package-manager=cargo&previous-version=2.8.2&new-version=2.8.3)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `427cef49f76e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.