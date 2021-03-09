## PyTorch Adversarial Attack Baselines for ImageNet, CIFAR10, and MNIST

> PyTorch adversarial attack baselines for ImageNet, CIFAR10, and MNIST (state-of-the-art attacks comparison)

* This repository provides simple PyTorch implementations for evaluating various adversarial attacks. 
* This repository shows state-of-the-art attack success rates for each dataset.
    * This repository utilizes attack libraries such as [Advertorch](https://github.com/BorealisAI/advertorch), [Foolbox](https://github.com/BorealisAI/advertorch), etc.
* If you have questions about this repository, please send an e-mail to me (dongbinna@postech.ac.kr) or make an issue.

### What does the distance metric mean?

* Generally, each pixel value is normalized between \[0, 1\].
* A perturbation with L0 norm of 1,000 could change 1,000 pixels (the number of changed pixels).
* A perturbation with L2 norm of 1.0 could change one pixel by 255, ten pixels by 80, 100 pixels by 25, or 1000 pixels by 8.
* A perturbation with Linf norm of 0.003922 could change all pixels by 1 (the maximum changeable amount of each pixel).
* A perturbation with MSE of 0.001 or lower generally seems imperceptible to humans.

### 1. ImageNet Dataset

* This repository provides a small ImageNet validation dataset of 1,000 classes.
    * This dataset has 5 images per class (total 5,000 images).
* This is a subset of the ImageNet validation dataset.
* The size of adversarial examples: 224 x 224 x 3 (150,528 parameters)
* The basic architecture: <b>ResNet-50</b> (top-1 accuracy: 76.06%)

#### 1) Linf FGSM (Untargeted)

* [Google Colab source code](/PyTorch_FGSM_Adversarial_Attack_using_ImageNet_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is normalized between \[0, 1\].

|Epsilon size|1/255|2/255|4/255|8/255|16/255|32/255|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|10.96%|6.34%|5.40%|6.86%|8.98%|7.36%|
|<b>Average L0 distance</b>|148600|148600|148600|148600|148600|148600|
|<b>Average L2 distance</b>|1.5113|3.0161|6.0128|11.9674|23.7250|46.5814|
|<b>Average MSE</b>|0.00001518|0.00006047|0.00024037|0.00095245|0.00374475|0.01444550|
|<b>Average Linf distance</b>|0.003922|0.007843|0.015686|0.031373|0.062745|0.125490|

#### 2) Linf PGD (Untargeted)

* [Google Colab source code](/PyTorch_Linf_PGD_Untargeted_Attack_using_ImageNet_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is normalized between \[0, 1\].
* PGD attack is the 7-step PGD attack.

|Epsilon size|1/255|2/255|4/255|8/255|16/255|32/255|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|0.56%|0.06%|0.02%|0.02%|0.00%|0.00%|
|<b>Average L0 distance</b>|148808|147740|147280|147590|147956|148511|
|<b>Average L2 distance</b>|1.1457|2.1242|4.0156|7.7791|15.2752|29.9894|
|<b>Average MSE</b>|0.00000874|0.00003002|0.00010719|0.00040217|0.00155080|0.00597913|
|<b>Average Linf distance</b>|0.003922|0.007843|0.015686|0.031373|0.062745|0.125490|

#### 3) L2 PGD (Untargeted)

* [Google Colab source code](/PyTorch_L2_PGD_Untargeted_Attack_using_ImageNet_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is normalized between \[0, 1\].
* PGD attack is the 7-step PGD attack.

|Epsilon size|0.25|0.5|1.0|2.0|4.0|8.0|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|23.56%|5.78%|0.76%|0.14%|0.08%|0.06%|
|<b>Average L0 distance</b>|149952|150033|150127|150197|150236|150262|
|<b>Average L2 distance</b>|0.25|0.5|1.0|2.0|4.0|8.0|
|<b>Average MSE</b>|0.00000041|0.00000166|0.00000664|0.00002657|0.00010629|0.00042517|
|<b>Average Linf distance</b>|0.009559|0.016910|0.029153|0.050194|0.088268|0.156057|

### 2. CIFAR10 Dataset

* The size of adversarial examples: 32 x 32 x 3 (3,072 parameters)
* The basic architecture: <b>ResNet-18</b> (top-1 accuracy: 95.28%)

#### 1) Linf FGSM (Untargeted)

* [Google Colab source code](/PyTorch_FGSM_Adversarial_Attack_using_CIFAR10_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is normalized between \[0, 1\].

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
* Each pixel (parameter) value is normalized between \[0, 1\].

|Epsilon size|1/255|2/255|4/255|8/255|16/255|32/255|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|98.86%|98.65%|98.19%|96.88%|91.80%|61.40%|
|<b>Average L0 distance</b>|459|459|459|459|459|459|
|<b>Average L2 distance</b>|0.0839|0.1671|0.3299|0.6554|1.3049|2.5937|
|<b>Average MSE</b>|0.00000901|0.00003569|0.00013916|0.00054924|0.00217703|0.00860155|
|<b>Average Linf distance</b>|0.003922|0.007843|0.015686|0.031373|0.062745|0.125490|
