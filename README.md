# 감시정찰을 위한 딥러닝 기반 표적 인식 알고리즘 연구(2022.04-2022.11)
* 2022 밀리테크 챌린지 우수상(한국과학기술원 총장상)

* Unadversarial Examples: Designing Objects for Robust Vision
*Hadi Salman\*, Andrew Ilyas\*, Logan Engstrom\*, Sai Vemprala, Aleksander Madry, Ashish Kapoor* <br>
[**Paper**](https://arxiv.org/abs/2012.12235) <br>
[**Blogpost (MSR)**](https://www.microsoft.com/en-us/research/blog/unadversarial-examples-designing-objects-for-robust-vision/) <br> 


## 설정(Colab에서 진행)
0. Google Drive 연결 및 임의의 Workspace 폴더 생성

1. %cd '/workspace 경로/'

2.  Clone repo: `!git clone https://github.com/microsoft/unadversarial.git`

3.  Install dependencies:
    `!pip install -r requirement.txt`


## Generating unadversarial examples for CIFAR10

1- Download a pretrained CIFAR10 models
  ```
  !mkdir pretrained-models & 
  !wget -O pretrained-models/cifar_resnet50.ckpt "https://www.dropbox.com/s/yhpp4yws7sgi6lj/cifar_nat.pt?raw=1"
  ```
  
2- Run
  ```
  python -m src.main \
        --out-dir OUT_DIR \
        --exp-name demo \
        --dataset cifar \
        --data /tmp \
        --arch resnet50 \
        --model-path pretrained-models/cifar_resnet50.ckpt \
        --patch-size 10 \
        --patch-lr 0.001 \
        --training-mode booster \
        --epochs 30 \
        --adv-train 0
  ```
`outdir/demo/save/`에서 이미지 확인

3- evaluate the pretrained model on a boosted CIFAR10-C dataset
  ```
  python -m src.evaluate_corruptions \
        --out-dir OUT_DIR \
        --exp-name demo \
        --model-path OUT_DIR/demo/checkpoint.pt.best \
        --args-from-store data,dataset,arch,patch_size
  ```    

## Extract 2D Patch
`src/extract_2Dpatch.py`에서 주석달린 부분 경로 설정해주고 patch size 지정, class 지정해주면 colab에서 이미지 생성
(현재 경로 src 폴더)
```
!python extract_2Dpatch.py
```

### Dataset(Classification에 사용할 데이터셋)
https://drive.google.com/drive/folders/15ctZhzgMUtBvl3ji6nOq3GhkRktwRooS?usp=sharing
