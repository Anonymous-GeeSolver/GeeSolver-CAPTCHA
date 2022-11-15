# GeeSolver

This reposity is official implementation of "GeeSolver: A Generic, Efficient, and Effortless Solver with Self-Supervised Learning for Breaking Text Captchas".

## Usage of text-based captchas

Text captchas have good user-friendliness, so many companies (e.g., Google, Microsoft, and Yandex) still use them on user login pages. After entering incorrect passwords multiple times, the user will be required to submit the results of text-based captchas. Detailed use cases are available on https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/tree/main/Cases (collected on Oct. 2022). 

Since Alexa.com ends service on May 1, 2022, we provide a copy of the complete list of the top-50 websites ranked by Alexa.com (including the corresponding captcha system) are available on https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/tree/main/AlexaList.

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

## Result

<img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/google.jpg" weight=200px>
| Scheme     | Example | Accuracy     |
| ----------- | -----| ------------ |
| Google     |<img src="https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/google.jpg" weight=200px>| 90.73%       |
| Yandex     | ![](https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/yandex.png) | 92.87%       |
| Microsoft  | ![](https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/microsoft.jpg) | 97.41%       |
| Wikiepdia  | ![](https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/wikipedia.png) | 97.80%       |
| Weibo      | ![](https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/weibo.jpg) | 92.47%       |
| Sina       | ![](https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/sina.png) | 97.00%       |
| Apple      | ![](https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/apple.jpg) | 95.60%       |
| Ganji      | ![](https://github.com/Anonymous-GeeSolver/GeeSolver-CAPTCHA/blob/main/images/ganji-1.png) | 99.73%       |
