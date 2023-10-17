# 제어공학1_Chapter3_Assignment

## P3.1
그림 P3.1에 스프링-질량-감쇠기 시스템이 주여져 있다. (a) 적당한 상태변수를 설정하라. (b) 상태변수로 표현된 1차 미분방정식을 구하라. (c) 상태미분방정식을 구하라.

<img src="https://ifh.cc/g/wXFAok.jpg" width="600" height="200"/>

### 풀이
__(a) 적당한 상태변수를 설정하라.__

스피링-질량-감쇠기는 뉴턴의 제 2법칙으로, 시스템을 표현하기 위한 충분한 상태변수는 질량의 위치와 속도이므로

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

폐루프의 전달함수는 

$$
T(s) = \frac{Y(s)}{R(s)} = \frac{s+2}{s+8} \cdot \frac{1}{s-3} \cdot \frac{1}{s} = \frac{s+2}{s^3+5s^2-24s}
$$

가 된다.

__(b) 상태변수 모델을 구할고 위상변수형 블록선도를 작성하라.__

matrix differential equation은

$$
A = \begin{bmatrix} 0 & 1 & 0 \\
0 & 0 & 1 \\
-2 & 23 & -5 \end{bmatrix}
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

## P3.12
전달함수가 $\frac{Y(s)}{R(s)} = T(s) = \frac{8(s+5)}{s^3 + 12s^2 + 44s + 48}$ 인스템에서 (a) 상태공간모델으르 구하라. (b) 상태천이행렬 $\Phi(t)$를 구하라.













