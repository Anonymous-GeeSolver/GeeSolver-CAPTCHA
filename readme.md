# GEESOLVER

This reposity is official implementation of "GEESOLVER: A Generic, Efficient, and Effortless Solver with Self-Supervised Learning for Breaking Text Captchas".

## Usage of text captchas

Text captchas have good user-friendliness, so many companies (e.g., Google, Microsoft) still use them on user login pages. After entering incorrect passwords multiple times, the user will be required to submit the results of text-based captchas. Detailed use cases are available on https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/tree/main/Cases (collected on Oct. 2022). The complete Alexa list and the corresponding captcha schemes are available on https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/tree/main/AlexaList.

## Dataset
https://drive.google.com/file/d/1LVygsMH6nqPWkGLofXHT1cFXmieGRfu1/view?usp=share_link
```
unzip dataset.zip
```

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

### 1. pretrain
```
python pretrain.py --dataset_name apple/ganji-1/microsoft/wikipedia/sina/weibo/yandex/google --num_layer 8 --mask_radio 0.6
```

### 2. finetune
```
python finetuning.py --dataset_name apple/ganji-1/microsoft/wikipedia/sina/weibo/yandex/google --num_layer 8 --mask_radio 0.6 --restore 600000
```

## Result


| Scheme      | Accuracy    |
| ----------- | ----------- |
| Google      | 76.4%       |
| Microsoft   | 96.4%       |
| Yandex      | 90.4%       |
| Wikiepdia   | 98.5%       |
| Weibo       | 92.5%       |
| Sina        | 97.1%       |
| Apple       | 92.9%       |
| Ganji       | 99.4%       |
