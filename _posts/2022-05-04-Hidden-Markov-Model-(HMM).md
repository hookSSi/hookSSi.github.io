---
layout: post
categories: [Lab]
use_math: true
---


## 개요
- [개요](#개요)
- [HMM](#Hidden-Markov-Model-(HMM))
- [중론](#중론)

Hidden Markov Model (HMM)은 Conditional Random Field (CRF)가 제안되기 이전에 POS tagging과 같은 sequential labeling에 자주 이용되던 알고리즘입니다.

HMM은 CRF와 비교하여 unsupervised learning도 할 수 있다는 장점이 있습니다.

학습 코퍼스를 이용한다면 HMM이 CRF보다 빠른 학습속도도 보이지만 HMM은 단어열의 문맥을 기반으로 추정하지 못합니다.

이는 unguaranteed independence problem이라는 HMM의 구조적 특징 때문입니다.

이 포스트에서는 제 스스로 HMM의 원리와 구조를 살펴보고자 작성되었습니다.

## Hidden Markov Model (HMM)

HMM은 길이가 $n$인 sequence $x_{1:n} = [x_1, x_2, ..., x_n]$에 대하여 $P(y_{1:n}|x_{1:n})가 가장 큰 $y_{1:n}$를 찾습니다.

품사 판별의 문제를 예로 들면 $n$개의 단어로 구성된 단어열에 대하여 각 단어의 품사 $y$를 부여하는 것입니다.

이 과정을 HMM의 decoding이라 하며 우리가 찾아야 하는 label $y$를 HMM에서는 state라 합니다.

이때 $P(y_{1:n}|x_{1:n})$는 다음처럼 계산됩니다.

$$
P(y_{1:n} \vert x_{1:n}) = P(x_1 \vert y_1) \times P(y_1 \vert START) \times P(y_2 \vert y_1) \times P(x_2 \vert y_2) \cdots
$$

위의 식은 현재 시점 $i$의 state인 $y_i$를 판별하기 위하여 이전 시점의 state인 $y_{i-1}$이 이용됩니다.

이처럼 이전의 한 단계 전의 state 정보를 이용하는 모델을 first-order Markov Model이라 합니다.

만약 이전 두 단계의 states 정보를 모두 이용한다면 $P(y_i|y_{i-2}, y_{i-1})이 학습되어야 하며, 이는 second-order Markov Model이라 합니다.

![](https://tva1.sinaimg.cn/large/e6c9d24egy1h1dxb8qie9j20e503674a.jpg)

이처럼 state 간의 변화 확률을 transition probability (전이 확률)라 합니다.

HMM은 각 state에서 우리가 관측 가능한 값(observation)이 발생할 확률이 있다고 가정합니다.

이를 emission probability, $P(x_i|y_i)$라 합니다.

그리고 컴퓨터에게 곱셈은 덧셈보다 비싼 작업이기 때문에 확률을 곱하는 작업들은 주로 log를 씌워 덧셈으로 변환합니다.

$$
log P(y_{1:n} \vert x_{1:n}) = log P(x_1 \vert y_1)+ log P(y_1 \vert S) + log P(y_2 \vert y_1) + log P(x_2 \vert y_2) \cdots
$$