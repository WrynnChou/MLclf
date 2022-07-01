![mini-ImageNet Logo](https://github.com/tiger2017/MLclf/blob/master/mini-imagenet.png)
![mini-ImageNet Logo](https://github.com/tiger2017/MLclf/blob/master/tiny-imagenet.png)
## The project Machine Learning CLassiFication (MLclf) 

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/python-3.6-blue.svg)](https://www.python.org/)
[![PyPI](https://img.shields.io/pypi/v/mlclf)](https://pypi.org/project/mlclf/)
[![Downloads](https://static.pepy.tech/personalized-badge/mlclf?period=total&units=international_system&left_color=blue&right_color=green&left_text=Downloads)](https://pepy.tech/project/mlclf)

#### The project is to transform the mini-imagenet dataset which is initially created for the few-shot learning (other datasets, e.g. tiny-imagenet, will come soon...) to the format that fit the classical classification task. You can also use this package to download and obtain the raw data of the mini-imagenet dataset (for few-shot learning tasks).
#### The original dataset includes totally 100 classes, but due to its intention to meta-learning or few-shot learning, the train/validatioin/test dataset contains different classes. They have respectively 64/16/20 classes.
##

#### In order to make the mini-imagenet dataset fit the format requirement for the classical classification task. MLclf made a proper transformation (recombination and splitting) of the original mini-imagenet dataset.
#### The transformed dataset is divided into train, validation and test dataset, each dataset of which includes 100 classes. Each image has the size 84x84 pixels with 3 channels.
###

The MLclf package can be found at: https://github.com/tiger2017/MLclf 
or  
https://pypi.org/project/MLclf/

Welcome to create an issue to the repository of MLclf on GitHub, and I will add more datasets loading functions based on the issues.


The mini-imagenet source data can be accessed from: https://deepai.org/dataset/imagenet
###
##### How to install MLclf package:
```angular2html
pip install MLclf
```

##### How to use this package:

```python
from MLclf import MLclf
import torch
import torchvision.transforms as transforms

# Download the original mini-imagenet data:
MLclf.miniimagenet_download(Download=True)


# Transform the original data into the format that fits the task for classification:
# Note: If you want to keep the data format as the same as that for the meta-learning or few-shot learning (original format), just set ratio_train=0.64, ratio_val=0.16, shuffle=False.

transform = transforms.Compose([transforms.ToTensor(), transforms.Normalize((0.5, 0.5, 0.5), (0.5, 0.5, 0.5))])
train_dataset, validation_dataset, test_dataset = MLclf.miniimagenet_clf_dataset(ratio_train=0.6, ratio_val=0.2, seed_value=None, shuffle=True, transform=transform, save_clf_data=True)

# The dataset can be transformed to dataloader via torch: 

train_loader = torch.utils.data.DataLoader(dataset=train_dataset, batch_size=128, shuffle=True, num_workers=0)


# You can check the corresponding relations between labels and label_marks of the image data:
# (Note: The relations can be obtained after MLclf.miniimagenet_clf_dataset is called, otherwise they will be returned as None instead.)

labels_to_marks = MLclf.labels_to_marks
marks_to_labels = MLclf.marks_to_labels
```
####

You can also obtain the raw data from the downloaded pkl files:
```python
from MLclf import MLclf

# The raw data of mini-imagenet can be also obtained via the function below:

data_raw_train, data_raw_val, data_raw_test = MLclf.miniimagenet_data_raw()
```

## Here is a random joke that'll make you laugh!
![Jokes Card](https://readme-jokes.vercel.app/api)