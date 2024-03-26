---
title:  "CS224W Lecture 6 : Graph Neural Network" 
 
categories:
  - Recom
  - Machine
 
tags:
  - Machine-Learning
  - Deep-Learning
  - Graph-Network
  - Graph-Neural-Network
  - Recommend-System

toc: true
toc_sticky: true

date: 2024-03-24
last_modified_at: 2024-03-27
---

[CS224W Lecture Playlist on Youtube](https://www.youtube.com/playlist?list=PLoROMvodv4rPLKxIpqhjhPgdQy7imNkDn)

# Graph Neural Networks

### Node Embeddings 복습하기

직관 : $d$차원 임베딩에 노드를 매핑하는 것 
—> 그래프 내 유사한 노드가 가깝게 임베딩되게 하는 것과 유사하다.

—> 그렇다면 어떻게 mapping 함수 $f$를 학습시킬 것인가?

- Encoder-Decoder 모델에서 : node embedding의 목표는 similarity $(u, v) \approx {z}_v^T {z}_u$ (내적)
- similarity $(u.v)$, ENC(u), ENC(v) → 정의해야 함
    - Encoder : ENC(v) = ${z}_v$ (for d차원 임베딩, $v$는 주어진 그래프의 노드)
    - Decoder (Similarity function) : (임베딩된) 벡터 공간에서의 관계를 원래 네트워크의 관계에 역으로 매핑.

### 얕은(“Shallow”) Encoding 복습하기

Encoder는 embedding-lookup하는 역할만 함

![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/4e13c145-839a-414f-9cf2-dc8f067618a2)

#### Shallow Encoders의 한계점

- $O(|V|)$ parameters are needed : 복잡도가 크다
    - 모든 노드가 각자의 임베딩을 갖고 있다 (공유 x)
    - 학습해야 하는 파라미터 수도 $|V|$ (차원 d 와 노드 개수의 곱) 에 비례
    - 각각 계산해야 하므로, 복잡도가 클 수밖에 없다.
- “Transductive”하다
    - 학습 중에 못 본 노드에 대한 임베딩을 만들 수 없다 (동적 그래프에 대한 임베딩을 생성할 수 없다)
- node feature를 사용하지 않는다

shallow encoder를 다룰 때, 6강에서 deep encoder를 다룬다고 하였다

## Deep Graph Encoders

GNN 기반의 “Deep” 한 방법 적용

ENC(v) = 그래프구조 기반의 / 다층구조 / 비선형 변환

입력값으로 “그래프 구조” 를 사용하며

출력값으로 노드 임베딩과, (sub)그래프에 대한 임베딩을 얻는다.

![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/29226d71-0824-439d-846d-08807f84c77a)

- Deep Encoder, GNN을 이용하여 해결하려는 문제
    - Node Classification : 주어진 노드의 타입 예측
    - Link Prediction : 두 노드가 연결되었는지 예측
    - Community Detection : 빽뺵하게 밀집된 노드 군집(Clusters)을 식별한다
    - Network Similarity : 두 (sub)네트워크가 얼마나 유사한지 확인한다.
    
    …
    

### Modern ML Toolbox

![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/e76fe5bd-64ef-40a9-98c4-0b48e3231bd2)

- 입력되는 이미지나 텍스트, 음성을 간단한 격자나 연결구조 그래프로, ML 역시 GNN의 일종으로 볼 수 있다

그러나 실제 네트워크는 훨씬 복잡하기 때문에 매우 어렵다

- 임의의 사이즈와 복잡한 위상수학적 구조 (격자처럼 친절한 구조가 아니다!)
- 고정된 노드가 딱히 없다
- 종종 동적이거나, 멀티모달 feature가 등장하기도 한다.
    - 멀티모달 : 이미지 + 동영상 / 음성 + 텍스트 등과 같이 여러 형태의 데이터가 동시에 입력되는 형태


# Basics of Deep Learning

## 최적화를 위한 ML

### 지도학습

input $x$에 대하여 (정답이 있는) 라벨 $y$를 예측하는 것

$x$로 가능한 것은 숫자, 시퀀스(자연어, 음성), 행렬(이미지), 그래프(노드, 엣지 잠재성을 갖는) 등이 있다.

지도학습의 task는 크게 분류(Classification)과 회귀(Regression)으로 나뉜다.

## 최적화 문제의 목표

최적화 문제의 목적함수는 아래와 같이 정의된다.

$$
\min_{\Theta} \mathcal{L}(y, f(x))
$$

$\Theta$ : 최적화시킬 파라미터의 집합

shallow encoder에서는 $\Theta = \{Z\}$

$\mathcal{L}$ : Loss function (L2, L1 등…)

목표 : loss (cost) 가 낮은 함수, 가설(hypothesis)을 찾는다

### Loss Function의 예

분류 문제에서는 보통 Loss function을 Cross Entropy Error (CE)로 사용한다. (* 회귀 문제는 Mean Square Error (MSE)를 사용)

- 라벨 y를 one-hot encoding한 categorical vector라 하자
    
    $y = (0, 0, 1,0,0)$  ( y는 클래스 “3” 에 있다.)
    
- $f(x) =$ Softmax $(g(x))$
- 이를 계산하면 $f(x) = (0.1, 0.3,0.4,0.1,0.1)$
- CE(y, f(x)) = $-{\sum}_{i=1}^C (y_i \log f(x)_i)$
    - log의 밑은 자연상수 $e = 2.718...$
- 모든 학습이 끝난 후의 Total Loss는 다음과 같다
    - $L = \sum_{(x,y)\in {T}}$ CE $(y, f(x))$
    - $\mathcal{T}$ : 학습에 사용된 모든 데이터와 라벨쌍 집합

### 목적함수의 최적화 - 기울기 벡터

Gradient (기울기) vector : 가장 빠르게 증가하는 방향과 비율…

$$
\nabla_{\Theta}\mathcal{L} = (\frac{\partial \mathcal{L}}{\partial \Theta_1}, \frac{\partial \mathcal{L}}{\partial \Theta_2}, ...)
$$

각 파라미터 $\Theta_1, \Theta_2, ...$ 에 대해 편미분

## 신경망 함수와 기울기

### 기울기 감소법(경사하강법.Gradient Descent)

우리는 증가가 아닌, “감소” 에 관심있다 (목적함수의 최솟값이 우리의 목표다)

→ 기울기의 역방향 고려 

: $\Theta <- \Theta - \eta \frac{\partial \mathcal{L}}{\partial \Theta}$를 반복하여 $\Theta$ 업데이트

학습률 (LR) $\eta$ : 기울기의 감소 정도를 결정하는 hyperparameter

LR Scheduling 기법으로 조정할 수 있다.

### **1.2.2 SGD (Stochastic Gradient Descent)**

기존 GD의 문제점 (급격한 감소로 인한 데이터 누락, 소실 등) 을 방지하기 위한 한 방법

모든 단계에서, 데이터셋의 부분집합을 포함하는 서로 다른 minibatch $\mathcal{B}$를 정의

- Batch, Epoch, Iteration 관련 개념
    - Minibatch : 데이터셋을 Batch size로 쪼갠 것
    - Iteration : (minibatch 단위로) 1회 학습한 것
    - Epoch : 전체 데이터셋을 한번 학습한 것
    
    예를 들어, 총 데이터가 64개, batch size가 4이면
    
    iteration = 64 / 4 = 16번 학습
    
    1 epoch = 64/(batch size) = 16 iteration
    

Adam, Adagrad, Adadelta, RMSprop 등이 SGD를 향상시킨 방법.

### Neural Network Function

목적함수는 아래와 같다

$$
\min_{\Theta} \mathcal{L}(y, f(x))
$$

딥러닝에서 함수 $\mathcal{f}$는 매우 복잡하다

- $f(x) = W\cdot x$, $\Theta = \{W\}$
- $f$가 scalar로 환원될 경우, 가중치 W는 학습 가능한 벡터가 된다
    
    $\nabla_{W}f = (\frac{\partial f}{\partial W_1}, \frac{\partial f}{\partial W_2}, \frac{\partial f}{\partial W_3}, ...)$
    
    
- $f$가 vector로 환원될 경우, 가중치 W는 가중치 벡터가 된다
    - 이를 $f$의 Jacobian Matrix라 한다.
    - (Transpose된 벡터)
    
    $\nabla_{W}f = W^T$
    

## 역전파 알고리즘과 비선형성

### 역전파 알고리즘

- $f(x) = W_2(W_1 x)$, $\Theta = \{W_1, W_2\}$

미적분에서의 chain rule을 적용하게 되면 다음과 같은 연산이 된다.

$\nabla_x f = \frac{\partial f}{\partial (W_1 x)} \frac{\partial (W_1 x)}{\partial x}$

역전파 알고리즘 또한, 이러한 chain rule을 적용하여 $\Theta$에 대한 $\mathcal{L}$을 구하는 것이다.

5강의 tree 구조에서 잎에서 뿌리로 거꾸로 가던 것 처럼. 출력값에서 입력값쪽으로 역으로 전파되는 것 처럼 간주하여, loss에서부터 gradient를 구해나가며, 오차를 줄여나가는 방법이라 할 수 있다.

### 역전파 알고리즘의 예시

![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/8b9aa5c3-d7b1-4b64-ab67-1edc1d980217)

위 그림과 같은 2층 선형 네트워크 구조를 예로 들면

- $f(x) = g(h(x)) = W_2(W_1 x)$
- $\mathcal{L} = \sum_{(x,y)\in \mathcal{T}}$ $||(y, f(x))||_2$ (L2 loss, minibatch $\mathcal{B}$에서)
- 역전파 알고리즘을 바탕으로, loss에서 시작하여 gradient를 구할 수 있다
    
    $\Theta = \{W_1, W_2\}$
    

$\frac{\partial \mathcal{L}}{\partial W_2 } =\frac{\partial \mathcal{L}}{\partial f} \frac{\partial f}{\partial W_2 } , \frac{\partial \mathcal{L}}{\partial W_1 } =\frac{\partial \mathcal{L}}{\partial f} \frac{\partial f}{\partial W_2 }\frac{\partial W_2}{\partial W_1 }$

### 비선형성

$f(x)$는 여전히 선형 함수이다. 비선형성을 추가시킬 요소가 필요하다. 이러한 요소는 “활성화 함수(Activate Function)”라 불리며, 대표적으로 ReLU와 Sigmoid가 있다.

- ReLU = $\max(x,0)$
- Sigmoid $\sigma(x) = \frac{1}{1+\exp(-x)}$

이외에도 여러 함수들이 있다.

### 다층 퍼셉트론 (Multi-Layer Perceptron, MLP)

다층 퍼셉트론의 각 층은 선형 변환과 비선형성을 조합한 것이다.

활성화 함수를 sigmoid로 하였을 경우 다음 수식을 만족한다

$x^{l+1} =  \sigma(W_l x^{(l)} + b^l )$

- $W_l$은 l층에서 $l+1$층으로 변환할 때 가중치 행렬이다
- $b^l$은 l 레이어의 편향(bias)로 x에 더하면 됨


# Deep Learning for Graphs

## Fundamentals

### setup

그래프 G를 가정

- V : vertex set (노드 집합)
- A : 인접행렬 (이진으로 가정)
- $X \in \mathbb{R}^{m \times |V|}$ : node features의 행렬
- v : 집합 V에 속하는 노드
    - $N(v)$ : v 이웃 노드들의 집합

node features의 예

- SNS : 사용자 프로필, 사용자 이미지, …
- 생물 네트워크 : 유전자 표현형, 유전자 기본 정보, …
- 그래프 데이터셋 내에 node feature가 없을 때는
    - 지시자 벡터 (노드의 one-hot encoding)
    - 상수 1의 벡터 : $[1,1,...,1]$

### A Naive Approach

- 인접행렬과 feature를 결합하고, deep neural net에 제공
    - Shallow Encoder와 유사한 문제들이 발생
        - $O(|V|)$ parameters
        - 다른 사이즈의 그래프에 적용 안 됨
        - 노드 순서에 민감

## Local Network Neighborhoods

### Convolutional Networks vs Graph

- CNN
    
    ![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/c028f2c3-1f00-4253-a47e-9f6f583c3b1c)
    
    이미지의 학습에 주로 사용되는 합성곱 신경망 (CNN) 을 그래프 개념으로 바꾸어 생각해 볼 수 있다…
    
    목표 - 합성곱을 통해 특성을 뽑아내는 것…
    
- Graph
    
    ![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/88e57224-fb4f-49f7-9d7e-5cad7994c794)
    
    실제 그래프는 형태가 부정확할 뿐만 아니라, 순서도 불변이어서… CNN처럼 적용하기 힘들다
    
    ![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/a82aeede-4b4e-42d3-90e8-c5c9005999ec)
    
    또한 그래프는 node, edge(link) 관계를 따져야 하니 CNN의 아이디어를 그대로 적용할 수 없다.
    

### Graph Convolutional Networks

GCN의 아이디어 : 노드의 이웃(Neighborhood)을 계산할 그래프로 정의

![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/88e57224-fb4f-49f7-9d7e-5cad7994c794)

##  Aggregate Neighbors

1. 핵심 아이디어 
    
    로컬 네트워크 이웃 기반으로 노드 임베딩 생성
    

직관 : 이웃한 노드들로부터 받는 노드 집합체의 정보를 얻을 때 신경망을 쓰자 (아래 그림에서 여러 노드들에 연결된 사각형 부분)


![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/4720d0c5-deed-454a-8fa2-02ba5cf7d705)


직관 : Network neighborhood를 “Computation Graph”로 정의한다
    
  ![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/a082c6ed-4df9-45ef-b72c-01c245376fb0)
    

노드마다 연결된 링크가 다르기 때문에, Network Neighborhood (Compuation Graph)도 다를 수 밖에 없다. *CNN에 일정한 합성곱이 유지되는 것과 다른데.. GCN은 패딩과 같이 오차를 보정할 요소가 없어도 되는걸까?*

## Stacking Multiple Layers

### Deep Model : Many Layers

임의의 깊이에 대해 모델을 적용할 수 있다

- 노드들은 각 층에서 임베딩을 가진다
- Layer-0에서의 노드 $u$의 임베딩은 입력값 $x_u$다.
- Layer-k에서의 임베딩은 *K hop (K 단계?)* 멀리 떨어진 노드에서 정보를 얻은 것으로 볼 수 있다.

#### Neighborhood Aggregation

- 주요 구별점 
여러 레이어를 거쳐온 서로 다른 정보를 어떻게 조합하고 다음 레이어의 정보로 보낼 수 있는가?

![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/29b905f4-1afe-4783-9e84-4946b4e5d5af)

- 기본 접근법
이웃들로부터 정보를 종합하고, 이를 신경망에 적용

![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/1930c858-4715-4bea-b990-492d7442c501)

#### The Math - Deep Encoder

정보를 종합하고 신경망에 적용할 때의 수식은 다음과 같다

$\mathbf{h}_v^0 = \mathbf{x}_v$ : 초기 0층(입력 레이어)의 임베딩은 node feature와 같다

$h_v^{l+1} = \sigma(W_l \sum_{u\in N(v)} \frac{h_u^{(l)}}{|N(v)|} + B_l h_v^{l}), \forall  l \in \{ 0, ..., L-1\}$

$z_v = h_v^{(L)}$

$\sigma$ : 활성화함수 (비선형)

$\sum_{u\in N(v)} \frac{\mathbf{h}_u^{(l)}}{|N(v)|}$ : 이웃 노드의 벡터 임베딩 평균

$h_v^{l}$ : 노드 v의 레이어 l에서의 임베딩

$L$ : 전체 레이어 수 (층수)

모델을 학습시키려면?? 

—> 임베딩에서의 loss function부터 정의해야 한다.

학습에 사용되는 (학습할 수 있는) 파라미터는 $l$ 레이어에서의 가중치 행렬 $W_l$ 와, $l$ 레이어의 정보를 변환하는 데 쓰이는 행렬 $B_l$ 뿐이다.

#### Matrix Formulation

많은 이웃 노드의 Aggregations는 (sparse) 행렬 연산으로 효율적인 표현이 가능하다.

![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/0be5b115-c9bd-40f3-a1ce-bb151cbfc651)

- $H^{(l)} = [h_1^{(l)}, ... , h_{|V|}^{(l)}]^T$
*l*번째 레이어의 모든 노드에 대한 vector를 병합한 행렬
- *A* : 인접행렬
    
    $AH^{(l)}$을 통해 *v*노드의 모든 이웃 노드의 벡터의 합을 구할 수 있다.
    
- $D$ : v노드의 이웃 노드의 수가 담긴 대각행렬
$D^{-1}=\frac{1}{|N(v)|}$ 로, 이웃 노드 개수의 역수가 된다.
    
    ![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/669399cd-61d9-4f07-98c8-f2f23dd5c694)
    
- $\tilde{A} = D^{-1}A$ 는 sparse한 행렬이기 때문에 sparse matrix multiplication을 도입해 효과적인 연산이 가능하다.
- 빨간색은 이웃 노드의 정보를 모으는 부분
파란색은 본인 노드의 정보를 변형하는 부분이다.

### Training

지도 학습 - 목적함수의 loss를 계산하여, 이를 최소화하도록 맞추어가면 됨

비지도 학습 - 그래프 구조를 관찰자로 사용

#### 비지도 학습

비슷한 노드는 비슷한 임베딩을 가진다

$$
\mathcal{L} = \sum_{z_u,z_v} \mathbf{CE}(y_{u,v},\mathbf{DEC}(z_u,z_v))
$$

$y_{u,v}=1$일 때 노드 u와 v는 similar하다 한다.

CE : Cross Entropy

DEC : Decoder (내적으로 계산)

노드 유사도는 어떤 걸 이용해도 좋다 (3강 참조)

Random Walks (node2vec, DeepWalk, struc2vec ….)

Matrix Factorization

Node Proximity in the graph

#### 지도 학습

직접적으로 학습 과정을 감독하면서 학습 (노드 분류 문제가 특히 지도학습에 해당)

- Cross Entropy를 사용하였을 때 loss function은 다음과 같다.

![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/794866b1-3038-4747-b40e-ad4b4fb4c9b3)

### Model Design

1. 이웃 노드들에서 정보를 취합할 때 사용할 함수를 정한다
2. 임베딩에서 사용할 loss 함수를 정한다
3. 노드 집합을 학습시킨다
    1. compute graphs 하나하나를 하나의 batch로 생각하여 학습시킨다.
4. 필요한 만큼 노드들에 대한 임베딩을 생성한다.
    1. 학습하지 않을 때도 임베딩을 생성할 수 있다.

### Inductive Capability

모든 노드에서 같은 aggrgation parameters는 공유된다

![image](https://github.com/deepshadow25/CS224W---Machine-Learning-with-Graphs/assets/115054681/fa5d6543-eeec-4584-81b9-cf23b850458d)

모델 파라미터의 개수는 $|V|$(차원 d 와 노드 개수의 곱)에 의해 결정된다

또한, parameters가 공유되기 때문에 이전에 보지 못한 노드들도 생성할 수 있다.

#### New Graphs

예시) 조직 A에서의 단백질 상호작용 그래프 모델을 학습한 것을 바탕으로, 조직 B에서 생성된 (모은) 데이터를 바탕으로 임베딩을 생성할 수 있음.

#### New Nodes

많은 앱(프로그램)들에선 이전에 못 본 노드들을 계속 마주치고는 한다

Youtube, Google Scholar, SNS (insta, …), community (reddit, 4chan ,..) — 어제 없던 글이나 영상, 유저가 오늘 새로 보인다.

필요한 경우 새로운 노드를 포함한 임베딩을 생성할 수 있다.


    오류나 틀린 부분이 있을 경우 언제든지 댓글 혹은 메일로 지적해주시면 감사하겠습니다!

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
