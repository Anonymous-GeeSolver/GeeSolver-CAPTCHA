# GeeSolver

This reposity is official implementation of "GeeSolver: A Generic, Efficient, and Effortless Solver with Self-Supervised Learning for Breaking Text Captchas".

## Overview of GeeSolver

<img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/Figs/GeeSolver-overview.png">

## Usage of text-based captchas

Text captchas have good user-friendliness, so many companies (e.g., Google, Microsoft, and Yandex) still use them on user login pages. After entering incorrect passwords multiple times, the user will be required to submit the results of text-based captchas. Detailed use cases and their security feature analysis are available on https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/tree/main/Cases. 

Since Alexa.com ends service on May 1, 2022, the complete list of the top-50 websites ranked by Alexa.com (including the corresponding captcha system) are available on https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/tree/main/AlexaList.

## Our insights into text-based captchas

We would like to better present our insights and corresponding designs through the following three questions.

**1. What hinders difficult-to-attack text captchas recognition?** 

We note that numerous difficult-to-attack captcha schemes that “damage” the standard font of characters, making each character diversified and confusing the solver.

**2. How do humans recognize these captchas?**

Humans can recognize each “damaged” character (e.g., occlusion, distortion) by its local information. Thus, we leverage MAE-style paradigm to train a ViT encoder, which is able to extract latent representation from the local information of the character for whole character reconstruction.

**3. What is the common characteristic of text captchas?**

The common characteristic of captcha images is that the text is arranged horizontally from left to right. Based on this characteristic, we design our sequence-based captcha decoder, which consists of three well-designed modules.

## The schematic illustration of GeeSolver

<img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/Figs/GeeSolver-model.png">

Our GeeSolver consists of a ViT encoder and a captcha decoder.

- [**ViT Encoder**] Numerous difficult-to-attack captcha schemes that “damage” the standard font of characters are similar to image masks. In this case, the MAE-based paradigm is very suitable for obtaining a ViT encoder (latent feature extractor) with the ability to infer characters from local information.

- [**Captcha Decoder**] Text-based captchas have the common characteristics that text is arranged horizontally from left to right, which inspired the design of a sophisticated sequence-based decoder to recognize captcha more efficiently.

## Dependency

```
torch=1.12.1
torchvision=0.13.1
timm=0.4.12
numpy=1.23.1
matplotlib=3.5.2
PIL=8.2.0
nltk=3.7
```

## Code

### 1. Pretrain
```
cd pretrain
python pretrain.py --dataset_name apple/ganji-1/microsoft/wikipedia/sina/weibo/yandex/google --num_layer 8 --mask_radio 0.6
```
The model will be saved every 100,000 iterations. For fast training, use `--restore 100000` in finetuning stage. For better effect, use `--restore 600000` in finetuning stage.

### 2. Finetune
```
cd finetuning
python finetuning.py --dataset_name apple/ganji-1/microsoft/wikipedia/sina/weibo/yandex/google --num_layer 8 --mask_radio 0.6 --restore 100000/600000
```

Note: When using `--dataset_name microsoft`, don't forget add `-–character 0123456789abcdefghijklmnopqrstuvwxyz-` in finetuning stage. Since Microsoft employs two-layer captchas , we use `-` as the delimiter between the upper layer and the lower layer.

## Results

| Scheme     | Example | Accuracy     |
| ----------- | -----| ------------ |
| Google     | <img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/google.jpg" width="120px" height="40px"> | 90.73%       |
| Yandex     | <img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/yandex.png" width="120px" height="40px"> | 92.87%       |
| Microsoft  | <img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/microsoft.jpg" width="120px" height="40px"> | 97.41%       |
| Wikiepdia  | <img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/wikipedia.png" width="120px" height="40px"> | 97.80%       |
| Weibo      | <img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/weibo.jpg" width="120px" height="40px"> | 92.47%       |
| Sina       | <img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/sina.png" width="120px" height="40px"> | 97.00%       |
| Apple      | <img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/apple.jpg" width="120px" height="40px"> | 95.60%       |
| Ganji      | <img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/ganji-1.png" width="120px" height="40px"> | 99.73%       |
