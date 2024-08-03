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
	- 生成随机变量
		- ```python
		  random_samples = dist.rvs(size=10)
		  print(f"Random samples: {random_samples}")
		  ```
-