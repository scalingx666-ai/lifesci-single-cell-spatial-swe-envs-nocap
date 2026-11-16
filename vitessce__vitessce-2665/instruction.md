# Issue

**Title:** NickAkhmetov/Fix bundle size comment churn from hashed chunk names

## Description

#### Background

The bundle size comment lists unchanged chunks as "removed" and "new file", and it reports large size swings for `index-********.js`. Example:

There are two causes:

1. **Hashes with dashes are not stripped.** Rollup hashes use the base64url alphabet (`[A-Za-z0-9_-]`), but the `strip-hash` regex only matched `\w`. When a hash contains a dash (for example `Iu1-a80m`), the old and new file names do not match.
2. **Several chunks are named `index-[hash].js`.** The lazy-loaded `@vitessce/spatial-three` and `@vitessce/spatial-accelerated` chunks are named after their `index.js` entry, the same as the main chunk. compressed-size-action keys file sizes by name after it strips the hash. All three chunks map to `index-********.js` and overwrite each other, so the reported size depends on which hash sorts last.

#### Change List

- `.github/workflows/bundle-size.yml`: change `strip-hash` to `-([\w-]{8})\.js$`.
- `packages/main/prod/vite.config.mjs`: add `output.chunkFileNames`. When a chunk would be named `index` and its last module is a workspace package's `dist-tsc/index.js`, name the chunk after the package directory. The main chunk keeps the name `index`.
- Changeset (patch for `vitessce`), because the published chunk file names change.

#### Testing

I ran `pnpm -C packages/main/prod build`. The output now has `index-*.js` (12 MB), `spatial-three-*.js` (45 kB) and `spatial-accelerated-*.js` (147 kB). Before this change, all three were named `index-*.js`.

I applied the action's `stripHash` logic to the new `dist/` file names. Every hash is stripped, and no two files map to the same name.

#### Checklist
 - [ ] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable
 - [x] New subpackage(s) manually published to NPM and trusted publishing enabled, or not applicable

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7608fcd065de`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.