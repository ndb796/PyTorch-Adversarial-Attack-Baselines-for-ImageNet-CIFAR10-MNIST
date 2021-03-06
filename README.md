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
* The basic architecture: <b>ResNet-50 (top-1 accuracy: 76.06%)</b>

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

#### 4) L2 CW (Untargeted)

* [Google Colab source code](/PyTorch_L2_Untargeted_CW_Attack_using_ImageNet_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is normalized between \[0, 1\].
* We set the binary search steps to 4.

|Number of iterations|100|
|-----------------|---|
|<b>Robust accuracy</b>|00.00%|
|<b>Average L0 distance</b>|148926|
|<b>Average L2 distance</b>|0.45|
|<b>Average MSE</b>|0.00000251|
|<b>Average Linf distance</b>|0.004477|

#### 5) L2 CW (Targeted)

* [Google Colab source code](/PyTorch_L2_Targeted_CW_Attack_using_ImageNet_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is normalized between \[0, 1\].
* We set the binary search steps to 4.
* We assign a random target label to each original image.
* The attack success rate only counts the case the adversarial example is classified as a target class.

|Number of iterations|100|
|-----------------|---|
|<b>Attack success rate</b>|99.92%|
|<b>Average L0 distance</b>|148926|
|<b>Average L2 distance</b>|0.70|
|<b>Average MSE</b>|0.00000382|
|<b>Average Linf distance</b>|0.025385|

#### 6) Boundary Attack (Untargeted)

* [Google Colab source code](/PyTorch_Untargeted_Boundary_Attack_using_ImageNet_Images.ipynb)
* The Foolbox provides a Boundary Attack implementation.
* Each pixel (parameter) value is normalized between \[0, 1\].
* The basic untargeted method includes Blended Uniform Noise Attack as a default for the initialization.
    * This attack finds a noise that is not classified as a original class.
* Boundary Attack is always successful because the result images are always adversarial.

|Number of iterations|100|500|1000|
|-----------------|---|---|---|
|<b>Robust accuracy</b>|00.00%|00.00%|00.00%|
|<b>Average L0 distance</b>|114484|114372|117345|
|<b>Average L2 distance</b>|36.31|33.34|30.97|
|<b>Average MSE</b>|0.01487032|0.01322446|0.01143493|
|<b>Average Linf distance</b>|0.232628|0.215504|0.203864|

#### 7) Boundary Attack (Targeted)

* [Google Colab source code](/PyTorch_Targeted_Boundary_Attack_using_ImageNet_Images.ipynb)
* The Foolbox provides a Boundary Attack implementation.
* Each pixel (parameter) value is normalized between \[0, 1\].
* We assign a random target image and label to each original image.
* The attack success rate only counts the case the adversarial example is classified as a target class.
* Boundary Attack is always successful because the result images are always adversarial.

|Number of iterations|100|500|1000|3000|5000|
|-----------------|---|---|---|---|---|
|<b>Attack success rate</b>|100.00%|100.00%|100.00%|100.00%|100.00%|
|<b>Average L0 distance</b>|150515|150517|150516|150512|150521|
|<b>Average L2 distance</b>|85.19|76.85|74.54|55.04|41.63|
|<b>Average MSE</b>|0.05373115|0.04324187|0.04044148|0.02298234|0.01335199|
|<b>Average Linf distance</b>|0.585978|0.534655|0.526516|0.416445|0.337554|

### 2. CIFAR10 Dataset

* The size of adversarial examples: 32 x 32 x 3 (3,072 parameters)
* The basic architecture: <b>ResNet-18 (top-1 accuracy: 95.28%)</b>

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

#### 2) Linf PGD (Untargeted)

* [Google Colab source code](/PyTorch_Linf_PGD_Untargeted_Attack_using_CIFAR10_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is normalized between \[0, 1\].
* PGD attack is the 7-step PGD attack.

|Epsilon size|1/255|2/255|4/255|8/255|16/255|32/255|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|51.26%|26.75%|8.28%|1.04%|0.08%|0.00%|
|<b>Average L0 distance</b>|3047|3011|3001|3015|3029|3042|
|<b>Average L2 distance</b>|0.1867|0.3461|0.6319|1.1733|2.2501|4.4030|
|<b>Average MSE</b>|0.00001362|0.00003906|0.00013022|0.00044856|0.00164901|0.00631511|
|<b>Average Linf distance</b>|0.003922|0.007843|0.015686|0.031373|0.062745|0.125490|

#### 3) L2 PGD (Untargeted)

* [Google Colab source code](/PyTorch_L2_PGD_Untargeted_Attack_using_CIFAR10_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is normalized between \[0, 1\].
* PGD attack is the 7-step PGD attack.

|Epsilon size|0.25|0.5|1.0|2.0|4.0|8.0|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|31.74%|13.56%|2.38%|0.13%|0.00%|0.00%|
|<b>Average L0 distance</b>|3066|3067|3068|3069|3069|3069|
|<b>Average L2 distance</b>|0.25|0.5|1.0|2.0|4.0|8.0|
|<b>Average MSE</b>|0.00002035|0.00008138|0.00032551|0.00130208|0.00520833|0.02083333|
|<b>Average Linf distance</b>|0.025261|0.043822|0.077334|0.141376|0.267958|0.523127|

#### 4) Boundary Attack (Targeted)

* [Google Colab source code](/PyTorch_Targeted_Boundary_Attack_using_CIFAR10_Images.ipynb)
* The Foolbox provides a Boundary Attack implementation.
* Each pixel (parameter) value is normalized between \[0, 1\].
* We assign a random target image and label to each original image.
* The attack success rate only counts the case the adversarial example is classified as a target class.
* Boundary Attack is always successful because the result images are always adversarial.

|Number of iterations|100|500|1000|3000|5000|10000|
|-----------------|---|---|---|---|---|---|
|<b>Attack success rate</b>|100.00%|100.00%|100.00%|100.00%|100.00%|100.00%|
|<b>Average L0 distance</b>|3071|3071|3071|3059|3062|3056|
|<b>Average L2 distance</b>|9.63|7.36|6.02|2.17|1.08|0.42|
|<b>Average MSE</b>|0.03306946|0.01989065|0.01330044|0.00196387|0.00054490|0.00008164|
|<b>Average Linf distance</b>|0.440098|0.344276|0.286082|0.110370|0.061091|0.032690|

#### 5) HopSkipJump Attack (Targeted)

* [Google Colab source code](/PyTorch_Targeted_HopSkipJump_Attack_using_CIFAR10_Images.ipynb)
* The Foolbox provides a HopSkipJump Attack implementation.
* Each pixel (parameter) value is normalized between \[0, 1\].
* We assign a random target image and label to each original image.
* The attack success rate only counts the case the adversarial example is classified as a target class.
* HopSkipJump Attack is always successful because the result images are always adversarial.
* Each iteration includes 100 gradient approximation steps.

|Number of iterations|10|30|50|
|-----------------|---|---|---|
|<b>Attack success rate</b>|100.00%|100.00%|100.00%|
|<b>Average L0 distance</b>|3065|3059|3059|
|<b>Average L2 distance</b>|3.33|1.79|1.32|
|<b>Average MSE</b>|0.00402476|0.00115264|0.00062992|
|<b>Average Linf distance</b>|0.166263|0.093042|0.070633|

### 3. MNIST Dataset

* The size of adversarial examples: 28 x 28 x 1 (784 parameters)
* The basic architecture: <b>LeNet (top-1 accuracy: 98.99%)</b>

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

#### 2) Linf PGD (Untargeted)

* [Google Colab source code](/PyTorch_Linf_PGD_Untargeted_Attack_using_MNIST_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is normalized between \[0, 1\].
* PGD attack is the 7-step PGD attack.

|Epsilon size|1/255|2/255|4/255|8/255|16/255|32/255|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|98.86%|98.65%|98.16%|96.73%|90.79%|46.27%|
|<b>Average L0 distance</b>|495|496|499|503|509|518|
|<b>Average L2 distance</b>|0.0830|0.1650|0.3258|0.6460|1.2826|2.5349|
|<b>Average MSE</b>|0.00000881|0.00003484|0.00013578|0.00053386|0.00210479|0.00822191|
|<b>Average Linf distance</b>|0.003922|0.007843|0.015686|0.031373|0.062745|0.125490|

#### 3) L2 PGD (Untargeted)

* [Google Colab source code](/PyTorch_L2_PGD_Untargeted_Attack_using_MNIST_Images.ipynb)
* Advertorch and Foolbox show almost the same results.
* Each pixel (parameter) value is normalized between \[0, 1\].
* PGD attack is the 7-step PGD attack.

|Epsilon size|0.25|0.5|1.0|2.0|4.0|8.0|
|-----------------|---|---|---|---|---|---|
|<b>Robust accuracy</b>|97.91%|96.06%|86.44%|26.70%|0.10%|0.00%|
|<b>Average L0 distance</b>|672|672|672|672|670|673|
|<b>Average L2 distance</b>|0.25|0.5|1.0|2.0|4.0|8.0|
|<b>Average MSE</b>|0.00007970|0.00031879|0.00127532|0.00510183|0.02040816|0.08163265|
|<b>Average Linf distance</b>|0.045673|0.092980|0.190897|0.391071|0.752917|0.914406|
