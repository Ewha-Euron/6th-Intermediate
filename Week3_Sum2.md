# 1. 신경망 개요

W3에서는 신경망 구현을 어떻게 하는지 알아보자.

기술적인 부분을 다루기 전에 뒤에서 자세히 볼 개념들을 간단하게 먼저 훑어보자.

---

로지스틱 회귀에서 보았던 시그모이드 계산 유닛들을 쌓아서 신경망을 만들 수 있다.

로지스틱 회귀의 신경망과 계산 그래프

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d01f4f40-e9e1-4692-ad14-1f42f1aa902b/112c4073-8b06-44a8-ba12-2c0ec1ddddc8/Untitled.png)

[]()

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d01f4f40-e9e1-4692-ad14-1f42f1aa902b/8ff03dd3-8e63-4a97-a6c5-9837dbbddeb8/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d01f4f40-e9e1-4692-ad14-1f42f1aa902b/c2565e80-0308-4d52-b451-7d691fd105a6/Untitled.png)

- 첫 번째 노드들은 z 계산 후 a를 계산하는 두 단계를 수행한다.
- 두번째 노드는 앞서 계산한 a를 이용하여 또 다른 z를 계산 후 a를 계산한다.
- 이 a가 예측값 $\hat{y}$이다.

여기서 첫 번째 노드들, 두 번째 노드라고 칭한 것들, 즉 일련의 노드들을 각각 하나의 **레이어(layer, =층)**이라고 한다.

l번째 레이어는 위첨자 [l]로 표시한다.

위 예시는 층이 2개인 신경망이다.

일반적인 신경망에서는 z→a 계산을 여러 번 수행하고, 마지막으로 손실 함수를 계산한다.

정방향 전파와 역방향 전파는 앞서 배웠던 것과 비슷하게 이루어진다.

# 2. 신경망 표현 방법

(신경망 그림 첨부)

앞서 보았던 신경망을 자세히 보자. 이 신경망은 hidden layer가 1개(single hidden layer)인 **2 layer NN**이다.

> $**a$(활성값, activations)\*\*: 신경망에서 하나의 층이 다음 층으로 전달하는 값

- input feature $x1, x2, x3$은 신경망의 **input layer(입력층)**
  - 0번째 레이어
  - $x = a^{[0]}$
- 노드들로 이루어진 중간의 레이어는 신경망의 **hidden layer(은닉층)**
  - input layer와 output layer 사이의 모든 층을 의미한다.
  - 지도학습의 train set에서는 (input, output) 쌍만 주어지고, 우리는 hidden layer의 값들을 알 수 없다.
  - $a^{[1]}$
    - $a^{[1]}\$ $a^{[1]}$$a_i^{[1]}$로 이루어진 열 벡터
    - 해당 층에서 몇 번째 노드인지를 아래 첨자 i로 표현한다.
- 노드 하나로 이루어진 마지막 레이어는 신경망의 **output layer(출력층)**
  - output layer는 예측값 $\hat{y}$를 계산한다.
  - $a^{[2]} = \hat{y} =a$ (최종 예측값)

<aside>
💡 신경망의 레이어를 셀 때 input layer는 세지 않는다.
위와 같은 신경망의 경우 input layer는 0번째 층이고, hidden layer부터 1번째 층이다. 따라서 2 layer NN이다.

</aside>

hidden layer와 output layer는 각각 연관된 파라미터를 가진다.

hidden layer의 파라미터: $w^{[1]},b^{[1]}$

- $w^{[1]}$의 차원: (4,3)
  - hidden layer의 노드 개수(4)
  - input layer의 노드 개수(3)
- $b^{[1]}$의 차원: (4,1)

output layer의 파라미터: $w^{[2]},b^{[2]}$

- $w^{[2]}$의 차원: (1,4)
  - output layer의 노드 개수(1)
  - hidden layer의 노드 개수(4)
- $b^{[2]}$의 차원: (1,1)

# 3. 신경망의 output 계산

**2 layer NN**에서 train sample이 하나에 대해 계산하기

신경망의 output 계산($x→\hat{y}$) 방법은 로지스틱 회귀와 비슷하지만 여러 번 반복된다는 점이 다르다.

노드 하나는 두 단계의 계산을 수행한다. 여러 개의 층을 이뤄 이를 여러 번 반복한다.

입력값이 노드 하나를 통과할 때 아래 과정을 거친다.

1. $*z=w^T+b*$
2. $*a=σ(z)*$

hidden layer의 첫 번째 노드는

1. $z_1=w_1^{[1]T}x+b_1^{[1]}$
2. $a_1^{[1]} = \sigma(z_1^{[1]})$ 를 계산한다.

두 번째 노드는

1. $z_2=w_2^{[1]T}x+b_2^{[1]}$
2. $a_2^{[1]} = \sigma(z_2^{[1]})$ 를 계산한다.

식을 모두 적으면 다음과 같다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d01f4f40-e9e1-4692-ad14-1f42f1aa902b/a5b8b958-c0d8-416a-bbf1-285b033f3de8/Untitled.jpeg)

신경망은 for문으로 구현하면 매우 비효율적라고 이미 배웠다.

이 식을 벡터화 해보자.

---

한 층에 노드가 여러 개면 세로로 쌓아 행렬를 구성한다.

각 w들로 (4,3) 행렬 만들기

행렬에 x 곱하기

b를 열 벡터로 만들어서 더하기

→ 각 층에서 열 벡터 z 생성

→ z 열 벡터에 시그모이드 함수를 적용하여 최종적으로 열 벡터 a 생성

이렇게 각 층에서 z, a를 계산한다.

# 4. 많은 샘플에 대한 벡터화

**2 layer NN2 layer NN**에서 m개의 모든 train sample에 대해 계산하기

> Recap: i번째 샘플은 위첨자 (i)로 표현한다.

역시 벡터화하여 for문을 제거하자.

하나의 샘플에 대해 각 층에서 계산했던 열 벡터 a와 z를 열 방향으로 이어 붙여 전체 샘플에 대해 각 층에서 A, Z 행렬을 만들 수 있다.

- 행: hidden 유닛의 개수
- 열: train sample 개수(m)

x도 역시 벡터화하여 행렬로 만든다.

- 행: feature 개수
- 열: m

→ 각 열만 보면 각 sample의 feature를 열 벡터로 표현한 것

# 5. 벡터화 구현 설명

결론적으로 우리는 정방향 전파를 벡터화했다. 이 벡터화가 왜 이렇게 구현되는지 알아보자.

간단히 하기 위해 b가 0이라고 가정한다.

- b가 있으면 브로드캐스팅에 의해 행렬의 각 열에 더해주게 될 것.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d01f4f40-e9e1-4692-ad14-1f42f1aa902b/fb12d38f-f60f-4a2b-a19e-2a0713e08364/Untitled.jpeg)

신경망의 각 층은 비슷한 계산을 수행한다.

2 layer가 아닌 더 깊은 신경망을 봐도 이를 더 반복하는 것 뿐이다.
