# Issue

**Title:** Newest Version of JEPA

## Description

The most important files written by Seb or me are listed below. Please provide your feedback on all the files, with a particular focus on emb_utils.py, config_utils.py, eval_utils.py, train.py, and eval.py.

main.py
The main entry point for the project, which supports running training and evaluation sweeps. It includes command-line arguments for customization and handles multi-GPU setups.

configs/cnd_gtb10_ep300.yaml
This configuration file defines the hyperparameters and settings used during the training process, such as model architecture, data handling, and optimization settings.

src/nichejepa/models/gene_transformer.py
Contains the model definition for the gene transformer, implementing the core architecture that will be trained and evaluated.

src/nichejepa/train.py
Handles the training process in a distributed setting. This script contains the logic for executing the training loop and logging results.

src/nichejepa/eval.py
Manages the evaluation process. It evaluates the trained model on the specified tasks and logs the performance metrics.

src/nichejepa/utils/emb_utils.py
Provides utility functions for handling and loading embeddings required by the model during training and inference.

src/nichejepa/utils/eval_utils.py
Includes helper functions to streamline the evaluation process, such as metrics calculations and data preparation.

src/nichejepa/utils/config_utils.py
Includes helper functions to setup the model and batch size params.

src/nichejepa/datasets/cell_neighborhood_dataset.py

Includes helper functions to create datasets.

tests
Includes test cases for differnet functions.

I now have a preliminary notebook on reproducibility_notebook_pre_merge on how to use the model, but I will update it today and push it back to nichejepa-reproducibility.

This version has not been updated for cls yet, but I will correct that today as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `157796df5b11`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.