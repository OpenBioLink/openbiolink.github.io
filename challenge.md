---
layout: page
title: "OpenBioLink2021 Challenge"
permalink: /
---

# ⛰️ Challenge

 To foster progress in link prediction on large-scale, heterogeneous biomedical data, we invite you to participate in the OpenBioLink Challenge. Link Prediction on knowledge graphs is a versatile paradigm for generating new insights about relationships between entities. It is especially important in fields such as biomedical research, where it can help with hypothesis generation, prioritizing drug targets or therapeutic substances for experimental screening etc.

## 🕑 Timeline

<div class="table-wrapper" markdown="block">

| Task                      |     Deadline              |                                               |
|---------------------------|---------------------------|-----------------------------------------------|
| Team registration         |            -              |  [Link](https://forms.gle/nJZACsSN7RUQM7xM7)  |
| Submission deadline       | 01.12.2021 - 23:59 GMT-0  |  [Link](https://forms.gle/ucNpmMKVVUfgtGzj6)  |

</div>

There is no deadline for registering your team however, you'll need to register to OpenBioLink2021 before being able to make a submission.

## 🏆 Prizes

+ Best predictive performance prize (**500 €**)
+ Best explainability prize (**500 €**)

The **best predictive performance** prize will be awarded to the model with the best result in terms of predictive accuracy (measured with the Hits@10 metric). It can only be given to submissions that improve on current baseline results.

The **best explainability prize** will be awarded to innovative models that provide good explanations for their predictions. Explainability is an important and still largely unaddressed issue in biomedical link prediction, and we want to foster the creation of explainable algorithms. The OpenBioLink challenge team will evaluate the quality of explanations and the innovativeness of the approach. Predictive performance is not a major criterion for winning the explainability prize, but it must exceed a Hits@10 value of 0.440.

It is possible for a team to win both prizes, i.e. to be awarded 1000 € in total.

Results of the challenge will be published in a joint paper on arXiv (and potentially a peer-reviewed journal), **including as co-authors members of all teams that made any submission** and who agree to be listed as co-authors. Even results of novel methods that do not improve upon the baseline results are expanding knowledge, and we welcome these submissions. 

Challenge participants are of course free to also publish about their work in their own scientific publications.

## 📈 Baseline results

The code of our embedding baseline models is located [here](https://github.com/nomisto/openbiolink-2021-embedding-baseline), the code for our explainable baseline is located [here](https://github.com/nomisto/openbiolink-2021-symbolic-baseline).

<div class="table-wrapper" markdown="block">

| Model          | Hits@10 | Explainable? | Paper |
|----------------|---------|--------------|-------|
| DistMult       | 0.542   |              | [here](https://arxiv.org/pdf/1412.6575.pdf) |
| RotatE         | 0.527   |              | [here](https://proceedings.mlr.press/v48/trouillon16.pdf) |
| ComplEx        | 0.514   |              | [here](https://openreview.net/pdf?id=HkgEQnRqYQ) |
| SAFRAN         | 0.507   | X            | [here](https://openreview.net/pdf?id=jCt9S_3w_S9) |
| AnyBURL        | 0.463   | X            | [here](https://arxiv.org/pdf/2004.04412.pdf) |
| TransE         | 0.446   |              | [here](https://papers.nips.cc/paper/2013/file/1cecc7a77928ca8133fa24680a88d2f9-Paper.pdf) |
| RESCAL*        | 0.408   |              | [here](https://icml.cc/2011/papers/438_icmlpaper.pdf) |
| TransR*        | 0.247   |              | [here](https://iie-liuyong.github.io/files/PCS-le.pdf) |

</div>

*Models of the [dgl-ke](https://github.com/awslabs/dgl-ke) framework, which are under suspicion to be bugged, see this [issue](https://github.com/awslabs/dgl-ke/issues/225).

## 🛠️ OpenBioLink Python Module

We provide a python package for [loading](./dataset) the openbiolink dataset and [evaluating](./participation) your approach. To install the package:

1. Install [pytorch](https://pytorch.org/)
2. Install the `openbiolink` package, (Version 0.1.4)

{% highlight bash %}
pip install openbiolink==0.1.4
{% endhighlight %}

## 🙋 Questions

If you have any questions where you feel like others can profit from their answers, feel free to create a discussion on our [Github repository](https://github.com/OpenBioLink/OpenBioLink/discussions/categories/obl2021). For all other questions please write us an email at *simon.ott [at] meduniwien.ac.at*.

The challenge is based on the OpenBioLink benchmark, first described in: Anna Breit, Simon Ott, Asan Agibetov and Matthias Samwald. **„OpenBioLink: A benchmarking framework for large-scale biomedical link prediction“**. *Bioinformatics* 36, Nr. 13 (July 2020): 4097–98. https://doi.org/10.1093/bioinformatics/btaa274.