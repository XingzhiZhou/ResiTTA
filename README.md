## ResiTTA

[ICASSP 2025] Resilient Test-Time Adaptation by Mitigating Batch-Normalization Overfitting

Implementation of ResiTTA in Pytorch. It is a resilient practical test-time adaptation method (ResiTTA), employing soft constraints on the BN statistics and a low-entropy sampling strategy, which reduces overfitting on domain shifts and enables rapid adaptation. The main model logic is implemented in resitta.py

## Install packages

```bash
$ pip install -r requirements.txt
```

## Usage of the model

```python
import torch
from yacs.config import CfgNode as cdict
from torchvision import models as pt_models
from resitta import normalize_model, ResiTTA


mu = (0.485, 0.456, 0.406)
sigma = (0.229, 0.224, 0.225)
backbone = normalize_model(pt_models.resnet50(pretrained=True), mu, sigma)

cfg = cdict(new_allowed=True)
cfg.merge_from_file('config.yml')

model = ResiTTA(model=backbone, **cfg.paras_adapt_model)
test_images = torch.rand(8, 3, 224, 224)

model(test_images)
```
