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

## P2.15
스프링-질량 시스템이 그림 P2.15에 주어졌다. 질량 m의 운동을 기술하는 미분방정식을 구하라. 초기조건이 영인 임펄스 입력에 대한 시스템의 응답$x(t)$를 구하라.

<img src="https://ifh.cc/g/VXfWP6.jpg" width="350" height="300"/>

### 풀이

스프링-질량-감쇠기 시스템은 기계적인 운동에 속하므로 뉴턴의 운동법칙을 적용하여 문제를 푼다. 이때 마찰력, 스프링으 장력, 물체의 중력에 대한 식을 구하면

$$
m\frac{d^2x(t)}{dt^2} + b\frac{dx(t)}{dt} + kx(t) = 0
$$

이 식을 라플라스 변환을 통해 정리하면

$$
m(S^2X(S) - Sx(0^-) - \frac{dx(t)}{dt}) + b(SX(S) - x(0^-)) + kX(S) = 0
$$

$$
r(t)=0,x(0^-)=x_0,\frac{dx(t)}{dt})=0 \to mS^2\cdot X(S) -mSx_0 + bSX(S) - bx_0 + kX(S) = 0
$$

식을 정리하면

$$
mS^2X(S) + bSX(S) + kX(S) = mSx_0 + bx_0
$$

$$
X(S)(mS^2+bS+k) = x_0(mS+b)
$$

$$
X(S) = \frac{mS+b}{mS^2+bS+k}x_0
$$

가 되고 이를 Matlab을 통해 역라플라스를 진행하면

```
syms S m b k
XS = (m*S + b) / (m*S^2 + b*S + k);
xt = ilaplace(XS);
disp('역라플라스:')
disp(xt);
역라플라스:
exp(-(b*t)/(2*m))*(cosh((t*(b^2/4 - k*m)^(1/2))/m) + (b*sinh((t*(b^2/4 - k*m)^(1/2))/m))/(2*(b^2/4 - k*m)^(1/2)))

```

위 연산을 진행하면


$$
e^-{\frac{bt}{2m}}(cosh(\frac{t\sqrt{\frac{b^2}{4}-km}}{m})+b\frac{sinh(\frac{t\sqrt{\frac{b^2}{4}-km}}{m})}{2\sqrt{\frac{b^2}{4}-km}}) \cdot x(0)
$$












































