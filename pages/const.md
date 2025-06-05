- const和指针 #const
  id:: 65d604e7-6580-4230-a087-1ca03f46abe3
	- const 在`*`左边：指针指向的内容不能变
	- const 在 `*`右边：指针的指向不能变
- const成员函数
  id:: 65d605a7-94a5-4469-948d-104a3ebc6f83
	- 使得class接口容易被理解，得知这个函数不会修改对象内容。
	  logseq.order-list-type:: number
	- 操作const对象。
	  logseq.order-list-type:: number
- 遇到一个错误：
	- 我定义了`float a[2][40]`二维数组。
	- 直接用`float* x = a;`想要获取数组指针，报错：
		- `error: cannot convert 'float (*)[40]' to 'float*' in initialization`
	- 原因：a是一个二维数组，他的类型是`flota(*)[40]`(指向`float[40]`的指针)，编译器不允许隐式转换为`float*`
	- 解决：
		- 直接取首地址：`float* x = &a[0][0]`
		  logseq.order-list-type:: number
		- 取第一行首地址：`float* x = a[0]`
		  logseq.order-list-type:: number
-