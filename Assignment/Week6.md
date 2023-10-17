# 제어공학1_Chapter3_Assignment

## P3.1
그림 P3.1에 스프링-질량-감쇠기 시스템이 주여져 있다. (a) 적당한 상태변수를 설정하라. (b) 상태변수로 표현된 1차 미분방정식을 구하라. (c) 상태미분방정식을 구하라.

<img src="https://ifh.cc/g/wXFAok.jpg" width="600" height="200"/>

### 풀이
__(a) 적당한 상태변수를 설정하라.__

스프링-질량-감쇠기는 뉴턴의 제 2법칙으로, 시스템을 표현하기 위한 충분한 상태변수는 질량의 위치와 속도이므로

$$
x(t) = (x_1(t), x_2(t))
$$

로 정의할 수 있다.

여기서

$$
x_1(t) = y(t), x_2(t) = \frac{dy(t)}{dt}
$$

이다.

__(b) 상태변수로 표현된 1차 미분방정식을 구하라.__

이 시스템의 미분방정식은

$$
M\frac{d^2y(t)}{dt^2} + b\frac{dy(t)}{dt} + ky(t) = u(t)
$$

이며 상태변수로 나타내기 위해 상태변수를 정의하여 대입하면

$$
M\frac{dx_2(t)}{dt} + bx_2(t) + kx_1(t) = u(t)
$$

로 표현할 수 있다.

__(c) 상태미분방정식을 구하라.__

따라서 

$$
\frac{dx_1(t)}{dt} = x_2(t)
$$

$$
\frac{dx_2(t)}{dt} = -\frac{b}{M}x_2(t) -\frac{k}{M}x_1(t) + \frac{1}{M}u(t)
$$

으로 두 개의 1차 미분방정식으로 쓸 수 있다.

## P3.3
그림 P3.3과 같은 RLC 회로가 주어졌다. 상태변수 $x_1(t) = i_L(t), x_2(t) = v_c(t)$로 설정하고 상태미분방정식을 구하라.

<img src="https://ifh.cc/g/w7SpNw.jpg" width="350" height="200"/>

### 풀이
주어진 상태변수는

$$
x_1(t) = i_L(t), x_2(t) = v_c(t)
$$

이다.

외부 회로에서 KVL을 적용하면

$$
L\frac{di_L(t)}{dt} - v_c(t) + v_2(t) - v_1(t) = 0
$$

이고 KCL을 노드를 기준으로 적용하면

$$
C\frac{dv_c(t)}{dt} = -i_L(t) + i_R
$$

이 된다. 여기서 R에 흐르는 i_R을 고려해보면

$$
i_RR - v_2(t) + v_c(t) = 0
$$

$$
i_R = \frac{v_2(t)}{R} - \frac{v_1(t)}{R}
$$

가 되고 이를 KCL에 적용하면

$$
C\frac{dv_c(t)}{dt} = -i_L(t) + \frac{v_2(t)}{R} - \frac{v_1(t)}{R}
$$

로 정리할 수 있다.

위 상태미분방정식들을 matrix형식으로 표현하면

$$
\begin{pmatrix} \dot{x_1} \\
\dot{x_2} 
\end{pmatrix} = \begin{bmatrix} 0 & 1/L \\
-1/C & -1/RC
\end{bmatrix}\begin{pmatrix} x_1 \\
x_2
\end{pmatrix} + \begin{bmatrix} 1/L & -1/L \\
0 & 1/RC
\end{bmatrix} \begin{pmatrix} v_1 \\
v_2
\end{pmatrix}, where x_1 = i_L  and  x_2 = v_c
$$

## P3.5
그림 P3.5에 폐루프 제어시스템이 주어져 있다. (a) 폐루프 전달함수 $T(s) = \frac{Y(s)}{R(s)}$를 구하라. (b) 상태변수 모델을 구할고 위상변수형 블록선도를 작성하라.

<img src="https://ifh.cc/g/g2pVxg.jpg" width="400" height="200"/>

### 풀이
__(a) 폐루프 전달함수 $T(s) = \frac{Y(s)}{R(s)}$를 구하라.__

폐루프의 전달함수는 반환되는 부분을 고려하여

$$
T(s) = \frac{Y(s)}{R(s)} = \frac{G(s)}{1+G(s)} = \frac{\frac{s+2}{s^3+5s^2-24s}}{1+\frac{s+2}{s^3+5s^2-24s}} = \frac{s+2}{s^3 + 5s^2 - 23s +2}
$$

가 된다.

__(b) 상태변수 모델을 구할고 위상변수형 블록선도를 작성하라.__

행렬미분방정식은

$$
A = \begin{bmatrix} 0 & 1 & 0 \\
0 & 0 & 1 \\
-5 & 23 & -2 \end{bmatrix}
$$

$$
B = \begin{bmatrix} 0 \\
0 \\
1
\end{bmatrix}
$$

$$
C = \begin{bmatrix} 2 & 1 & 0
\end{bmatrix}
$$

에서

$$
\dot{x} = Ax +Bu
$$

$$
y=Cx
$$

가 된다.

__(a),(b)를 matlab으로 아래와 같이 표현할 수 있다.__

* 코드
```matlab
b = [0 0 1 2];
a = [1 5 -23 2];

[A,B,C,D] = tf2ss(b,a);

A
B
C
D

syms s
Phi = inv(s*eye(3) - A);
G = C * Phi * B + D;
[n,d] = numden(G)

```

