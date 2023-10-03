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

## P2.26
로봇은 그리퍼로 무거운 부하를 들 수 있으며 팔각 부위의 유연성이 높다[6, 20]. 이 로봇의 두 질량모델이 그림 P2.26에 주어져 있다. 전달함수 $Y(s)/F(s)$를 구하라.

<img src="https://ifh.cc/g/Rlb6or.jpg" width="350" height="300"/>

### 풀이
스프링-질량-감쇠기 시스템은 기계적인 운동에 속하므로 뉴턴의 운동법칙을 적용하여 두 물체의 질량은 각각 M,m이며 움직인 거리를 $x(t), y(t)$라 설정한다.

$$
M\frac{\mathrm{d^2x(t)}}{\mathrm{d} x^2} +b( \frac{\mathrm{dx(t)} }{\mathrm{d} x} -\frac{\mathrm{dy(t)} }{\mathrm{d} x}) + K(x(t)-y(t)) = F(t)
$$

$$
M\frac{\mathrm{d^2y(t)}}{\mathrm{d} x^2} +b( \frac{\mathrm{dy(t)} }{\mathrm{d} x} -\frac{\mathrm{dx(t)} }{\mathrm{d} x}) + K(y(t)-x(t)) = 0
$$

위 두개의 식을 라플라스로 정리하게 되면 아래와 같은 식이 된다.

$$
MS^2X(S) +bSX(S) + KX(S) - bSY(S) - KY(S) = F(S)
$$


$$
mS^2Y(S) +bSY(S) + KY(S) - bSX(S) - KX(S) = 0
$$

전달함수 $\frac{Y(S)}{F(S)}$를 행렬식으로 구하면

$$\begin{bmatrix}
MS^2+bS+k & -(bS + k)\\ 
 -(bS+K)& mS^2+bS+K 
\end{bmatrix}
\begin{bmatrix}
X(S) \\
Y(S)
\end{bmatrix}
&equals;
\begin{bmatrix}
F(S) \\
0
\end{bmatrix}
$$

이를 역행렬로 $Y(S)$를 구하면

$$
\begin{bmatrix}
X(S) \\
Y(S)
\end{bmatrix}
&equals;
A^{-1}
\begin{bmatrix}
F(S) \\
0
\end{bmatrix}
$$

Matlab으로 연산하면 다음과 같다.

```
syms S M m b k F

% 행렬 A 정의
A = [M*S^2 + b*S + k, -(b*S + k);
     -(b*S + k), m*S^2 + b*S + k];

% 행렬 A의 역행렬 구하기
A_inv = inv(A);

% 입력 벡터 정의
B = [F; 0];

Y = inv(A) * B;

% Y(S)/F(S) 계산
transfer_function = Y(2)/F;

% 결과 출력
disp('A의 역행렬:');
disp(A_inv);

disp('Y(S)/F(S) = ');
disp(transfer_function);
A의 역행렬:
[(m*S^2 + b*S + k)/(b*m*S^3 + k*m*S^2 + M*b*S^3 + M*k*S^2 + M*m*S^4),         (k + b*S)/(b*m*S^3 + k*m*S^2 + M*b*S^3 + M*k*S^2 + M*m*S^4)]
[        (k + b*S)/(b*m*S^3 + k*m*S^2 + M*b*S^3 + M*k*S^2 + M*m*S^4), (M*S^2 + b*S + k)/(b*m*S^3 + k*m*S^2 + M*b*S^3 + M*k*S^2 + M*m*S^4)]
 
Y(S)/F(S) = 
(k + b*S)/(b*m*S^3 + k*m*S^2 + M*b*S^3 + M*k*S^2 + M*m*S^4)
```


위 연산의 결과로 전달함수는 다음과 같다.


$$
G(S) = \frac{Y(S)}{F(S)} = \frac{k+bS}{MmS^4+bmS^3+MbS^3+kmS^2+kMS^2}
$$

## P2.37
입력 힘 $u(t)$를 가지는 두 개의 질량 시스템을 그림 P2.37에 나타났다. $m_1 = m_2 = 1$ 이고 $K_1 = K_2 = 2$일 때, (a) 이 시스템을 표현하는 미분방정식을 구하라. (b) $U(S))에서 $Y(S)$까지의 전달함수를 계산하라.

<img src="https://ifh.cc/g/a0FFR2.jpg" width="300" height="400"/>

### 풀이

#### (a) 이 시스템을 표현하는 미분방정식을 구하라 

$$
m_{1}\frac{\mathrm{d^2}x(t)}{\mathrm{d} t} + k_1x(t) + k_2(x(t)-y(t)) = 0
$$

$$
m_{2}\frac{\mathrm{d^2}y(t)}{\mathrm{d} t} + k_2(y(t)-x(t)) = u(t)
$$

위 식에 $m_1 = m_2 = K_1 = K_2 = 1$을 대입하여 미분방정식으로 정리한다.

$$
\frac{\mathrm{d^2}x(t)}{\mathrm{d} x} = -2x(t) + y(t)
$$

$$
\frac{\mathrm{d^2}y(t)}{\mathrm{d} t} = u(t) + x(t) -y(t)
$$

#### (b) $U(S))에서 $Y(S)$까지의 전달함수를 계산하라.

위 (a)에서 구한 미분방정식을 가져와 라플라스 변환을 적용하고

$$
S^2X(S) = -2X(S) + Y(S) \to (S^2+2)X(S) - Y(S) = 0
$$

$$
S^2Y(S) = U(S) + X(S) - Y(S) \to -X(S) + (S^2 + 1)Y(S) = U(S)
$$

행렬방정식으로 접근하면

$$
\begin{bmatrix}
S^2+2 & -1\\ 
 -1& S^2+1
\end{bmatrix}
\begin{bmatrix}
X(S) \\
Y(S)
\end{bmatrix}
&equals;
\begin{bmatrix}
0 \\
U(S)
\end{bmatrix}
$$

가 된다.

역행렬을 통해 $Y(S)$에 대해 전개하면 $U(S)$에서 $Y(S)$의 전달함수를 구할 수 있다.

$$
\begin{bmatrix}
X(S) \\
Y(S)
\end{bmatrix}
&equals;
\begin{bmatrix}
\frac{S^2+1}{S^4+3S^2+1} & \frac{1}{S^4+3S^2+1}\\ 
\frac{1}{S^4+3S^2+1}& \frac{S^2+2}{S^4+3S^2+1}
\end{bmatrix}
\begin{bmatrix}
0 \\
U(S)
\end{bmatrix}
$$

$Y(S) = \frac{S^2+2}{S^4+3S^2+1}U(S)$ 이므로 전달함수는 다음과 같다.

$$
G(S) = \frac{Y(S)}{(U(S)} = \frac{S^2+2}{S^4+3S^2+1}
$$















