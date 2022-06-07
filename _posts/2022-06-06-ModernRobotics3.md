---
title: Modern Robotics, Course1 / Chapter 3
subtitle: Modern Robotics Chapter 3 - Rigid-Body Motions
toc: true
toc_label: "내용 목차"
tags: [study, robotics]
---

---
# 3.1 Rigid-Body Motions in the Plane (평면에서 강체의 움직임)  
<br>

![Figure 3.3](/assets/images/MR Figure 3.3.png)  
<br>

Figure 3.3에서 평면 몸체(회색 부분)를 봐봅시다.  
그림에서처럼 단위축 $\hat{x}_s,\, \hat{y}_s$를 갖는 고정된 기준틀(reference frame) $\{s\}$이 있을 때 비슷하게 단위축 $\hat{x}_b,\, \hat{y}_b$를 갖는 평면몸체의 기준틀을 지정할 수 있습니다.(책에서 hat표기는 단위벡터를 의미합니다.)  
그 틀을 body frame이라 하고 $\{b\}$로 표기합니다.  
<br>

평면 몸체의 **위치(position)** 를 설명하기 위해서는 고정된 기준틀(fixed frame)에 대한 몸체의 위치(position)와 방향(orientation)만으로 충분합니다.  
Figure 3.3에서 $\{b\}$의 원점인 $p$는 $\{s\}$의 좌표축을 이용해 다음과 같이 쓸 수 있습니다.  

$$
p = p_x \hat{x}_s\, +\, p_y \hat{y}_s 
\tag{3.1}
$$  


일반적으로 $p$벡터를 $p = (p_x,p_y)$로 표기하지만 이 방식은 기준틀(reference frame)이 모호해지는 단점이 있습니다.  
따라서 식 3.1과 같이 표기해 $(p_x,p_y)$가 어떤 기준틀에서 정의되었는지 확실하게 명시할 수 있습니다.  
<br>

다음으로 고정된 frame $\{s\}$에 대한 몸체의 frame $\{b\}$의 **방향(orientation)** 은 Figure 3.3에서 각 $\theta$를 통해 설명할 수 있습니다.  
$\{b\}$의 단위 벡터 $\hat{x}_b ,\, \hat{y}_b$를 $\{s\}$의 그것들로 표현하면 다음과 같습니다.  

$$
\begin{aligned}
\hat{x}_b &= cos\theta\hat{x}_s + sin\theta\hat{y}_s,\\
\hat{y}_b &= -sin\theta\hat{x}_s + cos\theta\hat{y}_s
\end{aligned}
$$  

$p$의 모든 성분을 $\{s\}$에 대해 쓰기로 하면 열벡터 $p \in \R^2$는  

$$
p = \begin{bmatrix} p_x \\ p_y \end{bmatrix}
$$  

이고 두 벡터 $\hat{x}_b ,\, \hat{y}_b$또한 열벡터로 쓸 수 있기 때문에 이들을 모아 $2 \times 2$ 행렬 $P$로 쓰면 다음과 같습니다.  

$$
P = \begin{bmatrix} \hat{x}_b & \hat{y}_b \end{bmatrix} = \begin{bmatrix} cos\theta & -sin\theta \\ sin\theta & cos\theta \end{bmatrix}
$$  
<br>

행렬 $P$는 **회전 행렬(rotation matrix)** 의 한 예시입니다.  
순서쌍 $(P,p)$는 $\{s\}$에 대한 $\{b\}$의 방향과 위치에 대한 정보입니다.  
<br>

![Figure 3.4](/assets/images/MR Figure 3.4.png)  
<br>

Figure 3.4에 있는 3개의 frame을 봅시다.  
위의 방식을 똑같이 적용하면 다음과 같은 $\{s\}$에 대한 $\{c\}$의 정보인 순서쌍 $(R,r)$을 얻을 수 있습니다.

$$
r = \begin{bmatrix}
    r_x \\
    r_y
\end{bmatrix},
\qquad
R = \begin{bmatrix}
    cos\phi & -sin\phi \\
    sin\phi & cos \phi
\end{bmatrix}
$$

