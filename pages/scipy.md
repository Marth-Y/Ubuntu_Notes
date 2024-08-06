- 创建一个正态分布对象 #scipy  #Gaussian
	- `scipy.stats.norm`
	- ```python
	  from scipy.stats import norm
	  
	  # 创建一个正态分布对象
	  dist = norm(mean, std)
	  ```
	- 计算概率密度函数 pdf
		- 概率密度函数描述了连续随机变量X在各个取值上的概率密度。
		- 这里的概率密度函数就是高斯函数
		- ```python
		  x = 1.5
		  pdf_value = dist.pdf(x)
		  print(f"PDF at x={x}: {pdf_value}")
		  ```
	- 计算累积分布函数 cdf
		- 累积分布函数 F(x)描述了连续随机变量 X 小于或等于某个值 x 的概率。
		- 这里的累积分布函数就是对高斯函数的积分
		- ```python
		  x = 1.5
		  cdf_value = dist.cdf(x)
		  print(f"CDF at x={x}: {cdf_value}")
		  ```
	- 生成n个随机变量
		- ```python
		  random_samples = dist.rvs(size=10)
		  print(f"Random samples: {random_samples}")
		  ```
- 描述一个概率分布的形状 #scipy
	- `scipy.stats.describe(zs)`
	- ```python
	  DescribeResult(nobs=5000, minmax=(-0.19143741858944452, 20.804030812682086), mean=9.996901102331591, variance=2.7388116003856884, skewness=0.015276194207011526, kurtosis=1.622567142788295)
	  ```
	- `nobs`：数据集中的观测数（样本大小）。
	- `minmax`：数据集的最小值和最大值。
	- `mean`：数据集的算术平均值。
	- `variance`：数据集的方差，衡量数据的离散程度。
	- `skewness`：数据集的偏度，衡量数据分布的不对称性。
	- `kurtosis`：数据集的峰度，衡量数据分布的尖锐程度。
-