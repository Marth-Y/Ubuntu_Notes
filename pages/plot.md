- `import matplotlib.pyplot as plt`
- 直方图 #plot
	- `hist`
	- `data`：要绘制直方图的数据。
	- `bins`（可选）：直方图的柱子数量，默认为 10。在这个例子中，`bins=200` 表示有 200 个柱子。
	- `density`（可选）：如果为 `True`，则将直方图归一化，使得总面积为 1，即概率密度。默认为 `False`。
	- `histtype`（可选）：直方图的类型。可以是 `'bar'`、`'barstacked'`、`'step'`、`'stepfilled'`。在这个例子中，`histtype='step'` 表示绘制一个不填充的线条直方图。
	- `lw`（可选）：线条的宽度。在这个例子中，`lw=2` 表示线条宽度为 2。
	- ```python
	  plt.hist(data, bins=200, density=True, histtype='step', lw=2)
	  ```
-