# 제어공학1_Chapter2_Assignment

## P2.7
그림 P2.7과 같이 1차 저역통과 필터로 구현한 적분 증폭기 회로의 전달함수를 구하라.

<img src="https://ifh.cc/g/r6VqLT.jpg" width="300" height="200"/>

### 풀이
이상적인 연산증폭기의 동작조건으로 $V_2(S)$와 $V_1(S)$간에 입출력 관계는

$$
V_2(S) = -\frac{Z_2(S)}{Z_1(S)}V_1(S)
$$

이고 여기서 $Z_1(S) = R, Z_2(S) = \frac{1}{C_S}$라고 한다면

$$
V_2(S) = -\frac{1}{RC_S}V_1(S)
$$

이고 여기서 라플라스 변환을 통해 전달함수를 구하면

$$
G(S) = \frac{V_2(S)}{V_1(S)} = -\frac{1}{RC_S}
$$

## P2.12
그림 P2.12에 주어진 블록선도로 표현된 개루프 제어시스템에 대해, $t \to \infty$일 때 단위계단 입력 $r(t)$에 대한 응답 $y(t) \to 1$이 되도록 $K$값을 정하라. 초기조건은 영이라고 가정한다.

<img src="https://ifh.cc/g/z0pmnG.jpg" width="300" height="200"/>

### 풀이
초기조건이 0이므로, Laplace로 입,출력 간의 관계를 타나낼 수 있다. $\to \frac{Y(S)}{X(S)} = \frac{K}{S+50}$

단위계단 입력으로 $r(t)$의 라플라스 변환값은 $R(S) = \frac{1}{S}$

$$
Y(S) = \frac{K}{S+50}R(S) = \frac{K}{S(S+50)} = \frac{K}{50}(\frac{1}{S}-\frac{1}{S+50})
$$

이 입출력 관계식을 역 라플라스 변환을 하면

$$
y(t) = \frac{K}{50}(1-e^{-50t})
$$

가 되고 이때, $t \to \infty, y(t) \to 1$이기 위해서 $K=50$이다.



























