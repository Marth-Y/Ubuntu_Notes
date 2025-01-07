- > 《现代C++语言核心特性解析》
- c++11
- # 为什么要有constexpr？
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
			- ++x改变了x的值，在下文会说到constexpr会自动为函数加上const属性
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
	- ## constexpr构造函数
		- constexpr也可以修饰常量自定义类型。因此需要对自定义类型的构造函数申明为constexpr的。
		- 例：
			- ```cpp
			  class X {
			  public:
			    X() : x1(5) {}
			    int get() const
			    {
			         return x1;
			    }
			  private:
			    int x1;
			  };
			  
			  constexpr X x;                    // 编译失败，X不是字面类型
			  char buffer[x.get()] = { 0 };     // 编译失败，x.get()无法在编译阶段计算
			  ```
		- constexpr构造函数构建规则：
			- 1. 构造函数必须用constexpr声明。
			- 2. 构造函数初始化列表中必须是常量表达式。
			- 3. 构造函数的函数体必须为空（这一点基于构造函数没有返回值，所以不存在return expr）​。
			- ```cpp
			  class X {
			  public:
			    constexpr X() : x1(5) {}
			    constexpr X(int i) : x1(i) {}
			    constexpr int get() const // const多余，constexpr会自动给函数加上const属性
			    {
			         return x1;
			    }
			  private:
			    int x1;
			  };
			  
			  constexpr X x;
			  char buffer[x.get()] = { 0 };
			  ```
		- constexpr也会退化：
			- ```cpp
			  int i = 8;
			  constexpr X x(i);     // 编译失败，不能使用constexpr声明，i不是常量，无法退化，编译失败
			  X y(i);               // 编译成功。退化
			  ```
		- 最后需要强调的是，==使用constexpr声明自定义类型的变量，必须确保这个自定义类型的析构函数是平凡的==，否则也是无法通过编译的。平凡析构函数必须满足下面3个条件。
			- 1．自定义类型中不能有用户自定义的析构函数。
			- 2．析构函数不能是虚函数。
			- 3．基类和成员的析构函数必须都是平凡的。
	- ## constexpr lambdas表达式
		- **从C++17开始， [[CPP/lambda]] 表达式在条件允许的情况下都会隐式声明为constexpr**，在lambda表达式不满足申明为constexpr形式时，会退化为为运行时lambda表达式存在
		- 也可以强制要求lambda表达式是一个常量表达式，用constexpr去声明它即可。可以检查lambda表达式是否有可能是一个常量表达式，如果不能则会编译报错。
-
-
-
- # constexpr与const对比
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
- # C++14下的constexpr
	- C++14标准对常量表达式函数的改进如下。
		- 1．函数体允许声明变量，除了没有初始化、 [[static]] 和thread_local变量。
			- 局部static变量运行到才会初始化.不符合常量定义，无法在编译器确定
		- 2．函数允许出现if和switch语句，不能使用go语句。
		- 3．函数允许所有的循环语句，包括for、while、do-while。
		- 4．函数可以修改生命周期和常量表达式相同的对象。
		- 5．函数的返回值可以声明为void。
		- 6．constexpr声明的成员函数不再具有const属性。（因为有4）
	- 例：
		- ```cpp
		  #include <iostream>
		  
		  class X {
		  public:
		    constexpr X() : x1(5) {}
		    constexpr X(int i) : x1(0) // 构造函数内可以使用if-else了 条件2、4、6
		    {
		        if (i > 0) {
		            x1 = 5;
		        }
		        else {
		            x1 = 8;
		        }
		    }
		    constexpr void set(int i) // 函数返回值可以是void 条件5
		    {
		        x1 = i;
		    }
		    constexpr int get() const
		    {
		        return x1;
		    }
		  private:
		    int x1;
		  };
		  
		  constexpr X make_x() // 条件4、6
		  {
		    X x;
		    x.set(42);
		    return x;
		  }
		  
		  int main()
		  {
		    constexpr X x1(-1);
		    constexpr X x2 = make_x();
		    constexpr int a1 = x1.get();
		    constexpr int a2 = x2.get();
		    std::cout << a1 << std::endl;
		    std::cout << a2 << std::endl;
		  }
		  ```
-
-
-