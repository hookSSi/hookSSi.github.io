---
layout: post
use_math: true
---


# pytorch custom loss function

## pytorch의 loss function 동작 방식

1. torch는 tensor에 requires_grad=True를 해두면 loss 함수를 통해 grad를 얻을 수 있습니다.

2. loss 함수를 통해 loss 값을 구한 후 그 값에 backward()처리를 해주면 이 loss를 구하면서 사용된 변수들의 gradient가 구해집니다.

3. optimizer를 사용한다면 optimizer로부터 iteration을 돌 때 매번 gradient를 초기화 할 수 있습니다.(zero_grad 함수)

## 만들기

```python

def mae_loss(input, target):
    N = input.size()[1]
    output = torch.abs(input - target)
    output = torch.sum(output, dim=1) / N
    output = torch.sum(output) / output.size()[0]
    return output
```

```python

class MAE(nn.Module):
    def __init__(self):
        super(MAE, self).__init__()

    def forward(self, inputs, targets):
        N = input.size()[1]
        output = torch.abs(input - target)
        output = torch.sum(output, dim=1) / N
        output = torch.sum(output) / output.size()[0]

        return output
```

## 체크리스트
1. input, target의 형식
2. 미분값 확인

# 미분값 확인 방법

```python
import torch

w = torch.tensor(2.0, requires_grad=True)

y = w**2
z = 2*y + 5

z.backward()

# 수집한 기울기들이 올바른지 확인
print('수식을 w로 미분한 값 : {}'.format(w.grad))
```

# 참고링크
[Loss Function Library](https://www.kaggle.com/bigironsphere/loss-function-library-keras-pytorch)

