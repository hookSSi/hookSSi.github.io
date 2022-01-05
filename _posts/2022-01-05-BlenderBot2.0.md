---
layout: post
---

## 개요
- [개요](#개요)
- [서론](#서론)
- [중론](#중론)

2021.07 페이스북 AI에서 BlenderBot 2.0이 발표하였습니다. 기존 BlenderBot과는 무엇이 다르고 어떻게 달라질 수 있는 지 알아보겠습니다.

## [서론](#서론)

BlenderBot은 페이스북 AI에서 발표한 오픈 도메인 챗봇 모델로 

대화에 적절히 개입, 지식과 강세, 페르소나를 나타내면서 멀티턴 대화에서 일관적인 페르소나를 유지하는 것에 초점을 두었습니다.

공개된 모델은 90M, 2.7B, 9.4B 개의 파라미터를 가지는 모델입니다.
˜
![blenderbot](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCgGWh%2FbtqDOH4j03w%2FpaYXPsJ41Zaq9K7sK9kWNk%2Fimg.png)

<center>회색: 사람, 파란색: 9.4B 모델</center>

BlenderBot의 제작 과정은 다음과 같습니다.

### 데이터셋

성격, 지식, 강조 등 모델에게 학습시키고자 하는 테스크를 선택하고 다음과 같은 BST 데이터셋으로 구성하여 훈련시킵니다.

![BST](https://miro.medium.com/max/4800/1*25iAJygniSg4t5BbNgiP8w.png)
<center>BST 데이터셋</center>

이 데이터셋에 대한 자세한 내용은 [참조](https://parl.ai/projects/bst/)

### 모델

Retrieval, Generative, Retrieve-and-refine 3가지의 아키텍처를 고려할 수 있으며 

각각은 트랜스포머 구조입니다.

### 훈련

Cross-Entropy loss, negative sampling, MLE, UL, n-gram 분포 트래킹을 통한 동어 반복 문제 방지 등 여러 기법이 쓰인 듯 합니다.

구글의 Meena와 비교할 때도 더 좋은 성능을 보이지만 BlenderBot의 한계는 다음과 같습니다.

1. 한 대화 안에서 말을 반복하거나, 정확하지 않은 정보, 모순이 생기는 경우 등 여전히 실수가 있다.
2. 14턴 이내의 짧은 대화만 가능하며 더 긴 대화는 못함
3. 바른 행동을 하게 하는 것은 여전히 과제

## [중론](#중론)

BlenderBot 2.0은 Long-term memory와 인터넷을 활용해서 최신 정보를 검색해서 어떤 토픽이든 잘 대화할 수 있다고 합니다.

봇은 대화를 하면서 얻은 정보를 적절하게 저장하면서 며칠, 몇주, 몇달간 유지되긴 때문에 1.0과 달리 긴 대화도 가능합니다.

이런 정보는 개인별로 저장하기 때문에 향후 서비스에서도 유용합니다.

인터넷 검색을 위한 query 생성이 가능하고 검색으로 부터 얻은 결과에서 정보를 얻기 때문에 이 모델은 계속 최신 정보를 유지할 수 있습니다.

### 소개

기존 Language generation model 들은 기억 기능이 없는 소위 Goldfish memory를 가지고 있었습니다.

BlenderBot 1.0에서도 특히 이런 문제가 있었는데 2.0은 검색 엔진을 이용해 새로운 지식을 얻어낼 뿐만 아니라 Long-term local memory store에 저장하고 활용할 수 있습니다.

### 모델 아키텍처

FAIR의 [Retrieval Augmented Generation](https://hyunlee103.tistory.com/119) 이라는 연구에 기반한 모델을 사용합니다.

이 방법은 Seq2seq generator와 Information Retrieval 모델을 조합한 것으로 Long-term memory와 인터넷 검색 결과 모두를 활용해서 응답을 생성합니다.

결과로 나온 Knowledge를 사용하여 응답을 생성해 낼 때는 [Fusion-in-Decoder](https://arxiv.org/abs/2007.01282)라는 방법으로 knowledge와 대화 기록이 인코딩되며

이 인코딩된 값 기반으로 응답을 생성해 냅니다.

또한 봇의 Long-term memory store에 어떤 정보를 추가할 지 판단하는 Neural module 또한 가지고 있습니다.

![blenderbot2.0](https://miro.medium.com/max/1400/1*9IWLfvCO8jdaUzn4iFdTCA.png)
<center>Blenderbot 2.0 구조</center>

### 데이터셋

* Wizard of the Internet
인터넷 검색을 사용해서 새로운 정보를 이용해 가면서 대화하는 데이터셋.

* Multi-Session Chat
여러 개의 세션으로 이어지는 대화이면서, Long context를 가지는 대화 데이터셋.

## [결론](#결론)

1.0과 비교해서 성능, 바른 행동 비율은 높아졌지만 여전히 1.0이 가지는 한계와 같은 한계를 가지고 있습니다.

그리고 인터넷 검색을 활용하기 때문에 인터넷 검색 결과의 팩트 체크가 필요한 전망이나

Long-term memory를 활용하기는 하지만 진정한 learning을 하는 것은 아니기에 잘못된 정보를 바로잡는 능력 등은 부족합니다.