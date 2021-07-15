# Revisit Deep Neural Networks
이번 장의 목표
- `DNN 학습 = ML(Maximum Likelihood) 추정` 이해

## Classic Machine Learning

<img src='images/Revisit Deep Neural Networks/ClassMachineLearning.png'>

전통적인 Machine Learning
1. 학습 데이터 수집 
    - $(x, y)$ 쌍으로 수집
2. 모델 정의
    - 데이터의 어떤 모델을 적합할지 정의
    - Loss Function 정의
3. 모델 학습
    - Loss Function을 최소화 하는 파라미터 찾기
4. 예측
    - 학습 한 모델에 입력 값을 대입

## Deep Neural Networks
DNN과 전통적인 Machine Learning 차이점이 존재

<img src='images/Revisit Deep Neural Networks/DeepNeuralNetworks.png'>

- Deep Neural Network 모델 사용
- Back Propagation 알고리즘 사용
    - 두 가지 제약조건으로 Loss Function을 MSE(Mean Squared Error), CE(Cross Entropy)로 제한
        - **가정1** : 전체 데이터의 Loss Function은 각 샘플의 Loss Function의 **합**과 같다.
        - **가정2** : Network의 **출력 값**과 **정답 값**으로만 Loss Function을 구성

<img src='images/Revisit Deep Neural Networks/Learning.jpg'>

- Loss를 최소화 할 때 Gradient Descent 사용
    - iterative Method를 이용해 정답에 가깝게 만듦
        - 이에 대해 의문점이 발생할 수 있음
            - $\theta$를 어떻게 업데이트 할 것인가?
            - 언제 학습을 종료 할 것인가?
        - 답변
            - Loss가 줄어드는 방향으로 이동
            - 이동 했을 시 Loss가 변하지 않으면 멈춤

<img src='images/Revisit Deep Neural Networks/DeltaTheta.jpg'>

- 그렇다면 어떻게 $\Delta\theta$를 변화 시켜야하나?
    - Taylor Expansion 사용
        - $L(\theta)$ 에 1차 미분부터 무한 차원까지의 미분을 모두 더한 값이 $L(\theta + \Delta\theta)$ 와 같음
        - 이때 1차 미분까지 더한 값만 같다고 근사
            - 좁은 영역에서만 감소 방향이 정확함
        - $\Delta\theta$를 learning rate $\eta$를 이용하여 정의 후 파라미터 업데이트
            - 대개 $\eta$의 값은 0.001이나 그보다 작은 값을 사용

<img src='images/Revisit Deep Neural Networks/Training.jpg'>

- 위의 **가정1** 에 따라서 Loss Function은 각 샘플들의 Loss Function들의 합과 같다고 정의
- 이를 Gradient를 취해주고 데이터의 개수로 나눠 평균 Loss를 재구성함
- 데이터 전부를 사용해 Loss 합을 구해 파라미터를 구하는 것은 효율성과 학습 속도가 느림
    - 이를 일정 데이터 묶음으로 나눠(mini-batch) 계산 후 파라미터 갱신
        - Stochastic Gradient Descent
    - 1 epoch 에 파라미터 갱신 -> 1 batch size 에 파라미터 갱신

<img src='images/Revisit Deep Neural Networks/Backpropagation.jpg'>

- $\theta$는 $w, b$ (weight, bias)로 구성 돼 있음
- 각 weight, bias는 레이어 별로 존재
    - Loss Function을 미분하여 layer 별 파라미터를 업데이트
        - Back Propagation 사용

### Back Propagation 알고리즘
1. Output layer에서 Error Signal을 구함
    - **가정2**에 따라 Loss를 network 출력값을 이용해 미분
    - 활성화 함수 값을 적용한 값을 요소별 곱을 구함
2. 근접 layer의 Error Signal을 구함
    - 이전 layer의 값을 넘겨 받아 weight와 곱함
    - 활성화 함수 값을 적용한 값을 요소별 곱을 구함
3. weight와 bias를 갱신
    - bias는 error값과 동일
    - weight는 error값과 앞단의 입력값과 곱함

<img src='images/Revisit Deep Neural Networks/LossFunction.jpg'>

DNN에서 사용하는 Loss Function은 MSE, CE로 한정 됨

