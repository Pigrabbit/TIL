# Linear Regression

우리가 하고 싶은 것은 input data를 통해 output을 예측하는 모델을 만드는 것이다. 그 중에서 가장 단순한것이 선형 일차 함수(linear model)일 것이다.

```
y = ax + b
```

x: input feature, y: output feature, b: bias

Linear regression의 목적은 loss = sum(predicted output feature value - output feature value)^2 를 최소화 하는 것이다. 그걸 어떻게 할까?

## Gradient decent method

gradient decent method를 통해 loss 를 최소로 하는 기울기 a 및 bias b를 찾는다.