또 frame $\{c\}$를 $\{b\}$에 대해 쓸 수 있습니다.  
$q$를 $\{b\}$의 좌표로 표현된 $\{b\}$의 원점으로부터 $\{c\}$의 원점까지의 벡터라 하고, $Q$를 $\{b\}$에 대한 $\{c\}$의 방향(orientation)이라 하면 다음과 같은 순서쌍 $(Q,q)$를 얻을 수 있습니다.  

$$
q = \begin{bmatrix}
    q_x \\
    q_y
\end{bmatrix},
\qquad
Q = \begin{bmatrix}
    cos\psi & -sin\psi \\
    sin\psi & cos \psi
\end{bmatrix}
$$

$(Q,q)$ ($\{b\}$에 대한 $\{c\}$의 위치)와 $(P,p)$ ($\{s\}$에 대한 $\{b\}$의 위치)를 알고 있다면, 다음과 같이 $\{s\}$에 대한 $\{c\}$의 위치를 계산해낼 수 있습니다.  

$$
R = PQ \tag{3.8}
$$
$$
r = Pq + p \tag{3.9}
$$
식(3.8)은 $Q$를 $\{s\}$ frame에 대한 것으로 변환한 것이고,  
식(3.9)는 $q$를 $\{s\}$ frame에 대해 변환하고 $p$와 벡터합 한 것입니다.  
<br>

![Figure 3.5](/assets/images/MR Figure 3.5.png)  
<br>

두개의 frame $\{d\}, \{c\}$이 붙어있는 강체(rigid body)에 대해 생각해봅시다.  
$\{d\}$는 초기에 $\{s\}$와 동일한 위치에 있고, $\{c\}$는 $\{s\}$에 대해 $(R,r)$로 표현됩니다.  
<br>

그리고 몸체가 움직여 $\{d\}$는 $\{d'\}$으로 움직여 $\{b\}$ ($\{s\}$에 대해 $(P,p)$로 표현)와 일치하게 되었습니다.  
이런 움직임 이후에 $\{c\}$는 어디로 위치하게 될지 알아봅시다.  
<br>

$\{c\}$의 도착 위치를 $\{c'\}$라 하고 이 frame의 위치를 $(R',r')$이라고 하면

$$
R' = PR \tag{3.10}
$$
$$
r' = Pr + p \tag{3.11}
$$
임을 알 수 있습니다.  
<br>

따라서 회전 행렬-벡터 쌍 $(P,p)$은 3가지 용도로 활용이 가능합니다.  

1. 강체(rigid body)의 위치(configuration)을 표현하기 위해 [Figure 3.3]
2. 벡터나 frame의 기준 frame (reference frame)을 바꾸기 위해 [Figure 3.4]
3. 벡터나 frame을 이동(displace)시키기 위해 [Figure 3.5(a)]
<br>

Figure 3.5의 움직임은 강체가 ①만큼 회전하고 ②만큼 평행운동 한 것으로 해석이 가능하지만, 다르게 보면 단순히 점 $s$를 기준으로 $\beta$만큼 회전 한 것으로도 볼 수 있습니다.  
이것은 하나의 평면 **나사 운동(screw motion)** 예시입니다.  
이 움직임은 세개의 변수 $(\beta, s_x, s_y)$로 표현될 수 있습니다.  
위의 예시에서는 $(s_x, s_y) = (0,2)$이겠군요.
<br>

screw motion을 표현하는 다른 방법은 motion을 회전과 직선 운동의 결합으로 표현하는 것입니다.  
Figure 3.5(b)를 보면 점 s를 기준으로 단위 각속도 $(\omega = 1\, rad/s)$ 만큼 회전하는 운동은 초기에 {$s$}의 원점이 {$s$} frame의 $+\hat{x}$방향으로 초당 2만큼 움직인다는 것을 알 수 있습니다. ($(v_x, v_y) = (2,0)$)  
<br>

이상을 하나의 **screw axis**인 벡터$S$로 표현하면
$$
S = (\omega, v_x, v_y) = (1, 2, 0)
$$
입니다.  
$S$를 따라 $\theta \over 2$만큼 이동하면 최종 지점에 도달합니다. 따라서 이 운동(움직임)을 $S\theta = (\pi/2, \pi, 0)$으로 표현할 수 있고 이것을 평면 강체의 움직임에 대한 **exponential coordinates**라고 합니다.  
<br>

---
# 3.2 Rotations and Angular Velocities  
<br>

## 3.2.1 Rotation Matrices (회전 행렬)