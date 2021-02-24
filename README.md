# Description

Imagewoof is a subset of 10 classes from Imagenet that aren't so easy to classify. Link to the original dataset: https://github.com/fastai/imagenette

We used the provided "noisy_imagewoof.csv" that came with the dataset to split the train set into 50% labelled and 50% unlabelled (i.e. those that are marked as noisy in the CSV file).

We then investigated 3 different approaches for the classification of this noisy Imagewoof dataset using PyTorch:

1. Transfer learning (feature extraction): A pre-trained ResNet18 model was used with its last fully-connected layer replaced, while keeping the rest of parameters frozen. This model was trained on just the labelled images (i.e. 50% of the train set).
2. Transfer learning (finetuning): A pre-trained ResNet18 model was used with its last fully-connected layer replaced. This time, the hidden layers were also updated. Disciminative learning rates were applied with earlier layers having lower learning rates and later layers having higher learning rates. This model was also trained on just the labelled images.
3. Semi-supervised learning (MixMatch): The MixMatch algorithm (original paper: https://paperswithcode.com/paper/mixmatch-a-holistic-approach-to-semi) was implemented. This model made use of both the labelled and unlabelled images to perform semi-supervised learning. We trained the ResNet34 model without any pre-training.

Performance comparison:

| Method                        | Validation Accuracy |
|-------------------------------|---------------------|
| ResNet18 (feature extraction) | 93%                 |
| ResNet18 (finetuning)         | 93.5%               |
| MixMatch                      | 60%                 |

See "notebook.ipynb" for more details.
