---
layout: post
categories: [ETC]
use_math: true
---

## Denoising Diffusion Probabilistic Models (DDPM)

DDPM은 간단히 이야기 하면 일단, 이미지에 노이즈를 계속 더합니다.

그리고 모델이 각 스텝 마다 노이즈를 예측하도록 모델을 훈련하고 모델을 사용하여 이미지를 생성합니다.

## Forwad Process

정방향 과정은 데이터 $x_0 \sim q(x_0)$에 대해 $T$ 타임스텝 동안 노이즈를 더하는 과정입니다.