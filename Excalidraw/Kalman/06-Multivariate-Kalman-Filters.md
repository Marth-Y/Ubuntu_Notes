---
excalidraw-plugin: parsed
tags:
  - excalidraw
  - kalman
---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'

#kalman #excalidraw 

# 23

```import math
import numpy as np
from numpy.random import randn

def compute_dog_data(z_var, process_var, count=1, dt=1.):
    "returns track, measurements 1D ndarrays"
    x, vel = 0., 1.
    z_std = math.sqrt(z_var) 
    p_std = math.sqrt(process_var)
    xs, zs = [], []
    for _ in range(count):
        v = vel + (randn() * p_std)
        x += v*dt        
        xs.append(x)
        zs.append(x + randn() * z_std)        
    return np.array(xs), np.array(zs)
import math
import numpy as np
from numpy.random import randn

def compute_dog_data(z_var, process_var, count=1, dt=1.):
    "returns track, measurements 1D ndarrays"
    x, vel = 0., 1.
    z_std = math.sqrt(z_var) 
    p_std = math.sqrt(process_var)
    xs, zs = [], []
    for _ in range(count):
        v = vel + (randn() * p_std)
        x += v*dt        
        xs.append(x)
        zs.append(x + randn() * z_std)        
    return np.array(xs), np.array(zs)
```


# import math
import numpy as np
from numpy.random import randn

def compute_dog_data(z_var, process_var, count=1, dt=1.):
    "returns track, measurements 1D ndarrays"
    x, vel = 0., 1.
    z_std = math.sqrt(z_var) 
    p_std = math.sqrt(process_var)
    xs, zs = [], []
    for _ in range(count):
        v = vel + (randn() * p_std)
        x += v*dt        
        xs.append(x)
        zs.append(x + randn() * z_std)        
    return np.array(xs), np.array(zs)

```Python
import math
import numpy as np
from numpy.random import randn

def compute_dog_data(z_var, process_var, count=1, dt=1.):
    "returns track, measurements 1D ndarrays"
    x, vel = 0., 1.
    z_std = math.sqrt(z_var) 
    p_std = math.sqrt(process_var)
    xs, zs = [], []
    for _ in range(count):
        v = vel + (randn() * p_std)
        x += v*dt        
        xs.append(x)
        zs.append(x + randn() * z_std)        
    return np.array(xs), np.array(zs)
```


# import math
import numpy as np
from numpy.random import randn

def compute_dog_data(z_var, process_var, count=1, dt=1.):
    "returns track, measurements 1D ndarrays"
    x, vel = 0., 1.
    z_std = math.sqrt(z_var) 
    p_std = math.sqrt(process_var)
    xs, zs = [], []
    for _ in range(count):
        v = vel + (randn() * p_std)
        x += v*dt        
        xs.append(x)
        zs.append(x + randn() * z_std)        
    return np.array(xs), np.array(zs)

```python
import math
import numpy as np
from numpy.random import randn

def compute_dog_data(z_var, process_var, count=1, dt=1.):
    "returns track, measurements 1D ndarrays"
    x, vel = 0., 1.
    z_std = math.sqrt(z_var) 
    p_std = math.sqrt(process_var)
    xs, zs = [], []
    for _ in range(count):
        v = vel + (randn() * p_std)
        x += v*dt        
        xs.append(x)
        zs.append(x + randn() * z_std)        
    return np.array(xs), np.array(zs)
```

# Excalidraw Data

## Text Elements
import math
import numpy as np
from numpy.random import randn

def compute_dog_data(z_var, process_var, count=1, dt=1.):
    "returns track, measurements 1D ndarrays"
    x, vel = 0., 1.
    z_std = math.sqrt(z_var) 
    p_std = math.sqrt(process_var)
    xs, zs = [], []
    for _ in range(count):
        v = vel + (randn() * p_std)
        x += v*dt        
        xs.append(x)
        zs.append(x + randn() * z_std)        
    return np.array(xs), np.array(zs) ^A8ntmPCm

跟踪一只狗 ^MsJ8m2cM

1. 模拟狗的运动生成每一步的测试数据 ^PhCPYVGT

一、Predict ^8UmRISgL

2. 初始状态设计 ^kduIIKLr

x = np.array([[10.0],
              [4.5]]) ^YbaSN8Up

初始位置为0,初始速度为1
每一步根据过程噪声更新速度和位置
添加测量噪声生成观测值 ^6USERUIH

状态向量包含两个变量:：
1. 位置 x
2. 速度 dx/dt。这是一个重要的设计决策,引入速度作为隐藏变量可以提高滤波精度。
这里初始位置为10，初始速度为4.5m/s ^mwbP0urq

