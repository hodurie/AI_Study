# Manifold Learning
```
Manifold
- 고차원 데이터를 공간 상에 표현 했을 때 이를 잘 어우르는 subspace
```

데이터를 잘 설명하는 Manifold를 찾아 차원을 줄이는 것이 Manifold Learning의 목표

<img src='images/Manifold Learning/ManifoldLearning.jpg'>

Manifold Learning의 목적
1. Data Compression
2. Data Visualization
3. **Curse of dimensionality**
4. **Discovering most important features**


## Data Compression

<img src='images/Manifold Learning/EX01.jpg'>

데이터 압축과 관련된 논문
- JPEG와 AutoEncoder를 비교
    - AutoEncoder의 압축 효과가 더 좋음

## Data Visualization
<img src='images/Manifold Learning/EX02.png'>

시각화 한 방식인 t-SNE
- 데이터가 갖고 있는 정보를 시각화를 통해 직관적으로 파악할 수 있음
    - 차원 축소가 필요한 이유

## Curse of Dimensionality

<img src='images/Manifold Learning/CoD.jpg'>

차원의 저주
- 차원이 증가할수록 한 공간에 데이터의 밀도가 희박해지는 문제
    - 데이터 분포 분석 또는 모델 추정에 필요한 샘플 데이터가 기하급수적으로 늘어남

<img src='images/Manifold Learning/Manifold.png'>

Manifold의 가정
- 고차원의 데이터는 저차원의 Manifold가 존재함
- 저차원의 Manifold를 벗어나면 밀도는 급격히 낮아짐

차원의 저주가 일어나지 않는 Manifold를 찾는 것이 Manifold Learning의 목표

```
Manifold Learning을 통해 특정 Domain의 Manifold 찾음
= 특정 Domain에 대한 관계성을 잘 찾음
= 특정 Domain을 잘 어우르는 확률 분포를 찾음
```

## Discovering Most Important Features

<img src='images/Manifold Learning/Mnist.png'>

Manifold를 잘 찾으면 여러 feature들 추출할 수 있음
- 좌표가 달라지면 이미지의 굵기, 회전 등의 변화가 생김
    - Unsupervised Learning을 통해 자동적으로 feature들을 찾음

<img src='images/Manifold Learning/Metric.jpg'>

feature을 잘 찾았다는 것은 Metric과 연결시켜 해석할 수 있음
- 고차원 상에선 A1과 B가 가까워 보이지만
- Manifold 상에선 A2와 A1이 가까움

<img src='images/Manifold Learning/Golf.jpg'>

위의 설명을 골프 사진에 대입
- 고차원 상에서 A1과 B의 중간 지점을 나타내면 의미 없는 사진이 도출 됨
    - Manifold에서 벗어난 결과이기 때문

<img src='images/Manifold Learning/Golf2.jpg'>

Manifold 상에서 A1과 B의 중간 지점을 나타내면 의미 있는 사진이 도출 됨

<img src='images/Manifold Learning/Mnist2D.png'>

Manifold를 잘 찾아내면 의미적으로 비슷한 데이터들 끼리 뭉치게 됨
- 유의미한 feature들로 나눠지게 됨

## Dimension Reudction
<img src='images/Manifold Learning/DimReduction.png'>

- 차원을 축소하는 이유는 Manifold를 잘 찾아내기 위함
- 앞으로 다룰 AE는 Non-Linear 방식으로 차원축소를