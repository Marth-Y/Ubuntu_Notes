- 取随机值 #numpy
	- 我的理解：不同的随机数种子对应了一组固定的伪随机数，这样是为了可重复实验。使得数据是随机的，但是是可复现的。
	- 可以设置随机数种子，以取不同的随机数序列。
	- ```python
	  N = 1000000
	  for r in np.random.rand(N):
	  ```
- 计算中位数 #numpy
	- ```python
	  x = {1.8, 2.0, 1.7, 1.9, 1.6}
	  np.median(x) # 1.8
	  ```
- 均值 #numpy
	- ```python
	  np.mean(x)
	  ```
- 求和 #numpy
	- ```python
	  np.sum(belief)
	  ```
- 方差 #numpy
	- ```python
	  print(f"{np.var(X):.2f} meters squared")
	  :.2f表示保留两位小数，f表示浮点数
	  ```
-