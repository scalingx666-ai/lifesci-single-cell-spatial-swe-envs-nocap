# Issue

**Title:** Add H0-mini model.

## Description

This PR integrates:

- The implementation of `H0-mini`. The model is available on [Hugging Face](https://huggingface.co/bioptimus/H0-mini).
- The implementation of `Kaiko ViT B/8` and `Hibou Large` available respectively on [Github](https://github.com/kaiko-ai/towards_large_pathology_fms) and [Hugging Face](https://huggingface.co/histai/hibou-L). 


Note:
- H0-mini is a ViT-B model with 768 output dimensions

To reproduce our results, you first need to be granted access to `bioptimus/H0-mini` on HF. Then, simply run `python src/hest/bench/benchmark.py --config bench_config/custom_bench_config.yaml` with `custom_bench_config.yaml`:

```yaml
# directory containing the data for each task
bench_data_root: '/root_dir/HEST/bench_data'

# directory where benchmark results will be dumped
results_dir: '/root_dir/HEST/ST_pred_results'

# directory where the vision embeddings will be dumped
embed_dataroot: '/root_dir/HEST/ST_data_emb'

# directory to the model weights root
weights_root: '/root_dir/HEST/fm_v1'

# inference parameters
batch_size: 128
num_workers: 16

# encoders to benchmark
encoders: [
  "h0_mini"
]

# datasets contained in `bench_data_root` to benchmark
datasets: [
  "IDC",
  "PRAD",
  "PAAD",
  "SKCM",
  "COAD",
  "READ",
  "CCRCC",
  "HCC",
  "LUNG",
  "LYMPH_IDC",
]

dimreduce: "PCA" 
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `07bda9b1ee07`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.