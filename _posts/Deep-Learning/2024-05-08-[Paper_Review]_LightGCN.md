---
title:  "[Paper Review] LightGCN: Simplifying and Powering Graph Convolution Network for Recommendation" 
 
categories:
  - Recom
  - Machine
  - Math
  - Seminar
 
tags:
  - Machine-Learning
  - Deep-Learning
  - Graph-Network
  - Graph-Neural-Network
  - Recommend-System
  - Discrete Mathematics

toc: true
toc_sticky: true
use_math: true

date: 2024-05-08
last_modified_at: 2024-05-09
---

가짜연구소(Pseudo Lab) 8기 "Deep Dive In GNN"의 논문 리뷰 자료를 동영상으로 녹화해 보았습니다.

하루 정도의 시간 동안 논문 리뷰 발표를 준비해서 부족한 점이 많았는데, 스터디 활동을 통해 부족한 점을 단번에 알 수 있게 되었던 것 같습니다.


<iframe width="560" height="315" src="https://www.youtube.com/embed/tAeD7FUBXdg?si=hrsOgjE0-9JqeK8V" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Part1

<iframe width="560" height="315" src="https://www.youtube.com/embed/hzRPqZ9HNY8?si=KtsYH0XjVR6aUEo2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Part2


리뷰 후 보완해야 할 점 (2024. May 9th)

- GNN에서의 Smoothness (Smoothing) 의 개념을 명확히 알아야 함

- LightGCN 논문의 Table 6에서 왜 Matrix Factorization 모델과 (Layer Combination이 없는) LightGCN-Single의 Smoothness를 비교했는가

- LightGCN이 기존 GCN, NGCF 대비 추천에 왜 더 뛰어난지, LightGCN 논문에서 가정했던 바에 대한 더 매끄러운 설명 필요



    오류나 틀린 부분이 있을 경우 언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다!

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
