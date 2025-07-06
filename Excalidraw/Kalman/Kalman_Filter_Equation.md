---
excalidraw-plugin: parsed
tags:
  - excalidraw
  - kalman
---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'

#kalman #excalidraw 

# Excalidraw Data

## Text Elements
import numpy as np
import math
from numpy.random import randn
from filterpy.kalman import KalmanFilter
from filterpy.common import Q_discrete_white_noise
import sys 
from pathlib import Path 
sys.path.append(str(Path(__file__).resolve().parent.parent))
# from kf_book.mkf_internal import plot_track

def compute_dog_data(z_var, process_var, count=1, dt=1.):
    "returns track, measurements 1D ndarrays"
    x, vel = 0., 1.
    z_std = math.sqrt(z_var) 
    p_std = math.sqrt(process_var)
    xs, zs = [], []
    for _ in range(count):
        v = vel + (randn() * p_std)
        x += v*dt        
        xs.append(x) # 这里xs应该就是实际的位置
        zs.append(x + randn() * z_std) # zs是测量值，实际位置加上噪声
    return np.array(xs), np.array(zs)

def pos_vel_filter(x, P, R, Q=0., dt=1.0):
    """ Returns a KalmanFilter which implements a
    constant velocity model for a state [x dx].T
    """
    
    kf = KalmanFilter(dim_x=2, dim_z=1)
    kf.x = np.array([x[0], x[1]]) # location and velocity
    kf.F = np.array([[1., dt],
                     [0.,  1.]])  # state transition matrix
    kf.H = np.array([[1., 0]])    # Measurement function
    kf.R *= R                     # measurement uncertainty
    if np.isscalar(P):
        kf.P *= P                 # covariance matrix 
    else:
        kf.P[:] = P               # [:] makes deep copy
    if np.isscalar(Q):
        kf.Q = Q_discrete_white_noise(dim=2, dt=dt, var=Q)
    else:
        kf.Q[:] = Q
    return kf

dt = .1 # 0.1s
x = np.array([0., 0.]) 
kf = pos_vel_filter(x, P=500, R=5, Q=0.1, dt=dt)


def run(x0=(0.,0.), P=500, R=0, Q=0, dt=1.0, 
        track=None, zs=None,
        count=0, do_plot=True, **kwargs):
    """
    track is the actual position of the dog, zs are the 
    corresponding measurements. 
    """

    print(f'run: x0={x0}, P={P}, R={R}, Q={Q}, dt={dt}, count={count}')
    # Simulate dog if no data provided. 
    if zs is None:
        track, zs = compute_dog_data(R, Q, count)

    # create the Kalman filter
    kf = pos_vel_filter(x0, R=R, P=P, Q=Q, dt=dt)  
    print(kf)

    # run the kalman filter and store the results
    xs, cov = [], []
    for z in zs:
        kf.predict()
        kf.update(z)
        xs.append(kf.x)
        cov.append(kf.P)

    xs, cov = np.array(xs), np.array(cov)
    # if do_plot:
        # xs 滤波后的位置，track是实际位置，zs是测量值，cov是每一步的协方差
        # plot_track(xs[:, 0], track, zs, cov, **kwargs)
    return xs, cov

P = np.diag([500., 49.])
Ms, Ps = run(count=50, R=10, Q=0.01, P=P) ^lHgshmbn

kalman filter通用代码流程： ^fbmbrAI4

kalman filter equation 流程 ^dQYTEWrk

一、Predict Equation ^mSocQS4h

x平:预测的值
F:状态转移矩阵
x:当前状态值
B:控制输入模型(可选的)
u:控制输入(可选的) ^nvzxbaAP

1.均值x平： ^egk6G1x1

2.协方差 ^QRyx4cNM

## Embedded Files
2ee895ef76f988851b012dce5a776b9e18a07244: [[Pasted Image 20250622204740_787.png]]

%%
## Drawing
```compressed-json
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
```
%%