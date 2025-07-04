---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'



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

## Embedded Files
38813f96d4f6ef9937cae93da9d5d617642d0a7d: [[Pasted Image 20250615223849_853.png]]

%%
## Drawing
```compressed-json
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
```
%%