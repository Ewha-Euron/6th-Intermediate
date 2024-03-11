# 1. 딥러닝 소개

## 1-1. 환영합니다!
"AI is the new electricity": 약 100년 전에 시작된 전기와 마찬가지로 AI는 여러 산업을 변화시키고 있다.

## 1-2. 신경망은 무엇인가?
__신경망(Neural Network)__: 입력(x)과 출력(y)을 매칭해주는 함수 찾는 과정 

__딥러닝(Deep Learning)__: 신경망을 학습시키는 것

## 1-3. 신경망을 이용한 지도학습
__지도 학습(Supervised Learning)__: 정답이 주어져있는 데이터를 사용하여 컴퓨터를 학습시키는 방법

, 신경망을 통해 구현 가능

<br/>

__구조적 데이터(Structured Data)__: 데이터베이스로 표현된 데이터, 정보의 특성이 잘 정의

__비구조적 데이터(Unstructured Data)__: 이미지, 오디오와 같이 특징적인 값을 추출하기 어려운 형태의 데이터

, 딥러닝 덕분에 컴퓨터가 비구조적 데이터를 인식 가능해짐

## 1-4. 왜 딥러닝이 뜨고 있을까요?
-__규모(Scale) 증가__: 신경망의 크기(많은 은닉 유닛, 연결, 파라미터), 데이터의 양

-__컴퓨팅 성능 향상(Computation)__

-__알고리즘(Algorithm)의 개선__ &nbsp;&nbsp; ex) Sigmoid 함수가 아닌 ReLU 함수를 사용함으로 Gradient 소멸 문제 해결

# 2. 신경망과 로지스틱회귀

## 2-1. 이진 분류
__이진 분류(Binary Classification)__: 결과가 ‘그렇다’이면 1로 표현, ‘아니다’이면 0

## 2-2. 로지스틱 회귀
__로지스틱 회귀(Logistic Regression)__: 답이 0 또는 1로 정해져있는 이진 분류 문제에 사용되는 알고리즘

![로지스틱 회귀 식](https://github.com/seoyeonkim3/Euron-Intermediate-study/blob/Week1/%EB%A1%9C%EC%A7%80%EC%8A%A4%ED%8B%B1%20%ED%9A%8C%EA%B7%80%20%EC%8B%9D.png?raw=true)
→시그모이드 함수를 통해 0과 1 사이의 값으로 변환

![시그모이드 함수](https://w7.pngwing.com/pngs/976/102/png-transparent-sigmoid-function-equation-angle-sigmoid-curve-angle-text-triangle-thumbnail.png)→시그모이드 함수

## 2-3. 로지스틱 회귀의 비용함수
__손실 함수(Loss Function)__: 하나의 입력특성에 대한 실제값과 예측값의 오차를 계산하는 함수

__비용 함수(Cost Function)__: 모든 입력에 대한 오차를 계산하는 함수, 모든 입력에 대해 계산한 손실 함수의 평균 값으로 구할 수 있음

<br/>
로지스틱 회귀 모델 학습: 비용함수를 최소화해주는 매개변수 w, b를 찾는 것

## 2-4. 경사하강법
__경사하강법(Gradient Descent)__: 비용함수를 최소화해주는 파라미터 w, b를 찾는 방법 중 하나

가장 가파른(steepest) 방향, 즉 함수의 기울기를 따라서 최적의 값으로 한 스텝씩 업데이트

![경사하강법 알고리즘](https://github.com/seoyeonkim3/Euron-Intermediate-study/blob/Week1/%EA%B2%BD%EC%82%AC%ED%95%98%EA%B0%95%EB%B2%95%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.png?raw=true)
→알고리즘

## 2-5. 미분
도함수(derivative, =어떤 함수의 기울기): 변수 a를 조금만 변화했을 때, 함수 f(a) 가 얼만큼 변하는지는 측정하는 것

## 2-6. 더 많은 미분 예제
![함수와 도함수](https://cphinf.pstatic.net/mooc/20181026_62/154051753591861ru0_PNG/derivatives.PNG)

