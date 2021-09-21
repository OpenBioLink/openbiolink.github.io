---
layout: page
title: "OpenBioLink2021 Challenge"
permalink: /dataset/
---

# Dataset

The OpenBioLink2021 Dataset is a highly challenging benchmark dataset containing about 4.5 million high quality biomedical facts from various renowned biomedical knowledge bases. The dataset was split randomly with a ratio of 90-5-5.

<div class="table-wrapper" markdown="block">

| # Train   | # Valid | # Test  | # Entities | # Relations |
|-----------|---------|---------|------------|-------------|
| 4,192,002 | 186,301 | 180,964 | 180,992    | 28          |

</div>

The dataset can be downloaded from [https://zenodo.org/record/5361324/files/KGID_HQ_DIR.zip](https://zenodo.org/record/5361324/files/KGID_HQ_DIR.zip?download=1) or loaded with the provided python dataloader module, which is further documented [here](../obl2021.html#obl2021.OBL2021Dataset). Please make sure that you get the dataset from one of the two sources, as other versions of OpenBioLink may differ. 

{% highlight python %}

from openbiolink.obl2021 import OBL2021Dataset

dl = OBL2021Dataset()

train = dl.training # torch.tensor of shape(num_train,3)
valid = dl.validation # torch.tensor of shape(num_val,3)

{% endhighlight %}