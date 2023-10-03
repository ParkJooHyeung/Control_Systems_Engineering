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

