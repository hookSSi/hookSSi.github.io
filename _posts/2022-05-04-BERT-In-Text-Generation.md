---
layout: post
use_math: true
---


## 개요
- [개요](#개요)
- [서론](#서론)

Auto Regressive Model인 GPT 계열은 Text Generation Task에서 효과적인 성능을 보이고 있습니다.

하지만 Non-Auto Regressive Model인 BERT는 Text Generation Task에서 거의 쓰이지 않거나 따로 처리가 필요합니다.

이런 차이를 만드는 이유는 무엇일까요?

## 서론

BERT(Bidrectional Encoder Representations from Transformers)

GPT 모델과 차이는 크게 2가지입니다.

1. Tranformer 구조에서 GPT는 디코더를 여러 layer로 쌓아 사용하는 반면 BERT는 인코더를 여러 layer로 쌓아 사용합니다.
2. 순방향으로 Attention을 참조하는 GPT와 달리 BERT는 양방향으로 Attention을 참조합니다.