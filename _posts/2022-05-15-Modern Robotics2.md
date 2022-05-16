---
title: Modern Robotics, Course1
subtitle: Modern Robotics Chapter 2 - Configuration Space
tags: [study, robotics]
---

# 2.1 Degrees of Freedom of a Rigid Body (강체의 자유도)  
<br>

로봇을 다룰 때 필요한 가장 기초는 '로봇이 어디에 있는가?'입니다. 이때 필요한 것이 로봇의 위치(Configuration)이죠.  
이 강의에서는 로봇의 몸체가 단단한 물체(강체, rigid body)인 상태에 대해서만 살펴봅니다. 이 로봇의 몸체를 link라 부르는데 link는 나무토막처럼 일정한 형태를 갖기에 몇개의 숫자로 위치를 표현할 수 있습니다.  
<br>

로봇의 가능한 모든 위치를 포함하는 n차원 공간을 **Configuration Space** (C-space)라고 합니다.  
**dof(degrees of freedom)**는 C-space의 차원이라고 할 수 있고, 로봇의 위치를 표현하기 위해 필요한 숫자의 갯수라고도 할 수 있습니다.  
<br>

책의 p.32 Figure 2.1을 보면  
![MR Figure 2.1](/assets/images/MR Figure 2.1.png)
(a)의 문은 그 위치를 표현하기 위해 경첩을 기준으로 얼마나 회전했는지에 대한 각도 1개만 있으면 됩니다.  
(b)의 점은 평면 상의 점이므로 점의 좌표인 x, y 2개의 값으로 위치를 표현할 수 있습니다.  
(c)의 동전은 동전위의 한 점의 x,y 좌표와 동전이 기울어진 정도 (각도) 3개의 값으로 위치를 표현할 수 있습니다.  
<br>

Figure 2.2를 통해 강체의 자유도를 알아봅시다.  
(b)에서 점 A, B, C는 모두 각각 2개의 좌표(값)로 표현가능합니다. {(x<sub>A</sub>, y<sub>A</sub>), (x<sub>B</sub>, y<sub>B</sub>), (x<sub>C</sub>, y<sub>C</sub>)} 6개의 임의의 값(독립적인 값, independent)으로 동전의 위치를 정할 수 있으면 이는 6의 dof를 갖는 것입니다.  
하지만 동전은 강체(rigid)이므로 A가 정해지면 A,B 간의 거리(d(A, B))가 일정함에 의해 B의 위치가 제한(constraint)됩니다. 그 위치는 A를 중심으로 하고 반지름의 d<sub>AB</sub>인 원 위이죠.  
이때 B의 위치는 phi<sub>AB</sub>(AB벡터와 x축 벡터가 이루는 각)하나로 표현이 가능합니다. 이후 점 C의 위치는 원AC, 원BC의 두 교점에서 가능한데, 이는 동전의 앞, 뒤에 따른 것이므로 사전에 동전의 면을 지정하면 C의 위치는 명백해집니다(C is fixed).  
따라서 동전의 평면에서의 위치(configuration)는 (x<sub>A</sub>, y<sub>A</sub>, phi<sub>AB</sub>) 이렇게 표현이 가능하고 3의 dof를 갖는다는 걸 알 수 있습니다.  
<br>

이 예를 일반적인 규칙으로 적용하면 dof에 대한 공식을 얻습니다.(식 2.1)    
dof = 지점들의 자유도의 합 - 제한들(constraints)의 갯수  
<br>

위의 예를 적용시켜보면 동전 위 지점들의 자유도 합은 A, B, C 모두 x, y값을 가지므로 2+2+2 = 6의 자유도를 갖습니다. 한편 A가 정해지면 B는 A에 의해 d(A,B)라는 1개의 constraint가 생기고, 마찬가지로 C는 A, B에 의해 2개의 constraints가 생깁니다. 따라서 1+2 = 3의 constraints(제한)이 있어 평면 위 동전의 자유도(dof)는 6-3 = 3이 되는 것입니다.  
<br>

이를 확장해 3차원 공간에서 동전의 위치를 생각해봅시다.(Figure 2.2(c))  
점 A, B, C는 모두 x,y,z좌표를 가질 수 있으므로 총 9의 자유도를 가집니다. 한편 A가 정해지면 B는 A에 의해 1개의 constraint를 갖고, C는 A, B에 의해 2개의 constraints를 갖게 되므로 3차원 공간에서 동전의 dof는 9 - 3 = 6이 됩니다.  
같은 예를 조금 다르게 살펴보면 점 A는 x,y,z 좌표를 자유롭게 선택 가능해 3의 자유도를 가집니다. 점 B도 x,y,z 좌표로 표현이 가능하나 A로 인한 1개의 constraint를 가지기 때문에 B는 3-1=2의 자유도를 가진다고 할 수 있습니다. 마찬가지로 점 C도 x,y,z 좌표를 가지지만 2개의 constraints를 갖기 때문에 C는 3-2=1의 자유도를 가집니다. 따라서 3차원 공간 위 동전의 자유도는 3+2+1=6이라고 할 수 있습니다.