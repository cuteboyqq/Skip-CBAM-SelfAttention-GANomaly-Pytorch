### Attention-Map-Guided-Two-stage-Anomaly-Detection-using-Hard-Augmentation-Pytorch
[(Back to menu)](#table-of-contents)

#### Anomaly Detection Network

implement from paper Attention Map-Guided Two-stage Anomaly Detection using Hard Augmentation https://arxiv.org/pdf/1805.08318.pdf , l just implement Attention Network
.

The Attention Network is able to generate Attention maps that show which part of region in image is anomaly and normal, 

and able to find anomaly images by loss value, it means if  loss value is greater than particular loss threshold, it will regard as anomaly image

but the acc is lower than skip-Attention GANomaly, so need ADGAN to further detect anomaly images.

below image ref. from paper https://arxiv.org/pdf/1805.08318.pdf

![image](https://user-images.githubusercontent.com/58428559/212247473-3b40b17c-c500-42df-a220-5066fa74d6dd.png)


### Implement-Issue

[(Back to menu)](#table-of-contents)

   -Generate fake image have some black images
   
   -Train attetion failed if the input_attn = 1, but succeed when input_attn=empty
   
   -The cutout augmentation  is not real, needs to further implement paper method
   
   -Maybe it is not easy to implement in tensorflow2 
   
   -The loss function is not same as paper, maybe result in false result

### Hard-Augmentation 
l just implement cutout augmgnetation...

[(Back to menu)](#table-of-contents)

Generator +  Discriminator model 


### Table of contents

<!-- After you have introduced your project, it is a good idea to add a **Table of contents** or **TOC** as **cool** people say it. This would make it easier for people to navigate through your README and find exactly what they are looking for.

Here is a sample TOC(*wow! such cool!*) that is actually the TOC for this README. -->

- [Attention-Map-Guided-Two-stage-Anomaly-Detection-using-Hard-Augmentation-Pytorch](#Attention-Map-Guided-Two-stage-Anomaly-Detection-using-Hard-Augmentation-Pytorch)
- [Implement-Issue](#Implement-Issue)
- [Hard-Augmentation](#Hard-Augmentation)
- [Requirement](#Requirement)
- [implement](#implement)
   - [SkipCBAM-AutoEncoder](#SkipCBAM-AutoEncoder)
   - [Self-Attention](#Self-Attention)
   - [AttentionNetwork](#AttentionNetwork)
- [Train-on-custom-dataset](#Train-on-custom-dataset)
- [Train](#Train)
- [Test](#Test)
- [Lose-value-distribution](#Lose-value-distribution)
- [Reference](#Reference)
   
### Requirement
```
pip install -r requirements.txt
```

### implement 
[(Back to menu)](#table-of-contents)

### SkipCBAM-AutoEncoder
[(Back to menu)](#table-of-contents)

1. implement skip-CBAM-GANomaly first, and then start adding self-Attention into skip-CBAM-GANomaly network

![CBAM-ori](https://user-images.githubusercontent.com/58428559/212244936-6fc7e821-f549-445d-85e7-d0bc6aaf9572.png)

### Self-Attention
[(Back to menu)](#table-of-contents)

below image is self-Attention network , ref. from paper https://arxiv.org/pdf/1805.08318.pdf

![image](https://user-images.githubusercontent.com/58428559/212248977-9d1689b4-b29c-4ff6-843d-b5ae95a55b07.png)



### AttentionNetwork
[(Back to menu)](#table-of-contents)
![CBAM](https://user-images.githubusercontent.com/58428559/212244779-9b757168-0ad9-4db2-8931-ddaaf776c38f.png)

### Train-on-custom-dataset
[(Back to menu)](#table-of-contents)

```
Custom Dataset
├── test
│   ├── 0.normal
│   │   └── normal_tst_img_0.png
│   │   └── normal_tst_img_1.png
│   │   ...
│   │   └── normal_tst_img_n.png
│   ├── 1.abnormal
│   │   └── abnormal_tst_img_0.png
│   │   └── abnormal_tst_img_1.png
│   │   ...
│   │   └── abnormal_tst_img_m.png
├── train
│   ├── 0.normal
│   │   └── normal_tst_img_0.png
│   │   └── normal_tst_img_1.png
│   │   ...
│   │   └── normal_tst_img_t.png


```

### Train
[(Back to menu)](#table-of-contents)
```
python train.py --img-dir "[train dataset dir]" --batch-size 64 --img-size 32 --epoch 20
```

![image](https://user-images.githubusercontent.com/58428559/210168476-2cb1d156-d373-4bcc-84f4-89ef64679728.png)



### Test
[(Back to menu)](#table-of-contents)
```
python test.py --nomal-dir "[test normal dataset dir]" --abnormal-dir "[test abnormal dataset dir]" --view-img --img-size 32
```


### Lose-value-distribution
[(Back to menu)](#table-of-contents)

Blue : normal dataset

Orange : abnormal dataset


![image](https://user-images.githubusercontent.com/58428559/210168535-682bd748-df50-4935-a2ef-f67ad9e3a313.png)

![image](https://user-images.githubusercontent.com/58428559/210168526-8c657772-35b3-4d9d-a8ee-cf81aadc919d.png)

![image](https://user-images.githubusercontent.com/58428559/210168496-76ade09d-28a1-4900-b68b-65be4d80496e.png)




### Reference 
[(Back to menu)](#table-of-contents)

GANomaly: Semi-Supervised Anomaly Detection via Adversarial Training

https://arxiv.org/abs/1805.06725

Skip-GANomaly: Skip Connected and Adversarially Trained Encoder-Decoder Anomaly Detection

https://arxiv.org/pdf/1901.08954.pdf

Attention Map-Guided Two-stage Anomaly Detection using Hard Augmentation

https://arxiv.org/pdf/1805.08318.pdf

