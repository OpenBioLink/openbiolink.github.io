---
layout: page
title: "OpenBioLink2021 Challenge"
permalink: /
---

**!!! This challenge has not started yet !!!**

# Challenge

To foster progress in link prediction on large-scale, heterogeneous biomedical data, we invite you to participate in the OpenBioLink Challenge. Link Prediction on knowledge graphs is a versatile paradigm for generating new insights about relationships between two entities. It is especially important in fields such as biomedical research, where it can help with hypothesis generation, prioritizing drug targets or therapeutic substances for experimental screening etc.

# Timeline


| Task                      |     Deadline              |               |
|---------------------------|---------------------------|---------------|
| Team registration         |            -              |  [Link](TBD)  |
| Submission deadline       | 01.12.2021 - 23:59 GMT-0  |  [Link](TBD)  |

There is no deadline for registering your team however, you'll need to register to OpenBioLink2021 before being able to make a submission.

# Prizes

+ Best predictive performance prize (**750 €**)
+ Best explainability prize (**250 €**)

Best predictive performance prize can only be given to submissions that improve on current baseline results. Best explainability prize will be awarded based on evaluation by the OpenBioLink Challenge team. Furthermore, results of the challenge will be published in a joint paper on arXiv (and potentially a peer-reviewed journal). Challenge participants are of course free to also publish about their work in their own scientific papers.

# Baseline results

The code of our embedding baseline models is located [here](https://github.com/nomisto/openbiolink-2021-embedding-baseline), the code for our explainable baseline is located [here](https://github.com/nomisto/openbiolink-2021-symbolic-baseline).

| Model          | Hits@10 | Explainable? |
|----------------|---------|--------------|
| DistMult       | 0.540   |              |
| RotatE         | 0.526   |              |
| ComplEX        | 0.524   |              |
| AnyBURL        | 0.460   | X            |
| TransE         | 0.449   |              |

# OpenBioLink Python Module

We provide a python package for [loading](./dataset) the openbiolink dataset and [evaluating](./participation) your approach. To install the package:

1. Install [pytorch](https://pytorch.org/)
2. Install the `openbiolink` package, (Version 0.1.4)

{% highlight bash %}
pip install openbiolink==0.1.4
{% endhighlight %}

# Questions

If you have any questions where you feel like others can profit from their answers, feel free to create a discussion on our [Github repository](https://github.com/OpenBioLink/OpenBioLink/discussions/categories/obl2021). For all other questions please write us an email at TBD.