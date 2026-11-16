# Issue

**Title:** Obsm in duckdb

## Description

### **PR Type**
Enhancement

___

### **Description**
- Store observation coordinates in DuckDB artifact

- Improved cluster ID mapping logic for short values

- Increased annotation job timeout to 180 seconds

- Version bump to 0.17.0

___

### Diagram Walkthrough

```mermaid
flowchart LR
  A["obsm coordinates"] -- "extract if available" --> B["save_obs_duckdb"]
  B -- "add as __vis_coordinates columns" --> C["DuckDB table"]
  D["cluster categories"] -- "check if all short" --> E["cluster_map logic"]
  E -- "use original labels or enumerate" --> F["cluster IDs"]
  G["annotation job"] -- "increase timeout" --> H["180 seconds"]
```

<details><summary><h3>File Walkthrough</h3></summary>

<table><thead><tr><th></th><th align="left">Relevant files</th></tr></thead><tbody><tr><td><strong>Configuration changes</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>__init__.py</strong><dd><code>Version bump to 0.17.0</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/__init__.py

- Version bumped from 0.16.1 to 0.17.0

</details>

  </td>
  <td><a href="">+1/-1</a>&nbsp; &nbsp; &nbsp; </td>

</tr>
</table></td></tr><tr><td><strong>Enhancement</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>client.py</strong><dd><code>Increase annotation timeout to 180 seconds</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/api/client.py

- Increased annotation job submission timeout from 60 to 180 seconds

</details>

  </td>
  <td><a href="">+1/-1</a>&nbsp; &nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>artifacts.py</strong><dd><code>Add obsm coordinates storage to DuckDB</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/core/artifacts.py

<ul><li>Added <code>obsm_coordinates</code> and <code>coordinates_key</code> parameters to <br><code>save_obs_duckdb</code> function<br> <li> Extract coordinate dimensions and store as <code>__vis_coordinates_{key}_1</code> <br>and <code>__vis_coordinates_{key}_2</code> columns in obs DataFrame</ul>

</details>

  </td>
  <td><a href="">+7/-0</a>&nbsp; &nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>main.py</strong><dd><code>Implement smart cluster ID mapping and coordinate passing</code></dd></summary>
<hr>

cytetype/main.py

<ul><li>Modified cluster ID mapping to use original labels if all are short <br>(<=3 chars), otherwise enumerate from 0<br> <li> Pass <code>coordinates_key</code> to <code>_build_and_upload_artifacts</code> method<br> <li> Extract obsm coordinates and pass to <code>save_obs_duckdb_file</code> function<br> <li> Added logic to check coordinate availability before extraction</ul>

</details>

  </td>
  <td><a href="">+16/-2</a>&nbsp; &nbsp; </td>

</tr>
</table></td></tr></tbody></table>

</details>

___

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fab67118cfc2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.