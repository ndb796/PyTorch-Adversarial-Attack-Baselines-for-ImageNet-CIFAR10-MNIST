## PyTorch Adversarial Attack Baselines for ImageNet, CIFAR10, and MNIST

> PyTorch adversarial attack baselines for ImageNet, CIFAR10, and MNIST (state-of-the-art attacks comparison)

* This repository provides simple PyTorch implementations for evaluating various adversarial attacks. 
* This repository shows state-of-the-art attack success rates for each dataset.
    * This repository utilizes attack libraries such as [Advertorch](https://github.com/BorealisAI/advertorch), [Foolbox](https://github.com/BorealisAI/advertorch), etc.
* If you have questions about this repository, please send an e-mail to me (dongbinna@postech.ac.kr) or make an issue.

### 1. ImageNet Dataset

* This repository provides a small ImageNet validation dataset of 1,000 classes.
    * This dataset has 5 images per class (total 5,000 images).
* This is a subset of the ImageNet validation dataset.
* The size of adversarial examples: 224 x 224 x 3 (150,528 parameters)
* The basic architecture: <b>ResNet-50</b> (top-1 accuracy: 76.06%)

#### 1) Linf FGSM (Untargeted)

* [Google Colab source code](/PyTorch_FGSM_Adversarial_Attack_using_ImageNet_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is between \[0, 1\].

|Epsilon size|1/255|2/255|4/255|8/255|16/255|32/255|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|10.96%|6.34%|5.40%|6.86%|8.98%|7.36%|
|<b>Average L0 distance</b>|148600|148600|148600|148600|148600|148600|
|<b>Average L2 distance</b>|1.5113|3.0161|6.0128|11.9674|23.7250|46.5814|
|<b>Average MSE</b>|0.00001518|0.00006047|0.00024037|0.00095245|0.00374475|0.01444550|
|<b>Average Linf distance</b>|0.003922|0.007843|0.015686|0.031373|0.062745|0.125490|

#### 2) Linf PGD (Untargeted)

* [Google Colab source code]()
* Each pixel (parameter) value is between \[0, 1\].

|Epsilon size|1/255 (4-step)|1/255 (7-step)|2/255 (4-step)|2/255 (7-step)|4/255 (7-step)|
|-----------------|---|---|---|---|---|
|<b>Robust accuracy</b>|0.96%|0.52%|0.10%|0.06%|0.02%|
|<b>Average L0 distance</b>|145509|148809|142349|147741|147280|
|<b>Average L2 distance</b>|1.1729|1.1456|2.2163|2.1242|4.0154|
|<b>Average MSE</b>|0.00000915|0.00000874|0.00003265|0.00003002|0.00010718|
|<b>Average Linf distance</b>|0.003922|0.003922|0.007843|0.007843|0.015686|

### 2. CIFAR10 Dataset

* The size of adversarial examples: 32 x 32 x 3 (3,072 parameters)
* The basic architecture: <b>ResNet-18</b> (top-1 accuracy: 95.28%)

#### 1) Linf FGSM (Untargeted)

* [Google Colab source code](/PyTorch_FGSM_Adversarial_Attack_using_CIFAR10_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is between \[0, 1\].

|Epsilon size|1/255|2/255|4/255|8/255|16/255|32/255|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|67.40%|58.08%|52.53%|48.15%|35.29%|16.74%|
|<b>Average L0 distance</b>|3053|3053|3053|3053|3053|3053|
|<b>Average L2 distance</b>|0.2166|0.4328|0.8640|1.7232|3.4283|6.7710|
|<b>Average MSE</b>|0.00001529|0.00006098|0.00024307|0.00096716|0.00382864|0.01494123|
|<b>Average Linf distance</b>|0.003922|0.007843|0.015686|0.031373|0.062745|0.125490|

### 3. MNIST Dataset

* The size of adversarial examples: 28 x 28 x 1 (784 parameters)
* The basic architecture: <b>LeNet</b> (top-1 accuracy: 98.99%)

#### 1) Linf FGSM (Untargeted)

* [Google Colab source code](/PyTorch_FGSM_Adversarial_Attack_using_MNIST_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is between \[0, 1\].

|Epsilon size|1/255|2/255|4/255|8/255|16/255|32/255|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|98.86%|98.65%|98.19%|96.88%|91.80%|61.40%|
|<b>Average L0 distance</b>|459|459|459|459|459|459|
|<b>Average L2 distance</b>|0.0839|0.1671|0.3299|0.6554|1.3049|2.5937|
|<b>Average MSE</b>|0.00000901|0.00003569|0.00013916|0.00054924|0.00217703|0.00860155|
|<b>Average Linf distance</b>|0.003922|0.007843|0.015686|0.031373|0.062745|0.125490|
