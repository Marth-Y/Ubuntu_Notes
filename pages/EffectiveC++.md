- 条款02：尽量以const、enum、inline替换# define #define #const #enum #EffectiveC++
  collapsed:: true
	- 1、define不易于编译报错时查看报错信息
		- `#define ASPECT 1.63`
		- 对于编译器而言，会替换掉`ASPECT`，只有 1.63 。导致报错时只会显示1.63，无法定位具体出错的位置。
			- > 之前同事有一次始终编译不过，提示的一个宏有错误，幸好是知道改在哪儿的宏，不然编译器只报宏替换后的错，完全看不懂为什么报错了。
	- 2、define会替换所有位置，占用空间更大。
		- 如：上面定义一个常量宏，会替换所有位置的宏，占用多份儿空间。而定义 const常量只会占用一份的空间
	- 3、define不具备封装性，即：没有`private: #define `这种东西，而`const`、`enum`、`inline`都有
	- 4、宏函数追求更高的执行效率，但是也会有缺点：
		- `FUN(++a,b)`可能导致a被多次累加
		- 宏函数中需要给每个变量加括号，不然可能导致未定义的行为。
		- 宏函数不具备封装性
	- ==小结==：
		- 对于单纯常量，最好以`const`或者`enum`替换宏。
		- 对于宏函数，最好用`inline`替换。
- 条款03：尽可能使用const #EffectiveC++ #const #static
  collapsed:: true
	- 1、const修饰指针
		- {{embed ((65d604e7-6580-4230-a087-1ca03f46abe3))}}
	- 2、const修饰迭代器
		- STL迭代器const迭代器：`const_iterator` #const #CPP/STL
	- 3、const修饰返回值
		- ```cpp
		  const T operator*(const T& lhs, const T& rhs);
		  
		  T a,b,c;
		  (a * b) = c;   // 避免为a*b赋值
		  ```
	- 4、const成员函数
		- {{embed ((65d605a7-94a5-4469-948d-104a3ebc6f83))}}
		- ==两个成员函数如果只是常量性不同，可以被重载== #重载
			- ```cpp
			  class T {
			  public:
			    const char& operator[](size_t position) const   // const常量会调用
			    { return test[position]; }
			    
			    char& operator[](size_t position)               // 非const常量会调用
			    { return test[position]; }
			  };
			  
			  只要重载operator[]并对不同版本给予不同返回类型，就可以使const和non-const获得不同的处理。
			  ```
		- 成员函数是const有两个流行概念==bitwise constness(physical constness)和logical constness==
			- `bitwise constness`阵营人为：`const`成员函数不可以更改对象内任何`non-static`成员变量。即：不可以更改对象的任何一个`bit`。
				- 但是，如果一个对象有一个指针成员，那么修改指针指向的对象，而指针指向没有变，这就导致编译器认为对象没有改变，它是`bitwise constness`。
			- 因此引出了`logical constness`，一个`const`成员函数可以在客户端侦测不出的情况下，修改它所处理的对象内的某些`bits`。那么如何让客户端编译器侦测不出来，或者说：同意修改呢？
				- 可以利用C++一个与`const`相关的摆动场：`mutable(可变的)`，它可以释放掉`non-static`成员变量的`bitwise constness`约束
				- ```cpp
				  class T{
				  public:
				    mutable bool flag;       // 即使在const成员函数内也可以改变
				    
				    void Change() const {
				      flag = true;           // 现在可以改变了。
				    }
				  };
				  ```
		- 在const和non-const成员函数中避免重复——==运用const成员函数实现non-const== #常量性转除
			- 对`operator[]`分为const和non-const版本是好事儿，但是如果其中加入了大量其他代码，则会导致连个臃肿的函数：
				- ```cpp
				  const char& operator[](size_t position) const {
				    // 边界检查
				    // 日志访问记录
				    // 数据完整性检查
				    return test[position];
				  }
				  
				  char& operator[](size_t position) {
				    // 边界检查
				    // 日志访问记录
				    // 数据完整性检查
				    return test[position];
				  }
				  ```
				- 当然，我们可以将边界检查、日志访问、数据完整性检验等移入一个函数，然后用`operator[]`调用即可减少代码的臃肿，但是还是会有重复调用、两次returen语句重复。更好的方式是使用`常量性转除(casting away constness)`。因为两个重载函数中操作一样，只有返回值不一样。因此可以用non-const调用const版本 #常量性转除
				- ```cpp
				  char& operator[](size_t position) {
				    return const_cast<char&>(          // 将op返回值的const移除。
				      static_cast<const T&>(*this)     // 将*this转为const对象
				      [position]                       // 调用const op[]
				    );
				  }
				  ```
				- 不要用const反向调用non-const实现，因为const承诺不修改其内容，non-const可能会修改内容。
	- > 1. 编译器强制实施bitwise constness，但是你编写程序时应该使用“概念上的常量性(conceptual constness)"
	  2. 当const和non-const成员函数有实质等价实现时，用non-const版本调用const版本避免代码重复
	-
-
-
-
-