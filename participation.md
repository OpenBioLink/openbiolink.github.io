---
layout: page
title: "Participation"
permalink: /participation/
---

# Participation

1. Register your Team: TBD Link to registration form
2. Make your submission: TBD Link to submission form

Your team name will be made publicly available in our leaderboards together with your model performance. For the awardees of each dataset, the team member information will be also made publicly available.

## Evaluation

To evaluate a trained model for submission you have to use our provided evaluator `openbiolink.obl2021.OBL2021Evaluator`, which evaluates a models prediction in a standardized way. A detailed documentation of it can be found [here](../obl2021.html#obl2021.OBL2021Evaluator).

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

Following code produces the score and the file needed for submission. The file is generated in the location from where the script is started. For the submission you need to copy and paste the line that starts with `{'h10': ...` to the submission form.

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
        rand = []
        for i in range(batch.shape[0]):
            rand.append(self.rng.choice(180992, 10, replace=False))
        return torch.tensor(rand)

    def getTop10Tails(self, batch):
        rand = []
        for i in range(batch.shape[0]):
            rand.append(self.rng.choice(180992, 10, replace=False))
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