3. 初始状态协方差设计 ^zdErp3uu

P = np.array([[500., 0.],
              [0., 49.]]) ^Zyr0SGCt

初始状态协方差矩阵:
P[0,0]=500 表示位置的初始不确定性
P[1,1]=49 表示速度的初始不确定性
对角线以外的元素为0,表示位置和速度最初没有相关性 ^882787lk

4. 过程模型设计 ^sMnkBRn6

F = np.array([[1, dt],
              [0, 1]]) ^DIBjUCPk

状态转移矩阵F:
新位置 = 旧位置 + 速度×时间
新速度 = 旧速度(假设速度保持不变) ^6yPW7Sp7

5. 过程噪声设计 ^khsE2lGZ

使用Q_discrete_white_noise函数生成过程噪声协方差矩阵Q,用于表示过程中的不确定性。 ^PDWjyf3o

from filterpy.common import Q_discrete_white_noise
Q = Q_discrete_white_noise(dim=2, dt=1., var=2.35)
print(Q) ^VneU0RBL

[[0.588 1.175]
 [1.175 2.35 ]] ^R4cmZkws

6. 设计控制函数 ^Ie2Fo03Y

     卡尔曼滤波器不只是对数据进行滤波，它还能让我们将诸如机器人和飞机这类系统的控制输入纳入其中。
假设我们正在控制一个机器人。在每个时间步长，我们会根据机器人当前的位置与期望位置向其发送转向和速度信号。
卡尔曼滤波器的方程将这些知识融入到滤波器方程中，基于当前速度和驱动电机的控制输入来预测位置。
请记住，我们绝不会丢弃任何信息。 ^UVbyzvVI

B = 0.  # my dog doesn't listen to me!
u = 0
x, P = predict(x, P, F, Q, B, u)
print('x =', x)
print('P =', P) ^jNAxlysD

Predict步骤总结 ^uoeSTG2L

预测步骤的主要任务就是设计以下矩阵 ^I3A8i9rh

x、P：初始状态和协方差 ^1JqHDEh3

F、Q：状态转移函数和过程噪声协方差 ^kGU6Iy5J

B、μ：可选的。控制输入和控制输入函数 ^YcYJnrb2

二、Update ^4bI4IYw9

1. 设计测量函数H ^nrGcPdfx

在更新步骤中，我们需要计算残差residual = measured - predicted。测量值是通过传感器等获取到的。那么就会有一个问题：
传感器获取到的值和predicted，也就是我们需要滤波的对象单位可能不一样。需要进行一些换算。也有可能是我们的测量值
和跟踪的状态矩阵数量不一样。我们也需要做一些变换，如测量值只有position x，而跟踪的状态有x和速度v。
因此有测量函数H。
一般将预测值向测量值单位转换。因为测量值无法转换出我们跟踪的隐藏状态。如：测量出的是position x，无法转换出我们
跟踪的速度状态。而我们的预测值很容易就能得到position ^Uari0MYk

速度是一个隐藏状态，在这里没有用传感器直接获得，而是通过位移来计算的 ^PRx5Gnos

H = np.array([[1.,0.]]) ^WpMdBqZB

2. 生成测试值以及测量噪声协方差矩阵 ^fzq54Cpg

测量值z就一是要给一维的vector。如果只有一个传感器读数，则z就是1x1的vector。如果有两个，则z就是2x1的vector ^vS3Dp4Nd

Kalman滤波中用R表示测量噪声协方差。其表征各个传感器数值之间的关系，以及传感器的误差 ^3U0N8Vvc

如果只有一个传感器，则R = [σ²] ^pWXnKXhi

R = np.array([[5.]]) ^W7zqmkYF

from filterpy.kalman import update
z = 1.
x, P = update(x, P, z, R, H)
print('x =', x) ^2Q6JMYQM

## Embedded Files
38813f96d4f6ef9937cae93da9d5d617642d0a7d: [[Pasted Image 20250615223849_853.png]]

cfd380ea8fc06c04f49f35a212c72e5c3ab2aa68: [[Pasted Image 20250621150337_546.png]]

1d02dfd896729abfde653fc07eafbc6f423f402e: [[Pasted Image 20250621152426_243.png]]

d8fc3ec1b602bc71fee2cc906bb8702cb1f7a952: [[Pasted Image 20250621152547_791.png]]

9ec9ac4390bf8e37a2838d90b9d4fba36e9b7ab6: [[Pasted Image 20250621153436_692.png]]

0c8d5220610de74a88c8574dc0c7dcb27270c836: [[Pasted Image 20250621153848_659.png]]

%%
## Drawing
```compressed-json
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
```
%%