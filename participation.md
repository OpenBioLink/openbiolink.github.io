---
layout: page
title: "OpenBioLink2021 Challenge"
permalink: /participation/
---

# 🚀 Participation

1. [Register your Team](https://forms.gle/nJZACsSN7RUQM7xM7)
2. [Make your submissions](https://forms.gle/ucNpmMKVVUfgtGzj6)

Please submit your approaches early, you can always overwrite your submission!

Note that your team name will be made publicly available in our leaderboards together with your model performance. For the awardees of each dataset, the team member information will be also made publicly available.

The code of all submissions has to be made public via a Github repository. It should include instructions on how to run the code from beginning to end (i.e. how to train a model, make hyperparameter searches and evaluate it) as we/the community will rerun the experiments of the awardees. **Everything should be reproducible**. Examples how we expect the repository to look like are our [embedding baseline repository](https://github.com/nomisto/openbiolink-2021-embedding-baseline) and [symbolic baseline repository](https://github.com/nomisto/openbiolink-2021-symbolic-baseline).

## Evaluation


  
<div markdown="block" style="margin-top:1rem;">

| ⚠️ For approaches that rely heavily on random number generators (such as most embedding approaches) we require **three submissions**: for each submission the model should be trained with a different random state (seed). All three models have to be trained with the same hyperparameters (if any).|

</div>

### Protocol and metric

All models are evaluated using the hits@10 metric, which is formally defined in the following. Let $$\mathcal{K}$$ be the set of all triples within the dataset, $$\mathcal{K}^{\text{test}}$$ be the set of test triples and $$\mathcal{E}$$ be the set of entities in $$\mathcal{K}$$. Given a triple $$(h, r, t)$$ of $$\mathcal{K}^{\text{test}}$$, the rank of $$(t \vert h,r)$$ is the filtered rank of object $$t$$, i.e. the rank of model score $$s(h,r,t)$$ among the collection of all pseudo-negative-object scores

<div class="formula-wrapper" markdown="block">

$$\{s(h,r,t'): t' \in \mathcal{E} \:\text{and}\: (h,r,t') \notin \mathcal{K}\}$$

</div>

Define rank of $$(h \vert r,t)$$ likewise. Then Hits@10 is calculated as:

<div class="formula-wrapper" markdown="block">

$$Hits@10 = \frac{1}{2* \vert \mathcal{\mathcal{K}^{\text{test}}} \vert} \sum_{(h,r,t) \in \mathcal{K}^{\text{test}}} \Big( 1(\text{rank}(t \vert h,r) \leq 10) + 1(\text{rank}(h \vert r,t) \leq 10 \Big)$$

</div>

To avoid artificially boosting performances: The score of the positive triple $$s(h,r,t)$$ must not be treated differently than the scores of pseudo-negative triples. Thus every approach should generate the ranking of entities according to the *random* or *ordinal* policy for dealing with same score entities. (For further information see page 4 in [Knowledge Graph Embedding for Link Prediction: A Comparative Analysis; Rossi et al](https://export.arxiv.org/pdf/2002.00819)).

<table style="width:100%;">
  <thead>
    <tr>
      <td align="left" style="border-bottom:none;">
        ⚠️ Two major things to take away here:
      </td>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td style="border-top:none;">
        <ul style="margin:0px;">
          <li>The number of negative evaluation triples is equal to number of entities in the dataset (Corruption with all entities)</li>
          <li>Do not use <i>top</i> policy (Inserting the correct entity on place one of a group of same score entities)</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Evaluator (Python package)

To create a submission for a model our provided evaluator `OBL2021Evaluator` has to be used, which evaluates predictions in a standardized way. A detailed documentation of it can be found [here](../obl2021.html#obl2021.OBL2021Evaluator).

First you have to prepare:
+ `top10_heads`: torch.Tensor or numpy.array of shape (num_testing_triplets, 10)
    *  Top 10 ranked predictions for the head entity. The value at (i,j) is the ID of the predicted head entity with rank `j+1` for the triple `dl.testing[i]`     
+ `top10_tails`: torch.Tensor or numpy.array of shape (num_testing_triplets, 10)
    * Top 10 ranked predictions for the tail entity. The value at (i,j) is the ID of the predicted tail entity with rank `j+1` for the triple `dl.testing[i]`

You can then run the evaluation by calling the evaluators `eval(...)` function with `top10_heads`, `top10_tails` and the set of test triples which can be retrieved from the Dataset module `dl.testing`. The `eval(...)` function creates a submission file in the location the script is started from and displays the calculated hits@10 metric which you also have to submit.

{% highlight python %}
from openbiolink.obl2021 import OBL2021Dataset, OBL2021Evaluator
dl = OBL2021Dataset()
ev = OBL2021Evaluator()
ev.eval(top10_heads, top10_tails, dl.testing)
{% endhighlight %}

## Minimal working example

The following code produces the score and the file needed for submission. The file is generated in the location from where the script is started. For the submission you need to copy and paste the line that starts with `{'h10': ...` to the submission form.

{% highlight python %}

"""
Import of the OpenBioLink Dataset and Evaluator.
"""
import torch
from tqdm import tqdm
from openbiolink.obl2021 import OBL2021Dataset, OBL2021Evaluator
from numpy.random import default_rng

class MockupModel:
    def __init__(self):
        self.rng = default_rng(0)

    def getTop10Heads(self, batch):
        rand = [self.rng.choice(180992, 10, replace=False) for _ in range(batch.shape[0])]
        return torch.tensor(rand)
    
    def getTop10Tails(self, batch):
        rand = [self.rng.choice(180992, 10, replace=False) for _ in range(batch.shape[0])]
        return torch.tensor(rand)

def main():
    # Mockup Model
    model = MockupModel()

    # Initialize dataset and evaluator
    dl = OBL2021Dataset()
    ev = OBL2021Evaluator()
    
    top10_heads = []
    top10_tails = []
    
    n_batches, batches = dl.get_test_batches(100)
    for batch in tqdm(batches, total=n_batches):
        top10_tails.append(model.getTop10Heads(batch))
        top10_heads.append(model.getTop10Tails(batch))
    top10_heads = torch.cat(top10_heads, dim=0)
    top10_tails = torch.cat(top10_tails, dim=0)
    
    ev.eval(top10_heads, top10_tails, dl.testing)

if __name__ == "__main__":
    main()
{% endhighlight %}

Above code should result in the following output:

{% highlight bash %}
Dataset not found, downloading to C:/Users/MyUser/Desktop/obl2021 ...
KGID_HQ_DIR.zip: 45.2MB [00:06, 7.47MB/s]                            
100%|██████████| 1810/1810 [00:05<00:00, 311.50it/s]
Submission file saved here: C:/Users/MyUser/Desktop/pred_OBL2021.npz
Please copy the following line in the respective field of the submission form:
{'h10': 4.697066833614372e-05}
{% endhighlight %}
