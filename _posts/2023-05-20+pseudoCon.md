--- 
title : 가짜연구소 6th PseudoCon 참여 후기


date : 2023-05-20
---

메모 우선
230520 6th PsuedoCon

패들랫, 가짜연구소 디스코드 참고

## 1. 다양한 산업에서의 GPT 활용 사례

<!-- 강연자 : 안성진 (Microsoft) -->

GPT 모델 활용 : 
프라이버시 - ChatGPT
OpenAI API & AOAI (Azure OpenAI)

활용 사례 
GPT-4 : How does it work, and how do I build apps with it? - CS50 talk
: Innovation  (대만 국립 사범대학)
: Cost Saving 
 - CarMax : Summarization에 GPT 활용 
 - Trelent : Github Copilot과 반대? Code를 통해 Documentation을 만드는 서비스에 GPT 활용
 - Thread : 고객 지원 요청에 대한 해결 과정 logging 시간을 줄이는 데 GPT 활용 (요약본 생성)
 - Morgan Stanley : 사내에 저장된 많은 PDF 자료를 검색, 관리함에 있어 용이하도록 GPT 활용

느낀점 : GPT API의 실무에서의 여러 사례를 알아볼 수 있었음. 나라면 이 API를 어떻게 활용할 수 있을까라는 생각을 하게 됨.

Q&A
보안 ISSUE 관련 질문

## 2. Diffusion Model이 불러온 새로운 시대

<!-- 강연자 : 조상우 --> 

Discriminative Model vs Generative Model
Discriminative : distribution P(y|x)
Generative : distribution P(x)
Conditional Generative : distribution P(x|y)

생성모델의 역사
VAE, GAN, NeRF ,... , Difusion

Diffusion
Forward - make Gaussian Blur
Reverse - Remake original image

Stable Diffusion

Text-to-Image 응용사례 및 한계점

응용사례
- DreamBooth

한계점

- 손발 모양 등을 잘 못그림 (추가 연구)

느낀점 : 생성모델 및 Diffusion에 대해 간단히 훑어볼 수 있었음. 더 심화된 이론을 확인해 보고 싶다는 느낌을 받음, 스터디를 소개하는 모습에서, 나도 언젠가 참여하고 싶다는 생각을 하게 됨



## 3. New Paradigm in NLP

<!-- 강연자 : 이정훈 (Allganize Korea) -->

GPT의 Instruction - 양자역학에 대해 설명해 줘?? vs (조건 추가)

Instruction을 어떻게 구성할지가 AI Prompt Engineer의 중요한 역량일 것이라 생각

CoT (선택 방식) : 출근하는 방법 중 더 빠른 건 무엇입니까? -> 

Prompt Engineering, Prompt Market (ChatGPT Prompt Markets)

단점 
- Hallucination 심함

GPT4 
Multi Modal
성능이 안 좋은 Task를 찾는 데에 있어 아직 약점이 있음

LangChain
- ChatModels
- Embeddings : 유사한 텍스트 탐색 등에 사용


## 4. 논문으로 알아보는 추천시스템 트렌드

<!-- 강연자 : 이경찬 (하나투어) -->

논문 리뷰를 통해 알게 된 추천 시스템 발전 과정

GNN (Graph Neural Network)

추천시스템의 기본 요소

기업 - 유저의 체류시간을 늘릴 수 있음

유저 - 입맛대로 컨텐츠를 볼 수 있음

User, Item, Interaction (평점, 조회수, 좋아요, 구독자수 등)

딥러닝 기반 추천 모델 -> 단순 내적은 성능을 저해할 수 있다. 그 한계를 극복할 수 있는 새로운 대안으로 등장

동적 선호도 반영 (2016)

GNN Based Recommendation (2018) - 고차원 연결성에 강점

동향 : 더 멀리 있는 신호를 포착하고, 더 최신 신호를 반영할 수 있는 구조와 데이터

확대 되어가는 데이터, 아키텍쳐


## 5. 강화학습을 활영환 산업 최적화 문제 도전기

<!-- 강연자 : 임용섭 -->


### 6. 파이썬의 비밀

<!-- 강연자 : 김광일 -->


### 7. SSL

강연자가 학부 2학년생임... <!-- 이게 재능인가?? -->
