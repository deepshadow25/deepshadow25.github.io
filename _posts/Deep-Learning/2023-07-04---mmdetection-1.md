---
title:  "Detectron2 다루어보기" 

categories:
  - CV

tags:
  - CV
  - Deep-Learning
  - Mask R-CNN

toc: true
toc_sticky: true

date: 2023-06-12
last_modified_at: 2023-06-23
---


# Detectron2란?

Facebook AI 연구팀에서 2019년에 발표한 pytorch 기반의 Object Detection과 Sementic Segmentation을 위한 CV 딥러닝 모듈이다.

[Detectron2 Official Github Webpage](https://github.com/facebookresearch/detectron2)

[Meta AI post](https://ai.facebook.com/blog/-detectron2-a-pytorch-based-modular-object-detection-library-/)

## Detectron2의 특징

기존의 Detectron1 모델을 업그레이드시킨 모델이라 할 수 있는 Detectron2는 Detectron1에 비해 더 많은 모델을 제공한다. 

Detectron1에서도 제공되던 Mask R-CNN, Fast R-CNN, RetinaNet, DensePose는 물론, Cascade R-CNN, Panoptic FPN (Feature Pyramid Network), Tensormask 그리고 FAIR에서 개발한 Mask R-CNN 모델 계열의 수많은 변형을 포함한 최신 객체 검출 알고리즘의 고품질 구현을 포함한다. 

이처럼 다양한 구현이 가능한 Detectron2에서는 기존의 객체 인식과 Instance Segmentation 뿐만 아니라, 의미에 따른 세분화 (Sementic Segmentation) 는 물론 Panoptic Segmentation (Instance Segmentation과 Sementic Segmentation의 중간 방식이라 한다.) 까지 해 볼 수 있다고 한다.

## Detectron2 구성

setup.py 파일을 이용해서 Detectron2를 사용하는 데 필요한 요소를 설치할 수 있다.

train.py 파일로 학습을 할 수 있는데, 이 때 명령어는  python train.py --type [폴더명] --iter [반복횟수]  와 같이 지정할 수 있다.

## Detectron2 사용해 보기




<br>

    

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
