---
layout: page
title: "Rules"
permalink: /rules/
---

# Rules

We are aware that our test set is publicly available. However we strongly adivse against cheating of any kind (usage of external data, hyperparameter searches on the test set, ...) as we will examine the public repository of the awardees very thoroughly. **Any detected misconduct of an awardee team will result in disqualification from the competition**.

+ We only accept submissions that are fully reproducible (including any Hyperparameter searches).
+ The code repositories of all submissions have to be made public including instructions on how to train, make hyperparameter search and evaluate. Examples are our [Embedding baseline repository](https://github.com/nomisto/openbiolink-2021-embedding-baseline) and [Symbolic baseline repository](https://github.com/nomisto/openbiolink-2021-symbolic-baseline).
+ We do not allow the usage of external data. Only the usage of data provided by the [DataLoader](../dataset) (training and validation set) is allowed.
+ The candidates for each prediction task `(h,r,?)` and `(?,r,t)` are all entities in the dataset (Important for approaches that rely on the generation of corrupted triples for evaluation).
+ Persons affiliated with the core organizing team cannot participate in challenge.