이 두 Loss Function은 어느 상황에서 사용해야 할까?
- 두 가지 관점에서 비교
    1. Back Propagation
        - CE가 더 좋음
    2. Maximum Likelihood
        - 출력값 Continuous : MSE
        - 출력값 Discrrete : CE

### Back Propagation 관점
#### MSE
- Loss Function을 output 값으로 미분
- 활성화 함수를 미분해 요소별 곱
- weight와 bias 업데이트

아래 그래프를 보면 초기 값에 따라 output의 차이가 발생

<img src='images/Revisit Deep Neural Networks/Output.jpg'>

초기값에 따라 output의 차이가 발생하는 이유는?
- Back Propagation은 활성화 함수 미분값이 존재
    - 미분한 값이 0에 까갑게 되면 파라미터의 수정이 거의 이루어지지 않음
    - Sigmoid 함수의 경우 layer을 지날때 마다 1/4 씩 최대값이 줄어듦
        - 출력단에선 파라미터의 갱신이 잘 되지만 입력단에선 수정이 거의 이루어지지 않음
            - Gradient Vanishing 문제
        - 이를 방지하기 위해 ReLU 함수로 대체해 사용

#### Cross Entropy

<img src='images/Revisit Deep Neural Networks/CrossEntropy.jpg'>

CE의 경우 MSE와 다르게 Error 값에 활성화 함수의 미분값이 곱해지지 않음
- 초기값에 민감하게 반응하지 않음
- Gradient Vanishing 문제에 어느정도 대처 할 수 있음

<img src='images/Revisit Deep Neural Networks/MSEvsCE.jpg'>

- CE가 초기값에 둔감하며 학습이 빠르게 일어남
- MSE의 경우 초기값에 민감함

### Maximum Likelihood 관점
<img src='images/Revisit Deep Neural Networks/MLE.png'>

- 네트워크의 출력값이 정답값과 비슷하게 만드는 쪽으로 모델 학습
    - $p(y|f_{\theta}(x))$ 출력값이 주어졌을 때 정답값이 나올 확률이 높은 쪽으로 모델 학습

위의 관점을 따르기 위해선 두 가지를 정해야 됨
1. 네트워크의 모델이 무엇인가?
2. 가능도를 최대로 하는 확률 분포가 무엇인가?

Loss Function에 대해 살펴보면 Negative Log Likelihood로 정의 돼 있음
- log 의 경우 전체 loss가 각 샘플의 loss의 합 이라는 가정을 만족시키기 위해 적용

```
두 관점에 따른 해석
1. BP 관점
- 정답값과 출력값의 차이를 어떻게하면 작게 만들까?

2. ML 관점
- 추정 파라미터 분포에서 정답값이 나올 확률이 최대가 되는 지점은 뭘까?
```

ML 관점에서의 장점
- 확률 분포를 이용해 **sampling**이 가능
    - 고정 입력에 **다양한 출력**이 가능

<img src='images/Revisit Deep Neural Networks/iidCond.jpg'>

Loss Function은 Negative Log Likelihood 사용
- 이를 사용하기 위해선 다음과 같은 가정을 만족해야 함
    - i.i.d
        - Independence
            - 각 데이터는 서로 독립적
            - 각 데이터에 대한 확률은 곱셈으로 표현 가능 $p(y|f_{\theta}(x)) = \Pi_{i}p_{D_i}(y|f_{\theta}(x_i))$
        - Indentical Distribution
            - 각 데이터는 동일한 분포에서 추출 됨

<img src='images/Revisit Deep Neural Networks/13p.jpg'>

Negative Log Likelihood를 가우시안 분포와 베르누이 분포를 적용
1. 가우시안 분포
    - 결과값이 MSE와 동일
2. 베르누이 분포
    - 결과값이 CE와 동일

위에서 출력값이 Continuous냐 Discrrete냐에 따라 Loss Function을 다르게 사용해야 한다는 것이 위의 식을 풂으로써 증명 됨
- 출력값 Continuous : MSE
- 출력값 Discrrete : CE

<img src='images/Revisit Deep Neural Networks/15p.jpg'>

- ML 관점에서 네트워크의 값은 Likelihood가 아님
- 규정한 확률 분포의 파라미터 값을 추정

<img src='images/Revisit Deep Neural Networks/Bengio.jpg'>

Bengio의 슬라이드를 참고하면 위의 내용을 한 슬라이드로 설명 가능