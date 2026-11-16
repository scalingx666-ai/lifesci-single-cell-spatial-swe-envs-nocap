# Issue

**Title:** NickAkhmetov/Fix handling of 403 responses during config generation and add tests for .zmetadata access

## Description

#### Background

Passing `https://data-1.vitessce.io/0.0.33/main/meta-2022-azimuth/meta_2022_azimuth.h5ad.zarr` to the config generator in the docs View Config Editor failed with:

```
Error: Could not generate config for URL https://.../meta_2022_azimuth.h5ad.zarr: Error: Could not generate config: setMetadataSummary
```


That store has no consolidated metadata, and the bucket returns **403 AccessDenied rather than
404** for keys that do not exist — the bucket policy grants `s3:GetObject` but not `s3:ListBucket`,
so S3 masks non-existence as AccessDenied. Verified by direct request:

| key | status |
|---|---|
| `/.zmetadata` | 403 (missing) |
| `/obsm/X_umap/.zarray` | 200 |
| `/obsm/X_pca/.zarray` | 403 (missing) |
| `/obs/.zattrs` | 200 |
| `/X/.zarray` | 200 |
| `/zarr.json` | 403 (missing) |

Both config generators assumed missing == 404, so both failed on this bucket:

- `VitessceAutoConfig.js` (used by the docs editor) branched on `response.ok` and exactly
  `response.status === 404`; a 403 fell through to
  `throw new Error(\`Could not generate config: ${response.statusText}\`)`. `statusText` is `""` in
  browsers over HTTP/2, so the visible tail was empty and the trailing `setMetadataSummary` came
  from the stack frame.
- `generate-config.js` (`generateConfigAlt`, used by the launcher and drag-and-drop) built a bare
  `new FetchStore(url)`. zarrita's `handle_response` returns `undefined` only for 404 and throws
  for every other non-200/206 status, so `zarrOpen(store, { kind: 'group' })` threw on the 403
  from `/zarr.json`.

The store itself is fine — the non-consolidated fallback already filters probe responses on `.ok`
and produces a usable config once it is reached.

The repo already solved this for the main data-loading path: `relaxedFetch` in
`packages/utils/zarr-utils/src/normalize.ts` maps a 403 response to a synthetic 404 before zarrita
sees it. It was module-private and unused by either generator.

#### Change List

- `packages/config/src/VitessceAutoConfig.js`: treat any non-ok `.zmetadata` response as "not
  consolidated" and fall back to probing known keys, instead of only handling 404 and throwing
  otherwise.
- `packages/utils/zarr-utils/src/normalize.ts`, `src/index.ts`: export the existing `relaxedFetch`
  helper.
- `packages/config/src/generate-config.js`: pass `relaxedFetch` to `FetchStore` in `getStore()`, so
  the newer generator tolerates the same buckets.
- `packages/config/src/VitessceAutoConfig.test.js`: regression test that stubs `fetch` to turn the
  fixture's 404 for `.zmetadata` into a 403, and asserts a config is still generated.
- Changeset (patch) for `@vitessce/config` and `@vitessce/zarr-utils`.


#### Checklist

 - [x] Have tested PR with one or more demo configurations
 - [x] Documentation added, updated, or not applicable

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `49b8bbf76981`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.