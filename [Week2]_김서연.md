# 2. 신경망과 로지스틱회귀
## 2-7. 계산 그래프 ~ 2-8. 계산 그래프로 미분하기
신경망 계산

  -정방향 전파: 신경망의 출력값 계산
  
  -역방향 전파: 경사, 도함수 계산

<br/>

__미분의 연쇄법칙(Chain Rule)__

-합성함수의 도함수(←합성함수를 구성하는 함수의 미분을 곱함으로써)에 대한 공식

-역방햔 전파에서 손실 함수의 그래디언트를 계산할 때 적용

![dvar 표기법](https://github.com/seoyeonkim3/Euron-Intermediate-study/blob/Week2/dvar%20%ED%91%9C%EA%B8%B0%EB%B2%95.png?raw=true)

## 2-9. 로지스틱 회귀의 경사하강법 ~ 2-10. m개 샘플의 경사하강법
로지스틱 회귀의 비용함수 수식

![로지스틱 회귀의 비용함수](https://github.com/seoyeonkim3/Euron-Intermediate-study/blob/Week2/%EB%A1%9C%EC%A7%80%EC%8A%A4%ED%8B%B1%20%ED%9A%8C%EA%B7%80%EC%9D%98%20%EB%B9%84%EC%9A%A9%ED%95%A8%EC%88%98%20%EC%88%98%EC%8B%9D.png?raw=true)

<br/>

코드 표현

![코드 표현](https://cphinf.pstatic.net/mooc/20180615_249/1529027949584hxeeh_PNG/image.PNG?type=w760)

# 3. 파이썬과 벡터화
## 3-1. 벡터화 ~ 3-2. 더 많은 벡터화 예제
__벡터화(Vectorization)__

-for문을 사용할 필요 없어짐

-백터화된 코드는 (벡터화되지 않은 코드보다) 실행 속도가 빠름

-Pyton, Numpy 같은 고수준 언어와 라이브러리를 사용하면, 하드웨어(CPU, GPU) 가속 이용 가능

<br/>

SIMD(Single Instruction Multiple Data)

-병렬 프로세서의 한 종류로, 하나의 명령어로 여러 개의 값을 동시에 계산하는 방식

-벡터화 연산을 가능하게 함

## 3-3. 로지스틱 회귀의 벡터화
for문(i 값을 변화시키며 계산)
<br/>
![for문](https://github.com/seoyeonkim3/Euron-Intermediate-study/blob/Week2/for%EB%AC%B8.png?raw=true)

벡터화
<br/>
![벡터화](https://github.com/seoyeonkim3/Euron-Intermediate-study/blob/Week2/%EB%B2%A1%ED%84%B0%ED%99%94.png?raw=true)

## 3-4. 로지스틱 회귀의 경사 계산을 벡터화 하기
for문
<br/>
![경사 for문](https://cphinf.pstatic.net/mooc/20180615_244/1529028895251WEzUQ_PNG/pic1.PNG)

벡터화
<br/>
![경사 벡터화](https://cphinf.pstatic.net/mooc/20180615_8/152902893889842v4T_PNG/pic2.PNG)
