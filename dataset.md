---
layout: page
title: "Dataset"
permalink: /dataset/
---

# Dataset

The OpenBioLink2021 Dataset is a highly challenging benchmark dataset containing about 4.5 billion high quality biomedical facts from various renowned biomedical knowledge bases. The dataset was split randomly with a ratio of 90-5-5.

| # Train   | # Valid | # Test  | # Entities | # Relations |
|-----------|---------|---------|------------|-------------|
| 4,192,002 | 186,301 | 180,964 | 180,992    | 28          |

The dataset can be downloaded [here](https://zenodo.org/record/5361324/files/KGID_HQ_DIR.zip?download=1) or loaded with the provided DataLoader, which is further documented [here](../obl2021.html#obl2021.OBL2021Dataset)

{% highlight python %}

from openbiolink.obl2021 import OBL2021Dataset

dl = OBL2021Dataset()

train = dl.training # torch.tensor of shape(num_train,3)
valid = dl.validation # torch.tensor of shape(num_val,3)

{% endhighlight %}