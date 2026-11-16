# Issue

**Title:** crs-registration

## Description

**ST vs ST integration/alignment:**

* VoltRon (R-native, GitHub):

  -  https://github.com/BIMSBbioinfo/VoltRon
  -  https://bioinformatics.mdc-berlin.de/VoltRon/conversion.html#SpatialExperiment
  -  https://bioinformatics.mdc-berlin.de/VoltRon/registration.html#Alignment_of_Xenium_and_HE
  
* STAlign (Python, reticulate/basilisk):

  - https://github.com/JEFworks-Lab/STalign

TODO: ST vs scRNA integration

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e7c28f3da1e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.