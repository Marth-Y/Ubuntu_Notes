- c++ 11
- # 为什么要有constexpr？
  collapsed:: true
	- 在 `constexpr` 之前已经有了const关键字定义常量，但是没有一种方法能明确的告诉编译器在编译阶段就计算出结果。
	- ## const和宏常量的不确定性 #define
		- const和宏定义的常量无法确保在编译期就被计算出，换而言之就是const定义的常量有两种情况：编译期常量和运行期常量。
		- 例：
			- ```cpp
			  // 编译期常量
			  const int x = 5;
			  #define x 5
			  int a[x]; // √
			  
			  // 运行期常量,需要运行调用函数后才能赋值常量x
			  int getSize() {
			    return 5;
			  }
			  const int x = getSize();
			  #define x getSize()
			  int a[x]; // × error
			  ```
	- 因此为了提高运行效率，我们需要明确指出某个值是编译期常量，因此C++11引入了 constexpr
		- ### 标准库举例
			- 在原来C`<limits.h>`头文件中，最大值用宏定义实现：
				- ```cpp
				  #define UCHAR_MAX 0xff // unsigned char最大值
				  ```
			- cpp标准库中有一个`<limits>`的头文件，其内定义了某一种数值的最大值：
				- ```cpp
				  std::numeric_limits<unsigned char>::max()
				  ```
			- cpp中的实现就是一个运行时常量了。后来有了constexpr，标准库做了优化，可以是编译期常量了。
- # How to ues ?
  collapsed:: true
	- ## constexpr值
		- constexpr值即常量表达式值，是一个用constexpr说明符声明的变量或者数据成员，它要求该值必须在编译期计算，因此，常量表达式的值必须被常量表达式初始化。
			- 例：
				- ```cpp
				  constexpr int x = 43;
				  int a[x]; // √
				  
				  constexpr int x = getSize(); // error getSize不是常量表达式
				  ```
	- ## constexpr函数
		- constexpr函数即常量表达式函数，在编译期间就可以计算出结果的函数（C++11。后续C++14中有所放宽，见下文）
			- 函数必须返回一个值
			  logseq.order-list-type:: number
			- 函数体必须只有一条语句：`return expr;`其中`expr`必须也是一个常量表达式。如果函数有形参，则将形参替换到expr中后，expr仍然必须是一个常量表达式。
			  logseq.order-list-type:: number
			- 函数使用之前必须有定义。
			  logseq.order-list-type:: number
			- 函数必须用constexpr声明。
			  logseq.order-list-type:: number
		- 例：
			- ```cpp
			  constexpr int max_unsigned_char()
			  {
			    return 0xff;
			  }
			  
			  constexpr int square(int x) // 接受常量则成立
			  {
			    return x * x;
			  }
			  
			  constexpr int abs(int x)
			  {
			    return x > 0 ? x : -x;
			  }
			  
			  int main()
			  {
			    char buffer1[max_unsigned_char()] = { 0 };
			    char buffer2[square(5)] = { 0 };
			    char buffer3[abs(-8)] = { 0 };
			  }
			  ```
		- 有趣的是：
			- ```cpp
			  constexpr int get(int x) {
			      return ++x;
			  }
			  
			  int main() {
			      constexpr int x = get(5);
			  }
			  
			  $ g++ test.cc -o test --std=c++11
			  test.cc: In function ‘constexpr int get(int)’:
			  test.cc:6:12: error: expression ‘++ x’ is not a constant expression
			      6 |     return ++x;
			        |            ^~~
			  $ g++ test.cc -o test --std=c++14
			  $ 
			  ```
			- C++11中不认为`++x`是常量表达式，所以在C++11中无法编译通过，但是C++14可以编译通过
		- ### 条件语句与循环语句
			- constexpr函数只支持一条返回语句，因此条件语句只能用条件运算符代替，循环可以用递归代替。
				- ```cpp
				  constexpr int abs2(int x)
				  {
				    if (x > 0) {
				         return x;
				    } else {
				         return -x;
				    }
				  }
				  ------------------------条件运算符
				  constexpr int abs2(int x)
				  {
				    return x > 0 ? x : -x;
				  }
				  
				  ------------------------------------------------------
				  constexpr int sum(int x)
				  {
				    int result = 0;
				    while (x > 0)
				    {
				         result += x--;
				    }
				    return result;
				  }
				  ------------------------递归
				  constexpr int sum(int x)
				  {
				    return x > 0 ? x + sum(x - 1) : 0;
				  }
				  ```
		- constexpr函数的行为并不是向constexpr值一样确定的。
			- ==大白话：constexpr函数只是提醒编译器在编译期求值，能求就求，求不了就退化==
				- 带形参的常量表达式函数接受了一个非常量实参时，常量表达式函数可能会退化为普通函数：
				- ```cpp
				  constexpr int square(int x)
				  {
				    return x * x;
				  }
				  
				  int x = 5;
				  std::cout << square(x); // 肯能退化，具体看编译器的处理。GCC这里不会退化
				  ```
-
-
- # constexpr与const对比
  collapsed:: true
	- ## 都可以定义编译期常量
		- ```cpp
		  constexpr int x = 4;
		  int a[x];
		  ```
	- ## const可以定义运行期常量
		- ```cpp
		  const     int x = getSize(); // √
		  constexpr int x = getSize(); // ×
		  ```
	- constexpr是一个加强版的const，它不仅要求常量表达式是常量，并且要求是一个编译阶段就能够确定其值的常量。
-