* 출력

<img src="https://ifh.cc/g/DbJG0H.png" width="400" height="400"/>

## P3.12
전달함수가 $\frac{Y(s)}{R(s)} = T(s) = \frac{8(s+5)}{s^3 + 12s^2 + 44s + 48}$ 인스템에서 (a) 상태공간모델으르 구하라. (b) 상태천이행렬 $\Phi(t)$를 구하라.

<img src="https://ifh.cc/g/xwXNoY.jpg" width="400" height="150"/>

### 풀이

__(a) 상태공간모델을 구하라.__

상태공간모델은

$$
\dot{x} = \begin{bmatrix} 0 & 1 & 0 \\
1 & 0 & 0\\
-12 & -44 & -48 \end{bmatrix}x + \begin{bmatrix} 0 \\
0 \\
1 \end{bmatrix}r
$$

$$
y = \begin{bmatrix} 48 & 8 & 0\end{bmatrix}x
$$

이다.

__(b) 상태천이행렬 $\Phi(t)$를 구하라.__

$$
\Phi(t) = \begin{bmatrix} \Phi_1(t) \vdots \Phi_2(t) \vdots \Phi3(t)\end{bmatrix}
$$


$$
\Phi_1(t) = \begin{bmatrix} e^{-6t} - 3e^{-4t} + 3e^{-2t} \\
-6e^{-6t} - 12e^{-4t} - 6e^{-2t} \\
36e^{-6t} - 48e^{-4t} + 12e^{-2t} \end{bmatrix}
$$


$$
\Phi_2(t) = \begin{bmatrix} \frac{3}{4}e^{-6t} - 2e^{-4t} + \frac{5}{4}e^{-2t} \\
-\frac{9}{2}e^{-6t} + 8e^{-4t} - \frac{5}{2}e^{-2t} \\
27e^{-6t} - 32e^{-4t} + 5e^{-2t} \end{bmatrix}
$$


$$
\Phi_3(t) = \begin{bmatrix} \frac{1}{8}e^{-6t} - \frac{1}{4}e^{-4t} + \frac{1}{8}e^{-2t} \\
-\frac{3}{4}e^{-6t} - e^{-4t} - \frac{1}{4}e^{-2t} \\
\frac{9}{2}e^{-6t} - 4e^{-4t} + \frac{1}{2}e^{-2t} \end{bmatrix}
$$

__위 풀이를 matlab으로 표현하면 아래와 같다.__
* 코드
```matlab
b = [0 0 8 40];
a = [1 12 44 48];

[A,B,C,D] = tf2ss(b,a);
A
B
C
D

syms s
Phi = inv(s*eye(3) - A);
G = C * Phi * B + D;
[n,d] = numden(G)

num = sym2poly(n)
den = sym2poly(d)
[A, B, C, D] = tf2ss(num, den)

PI = ilaplace(G)
```

* 출력

<img src="https://ifh.cc/g/vZpff4.png" width="400" height="600"/>


## P3.17
다음과 같은 상태변수 방정식으로 표현된 시스템이 있다.

$$
\dot{x} = \begin{bmatrix} 1 & 1 & -1\\
4 & 3 & 0\\
-2 & 1 & 10 \end{bmatrix}x(t) + \begin{bmatrix} 0\\
0\\
4 \end{bmatrix}u(t)
$$

$$
y(t) = \begin{bmatrix} 1 & 0 & 0 \end{bmatrix}x(t)
$$

$G(s) = Y(s)/U(s)$를 구하라.

<img src="https://ifh.cc/g/h0hGVS.jpg" width="400" height="200"/>

### 풀이

상태공간 모델부터 설정하면

$$
\dot{x} = Ax(t) + Bu(t), y(t) = Cx(t) + Du(t)
$$

가 되고 여기에 라플라스 변환을 취해주게 되면

$$
sIX(s) = AX(s) + BU(S), Y(s) = CX(s) + DU(s)
$$

가 된다. 여기에 $sIX(s) = AX(s) + BU(S)$를 $X(s)$에 대한 식으로 전환하여 $Y(s)$식에 대입하게 되면

$$
X(s) = \frac{BU(s)}{sI-A} = \Phi BU(s)
$$

$$
Y(s) = CX(s) = \Phi BCU(s)
$$

이러한 상태변수방정식으로 표현할 수 있으며 

$$
\dot{x} = \begin{bmatrix} 1 & 1 & -1\\
4 & 3 & 0\\
-2 & 1 & 10 \end{bmatrix}x(t) + \begin{bmatrix} 0\\
0\\
4 \end{bmatrix}u(t)
$$

$$
y(t) = \begin{bmatrix} 1 & 0 & 0 \end{bmatrix}x(t)
$$

에서 전달함수는

$$
G(s) = C(sI-A)^{-1}B = \frac{-4s+12}{s^3 - 14s^2 + 37s +20}
$$

가 된다.

__위 풀이를 matlab으로 표현하면 아래와 같다.__

* 코드


```matlab
syms s
A = [1, 1, -1; 4, 3, 0; -2, 1, 10];
B = [0; 0; 4];
C = [1, 0, 0];
D = 0;
Phi = inv(s*eye(3) - A);
G = C*Phi*B+D;
[n,d] = numden(G)
```

* 결과


<img src="https://ifh.cc/g/mLckDt.png" width="400" height="200"/>








