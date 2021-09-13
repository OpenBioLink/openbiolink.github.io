---
layout: page
title: "Rules"
permalink: /rules/
---

# Rules

We are aware that our test set is publicly available. However we strongly adivse against cheating of any kind (usage of external data, hyperparameter searches on the test set, ...) as we will examine the public repository of the awardees very thoroughly. **Any detected misconduct of an awardee team will result in disqualification from the competition**.

+ We only accept submissions that are fully reproducible (including any Hyperparameter searches).
+ The code repositories of all submissions have to be made public
+ We do not allow the usage of external data. Only the usage of data provided by either the [python dataloader module](../dataset) or the [downloadable resource](https://zenodo.org/record/5361324/files/KGID_HQ_DIR.zip) is allowed.
+ It is not allowed to resplit the dataset (i.e. use a larger/smaller validation set) or use the sets other than their intended use (f.e. train a model on the union of training and validation set).
+ The intended uses of the different sets are:
    * Training set: Used during the learning process (e.g. to fit parameters) of a model
    * Validation set: Used to tune hyperparameters/model selection
    * Test set: Used **only** during the final evaluation process
+ Persons affiliated with the core organizing team cannot participate in challenge.
