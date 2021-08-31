---
layout: page
title: "Participation"
permalink: /participation/
---

# Participation

1. Register your Team: TBD Link to registration form
2. Make your submission: TBD Link to submission form

## Evaluation

To evaluate a trained model on a OpenBioLink dataset a subclass of `openbiolink.evaluation.evaluation.Evaluator` has to be created that implements the function `score_batch()` function. A reference to this class can be found [here](../obl2021.html#obl2021.OBL2021Evaluator).

### Implementing `__init__`

The `Evaluator` class uses an instantiation of `openbiolink.evaluation.dataLoader.DataLoader`, which is used to download the specified version of the OpenBioLink dataset, see also (here)[""].

### Implementing `score_batch()`

The function `score_batch` is used to retrieve the scores of a set of test triples. It gets called with a tensor of batch test triples (shape `(batch_size, 3)`) and should return a tuple `(score_head, score_tail)`, two tensors of shape `(batch_size, num_entities)`. OpenBioLink is evaluated by corrupting the head/tail of a triple with all possible entities in the dataset. Consider $$\mathcal{K} = (\mathcal{E},\mathcal{R},\mathcal{T})$$ where $$\mathcal{E}$$ is the set of unique entities, $$\mathcal{R}$$ is the set of unique relations, and $$\mathcal{T}$$ are the triples in the dataset. Then the corrupted tail triples for a positive triple $$(h, r, t)$$ are $$(h, r, e)$$ for $$e \in \mathcal{E}$$ and the corrupted head triples are $$(e, r, t)$$ for $$e \in \mathcal{E}$$. The value of `score_head[i,j]` is then the score of `(j, batch[i,1], batch[i,2])`, while the value of `score_tail[i,j]` is the score of the triple `(batch[i,0], batch[i,1], j)`.

### Calling function `evaluate()`

After the creation of a custom class that implements `Evaluator`, your approach can be evaluated by calling `evaluate(batch_size)` with the desired size of the batch that gets passed to `score_batch()`.

### Example

The following is a sketch of how to use the evaluator to create a submission file. Concrete examples of evaluating an embedding model trained with [dgl-ke]("") can be seen [here]("") and an example of evaluating the symbolic rule-based approach [AnyBURL/SAFRAN]("") can be seen [here]("").

{% highlight python %}

"""
Import of the OpenBioLink Dataset and Evaluator.
"""
import torch
from openbiolink.obl2021 import OBL2021Dataset, OBL2021Evaluator

"""
Implementation of the score_batch function of the OBL2021 class
"""
class MyEval(OBL2021Evaluator):
    def __init__(self, model):
        dl = OBL2021Dataset()
        super().__init__(dl)
        self.model = model

    def score_batch(self, batch):
        # of shape (batch.size()[0], self.dl.num_entities)
        head_scores = self.model.score_heads(batch[:,1], batch[:,2]) 
        # of shape (batch.size()[0], self.dl.num_entities)
        tail_scores = self.model.score_tails(batch[:,0], batch[:,1]) 
        return head_scores, tail_scores

if __name__ == "__main__":
    ev = MyEval()
    ev.evaluate(100)
	
{% endhighlight %}
