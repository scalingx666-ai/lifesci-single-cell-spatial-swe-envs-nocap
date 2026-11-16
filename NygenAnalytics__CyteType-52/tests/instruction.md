# Issue

**Title:** Add ontology term name and cell state to obs

## Description

### **PR Type**
Enhancement

___

### **Description**
- Add ontology term IDs and cell states to obs columns

- Separate ontology term names from IDs in API response

- Update API domain to production endpoint

- Improve documentation with visualization examples

___

### Diagram Walkthrough

```mermaid
flowchart LR
  API["API Response"] -->|Extract cellOntologyTermName| OntologyName["ontologyTerm"]
  API -->|Extract cellOntologyTerm| OntologyID["ontologyTermID"]
  API -->|Extract cellState| CellState["cellState"]
  OntologyName --> OBS["adata.obs columns"]
  OntologyID --> OBS
  CellState --> OBS
```

<details> <summary><h3> File Walkthrough</h3></summary>

<table><thead><tr><th></th><th align="left">Relevant files</th></tr></thead><tbody><tr><td><strong>Configuration changes</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>__init__.py</strong><dd><code>Version bump to 0.11.0</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/__init__.py

- Version bump from 0.10.0 to 0.11.0

</details>

  </td>
  <td><a href="">+1/-1</a>&nbsp; &nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>config.py</strong><dd><code>Update API domain to production endpoint</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/config.py

<ul><li>Update DEFAULT_API_URL from Modal endpoint to production domain<br> <li> Change from <code>https://nygen-labs-prod--cytetype-api.modal.run</code> to <br><code>https://prod.cytetype.nygen.io</code></ul>

</details>

  </td>
  <td><a href="">+1/-1</a>&nbsp; &nbsp; &nbsp; </td>

</tr>
</table></td></tr><tr><td><strong>Enhancement</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>api.py</strong><dd><code>Separate ontology term names and IDs</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/api.py

<ul><li>Split ontology term extraction into two fields: <code>ontologyTerm</code> (name) <br>and <code>ontologyTermID</code> (ID)<br> <li> Extract <code>cellOntologyTermName</code> for term names<br> <li> Extract <code>cellOntologyTerm</code> for term IDs</ul>

</details>

  </td>
  <td><a href="">+3/-0</a>&nbsp; &nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>main.py</strong><dd><code>Store ontology IDs and cell states in obs</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

cytetype/main.py

<ul><li>Add ontology term ID mapping to <code>adata.obs</code> with key <br><code>{results_prefix}_cellOntologyTermID_{group_key}</code><br> <li> Add cell state mapping to <code>adata.obs</code> with key <br><code>{results_prefix}_cellState_{group_key}</code><br> <li> Update success log message to include new columns</ul>

</details>

  </td>
  <td><a href="">+27/-0</a>&nbsp; &nbsp; </td>

</tr>
</table></td></tr><tr><td><strong>Documentation</strong></td><td><table>
<tr>
  <td>
    <details>
      <summary><strong>README.md</strong><dd><code>Update docs with improved examples</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

README.md

<ul><li>Update example API domain URL from Modal to production<br> <li> Improve code example with variable <code>group_key</code> for reusability<br> <li> Add UMAP visualization step to pipeline<br> <li> Update visualization examples to show all four annotation columns</ul>

</details>

  </td>
  <td><a href="">+13/-7</a>&nbsp; &nbsp; </td>

</tr>

<tr>
  <td>
    <details>
      <summary><strong>examples.md</strong><dd><code>Update all report links to production domain</code>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; </dd></summary>
<hr>

docs/examples.md

<ul><li>Replace all Modal API URLs with production domain across multiple <br>dataset links<br> <li> Update 16 report links to use <code>https://prod.cytetype.nygen.io</code></ul>

</details>

  </td>
  <td><a href="">+20/-20</a>&nbsp; </td>

</tr>
</table></td></tr></tr></tbody></table>

</details>

___

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dacf0a0d497d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.