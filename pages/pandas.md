# 生成csv文件 #python
	- ```python
	  import os
	  data_file = os.path.join('./house_tiny.csv') 
	  with open(data_file, 'w') as f:
	      f.write('NumRooms,Alley,Price\n')
	      # 列名
	      f.write('NA,Pave,127500\n')
	      # 每行表示一个数据样本
	      f.write('2,NA,106000\n') 
	      f.write('4,NA,178100\n') 
	      f.write('NA,NA,140000\n')
	  
	  ```
- # 使用pandas直接读取csv #python
	- ```python
	  import pandas as pd
	  import os
	  
	  data_file = os.path.join('04\house_tiny.csv')
	  
	  data = pd.read_csv(data_file)
	  print(data)
	  
	  ------
	     NumRooms Alley   Price
	  0       NaN  Pave  127500
	  1       2.0   NaN  106000
	  2       4.0   NaN  178100
	  3       NaN   NaN  140000
	  ```
	- ## 处理缺失值
		- 从结果来看有很多缺失值：`NaN`。为了处理缺失的数据，典型的方法包括插值法和删除法，其中插值法用一个替代值弥补缺失值，而删除法则直接忽略缺失值。
		- 对`pandas`的索引切切片需要加上`.iloc[]`
			- `inputs.iloc[:,0]`取列只会有数值，不会有列名
			- `inputs.iloc[0,:]`取的是列明
		- ```python
		  // 插值法：使用每列均值填充
		  inputs, outputs = data.iloc[:, 0:2], data.iloc[:, 2] 
		  inputs = inputs.fillna(inputs.mean())
		  print(inputs)
		  
		  	NumRooms Alley
		  0		 3.0 Pave
		  1		 2.0 NaN
		  2		 4.0 NaN
		  3		 3.0 NaN
		  
		  对Alley来说只接受两种类型：Pave NaN，pandas可以自动将此列转换为两列“Alley_Pave”和“Alley_nan”。
		  巷子类型为“Pave”的行会将“Alley_Pave”的值设置为1，“Alley_nan”的值设置为0。
		  缺少巷子类型的行会将“Alley_Pave”和“Alley_nan”分别设置为0和1。
		  
		  inputs = pd.get_dummies(inputs, dummy_na=True) 
		  print(inputs)
		  
		     NumRooms  Alley_Pave  Alley_nan
		  0       3.0        True      False
		  1       2.0       False       True
		  2       4.0       False       True
		  3       3.0       False       True
		  ```
		- ### practice 删除缺失值最多的列
			- ```cpp
			  # 计算每一列的缺失值数量
			  missing_values = data.isnull().sum()
			  
			  # 找出缺失值最多的列
			  max_missing_column = missing_values.idxmax()
			  
			  # 删除缺失值最多的列
			  df = data.drop(columns=max_missing_column)
			  print(df)
			    
			  ---删除前
			     NumRooms Alley   Price
			  0       NaN  Pave  127500
			  1       2.0   NaN  106000
			  2       4.0   NaN  178100
			  3       NaN   NaN  140000
			  ---删除后
			     NumRooms   Price
			  0       NaN  127500
			  1       2.0  106000
			  2       4.0  178100
			  3       NaN  140000
			  ```
		-
-
-
-