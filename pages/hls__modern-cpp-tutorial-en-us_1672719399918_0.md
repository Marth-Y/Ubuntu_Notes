file:: [modern-cpp-tutorial-en-us_1672719399918_0.pdf](../assets/modern-cpp-tutorial-en-us_1672719399918_0.pdf)
file-path:: ../assets/modern-cpp-tutorial-en-us_1672719399918_0.pdf
tag:: #cpp

- # Preface
  ls-type:: annotation
  hl-page:: 8
  hl-color:: red
  id:: 63b3ac7f-1c4c-4e20-8727-a590e7d55af6
  hl-stamp:: 1673151259566
  collapsed:: true
	- Introduction
	  ls-type:: annotation
	  hl-page:: 8
	  hl-color:: yellow
	  id:: 63b3ac90-e426-4077-89f5-a95822c71f27
- # Chapter 01: Towards Modern C++
  ls-type:: annotation
  hl-page:: 9
  hl-color:: red
  id:: 63b3b1ca-06e2-4e62-93aa-01a53c266d4c
  collapsed:: true
	- Compilation Environment：`clang++`、`-std=c++2a`
	  hl-page:: 9
	  ls-type:: annotation
	  id:: 63b3b1db-dbd6-4a56-addd-addb5e838959
	  hl-color:: yellow
	- ## 1.1 Deprecated Features
	  hl-page:: 10
	  ls-type:: annotation
	  id:: 63b3b571-10ca-47af-af76-f442cef7c480
	  hl-color:: yellow
	  collapsed:: true
		- The string literal constant is no longer allowed to be assigned to a char *. If you need to assign and initialize a char * with a string literal constant, you should use const char * or auto.
		  hl-page:: 10
		  ls-type:: annotation
		  id:: 63b3b583-e868-440a-b053-973dae452e54
		  hl-color:: yellow
			- char *str = "hello world!"; // A deprecation warning will appear
			  ls-type:: annotation
			  hl-page:: 10
			  hl-color:: yellow
			  id:: 63b3b5e2-ba20-4b53-a21e-6856ecc09869
			  hl-stamp:: 1673151277562
		- C++98 exception description, unexpected_handler, set_unexpected() and other related features are deprecated and should use noexcept.
		  ls-type:: annotation
		  hl-page:: 10
		  hl-color:: yellow
		  id:: 63b3b5da-758a-4944-a237-049a2b0b81d1
		- auto_ptr is deprecated and unique_ptr should be used.
		  ls-type:: annotation
		  hl-page:: 10
		  hl-color:: yellow
		  id:: 63b3b5dc-757d-4756-a14e-15026417afd9
		- register keyword is deprecated and can be used but no longer has any practical meaning.
		  ls-type:: annotation
		  hl-page:: 10
		  hl-color:: yellow
		  id:: 63b3b623-375d-4006-90e2-4f7ddf7b1e20
		- The ++ operation of the bool type is deprecated.
		  ls-type:: annotation
		  hl-page:: 10
		  hl-color:: yellow
		  id:: 63b3b62f-1ed2-4753-b2a4-ea51bfe8b37a
			- Note:很奇怪，为什么bool类型原来能++？。
		- If a class has a destructor, the properties for which it generates copy constructors and copy assignment operators are deprecated.
		  ls-type:: annotation
		  hl-page:: 10
		  hl-color:: yellow
		  id:: 63b3b67a-9faa-453f-b7e2-28a4fc278ad6
		- C language style type conversion is deprecated (ie using (convert_type)) before variables, and static_cast, reinterpret_cast, const_cast should be used for type conversion.
		  ls-type:: annotation
		  hl-page:: 10
		  hl-color:: yellow
		  id:: 63b3b6d6-0800-42ca-95bd-bf184ef6c1e0
			- C++风格的类型转换的区别：
			- static_cast
			- const_cast
			- reinterpret_cast
		- In particular, some of the C standard libraries that can be used are deprecated in the latest C++17 standard, such as <ccomplex>, <cstdalign>, <cstdbool> and <ctgmath> etc.
		  ls-type:: annotation
		  hl-page:: 10
		  hl-color:: yellow
		  id:: 63b3b85b-b6f0-4695-bfca-2710b58f9651
			- ==这些库在C++17中已经被弃用==
		- There are also other features such as parameter binding (C++11 provides std::bind and std::function), export etc. are also deprecated
		  ls-type:: annotation
		  hl-page:: 10
		  hl-color:: yellow
		  id:: 63b3b8fc-4180-43db-8130-559fcb54495b
		- These features mentioned above If you have never used or heard of it, please don’t try to understand them. You should move closer to the new standard and learn new features directly.
		  ls-type:: annotation
		  hl-page:: 10
		  hl-color:: purple
		  id:: 63b3b904-1dd7-471f-9778-fb9d346895b4
		  background-color:: green
	- ## 1.2 Compatibilities with C
	  ls-type:: annotation
	  hl-page:: 11
	  hl-color:: yellow
	  id:: 63b3baf0-4ca1-41fd-95cb-0dde91f98d4a
	  collapsed:: true
		- From now on, you should have the idea that “C++ is not a superset of C” in your mind
		  ls-type:: annotation
		  hl-page:: 11
		  hl-color:: yellow
		  id:: 63b3bbea-333f-405f-8f99-869f765c8d6b
		  hl-stamp:: 1673151268086
		- When writing C++, you should also avoid using program styles such as void* whenever possible.
		  ls-type:: annotation
		  hl-page:: 11
		  hl-color:: yellow
		  id:: 63b3bc10-6b04-40b0-b5d2-3da6066a2859
		- When you have to use C, you should pay attention to the use of extern "C", separate the C language code from the C++ code, and then unify the link, for instance:
		  ls-type:: annotation
		  hl-page:: 11
		  hl-color:: yellow
		  id:: 63b3bcba-5b86-41c6-acc8-9184dddc45ef
			- ```cpp
			  // foo.h
			  #ifdef __cplusplus 
			  extern "C" {
			  #endif 
			  int add(int x, int y);
			  #ifdef __cplusplus
			  }
			  #endif
			  // foo.c 
			  int add(int x, int y) 
			  { return x+y;}
			  // 1.1.cpp
			  #include "foo.h"
			  #include <iostream>
			  #include <functional> 
			  int main()
			  {
			    [out = std::ref(std::cout << "Result from C code: " << add(1, 2))]()
			    { 
			      out.get() << ".\n";
			    }();
			    return 0;
			  }
			  ```
			- 先用gcc编译`foo.c`：`gcc -c foo.c`
			- 然后编译cpp文件
			- 最后将`.o`文件链接起来
- # Chapter 02: Language Usability Enhancements
  ls-type:: annotation
  hl-page:: 13
  hl-color:: red
  id:: 63b3bdd4-99bf-4437-8109-a7592ee603fa
	- ## 2.1 Constants
	  ls-type:: annotation
	  hl-page:: 13
	  hl-color:: yellow
	  id:: 63b568ac-9ca0-44ae-940e-edfe6e860794
	  collapsed:: true
		- ### nullptr
		  ls-type:: annotation
		  hl-page:: 13
		  hl-color:: purple
		  id:: 63b568fc-da8b-49f1-ad7e-278373483f34
		  collapsed:: true
			- The purpose of nullptr appears to replace NULL. In a sense, traditional C++ treats NULL and 0 as the same thing, depending on how the compiler defines NULL, and some compilers define NULL as ((void*)0) Some will define it directly as 0.
			  hl-page:: 13
			  ls-type:: annotation
			  id:: 63b56927-d9be-497c-a7fa-ea5979b5d8ca
			  hl-color:: yellow
			- C++ does not allow to implicitly convert void * to other types.
			  ls-type:: annotation
			  hl-page:: 14
			  hl-color:: yellow
			  id:: 63b56941-8c59-4a5b-9105-14482610f973
			- 为什么用`nullptr`替换`NULL`?
				- 在传统C++中`NULL`被定义为`0`或者`((void *)0)`
				- C++不允许`((void *)0)`到`0`的隐式转换。试想如果编译器将`NULL`定义为`((void *)0)`或者`0`，存在前面的隐式转换，那么就会出现以下的误解：
				- ```cpp
				  void foo(int);
				  void foo(char*);
				  
				  foo(NULL);
				  ```
					- `foo`将会调用哪一个呢？
					- ![image.png](../assets/image_1672834094046_0.png)
				- 为了解决这个问题，C++11引入了`nullptr`关键字
				- To solve this problem, C++11 introduced the nullptr keyword, which is specifically used to distinguish null pointers, 0. The type of nullptr is nullptr_t, which can be implicitly converted to any pointer or member pointer type, and can be compared equally or unequally with them.
				  ls-type:: annotation
				  hl-page:: 14
				  hl-color:: red
				  id:: 63b56c5c-c2ea-4c68-aedb-c0d43c3ac51e
					- ```CPP
					  #include <type_traits>
					  
					  void foo(int)
					  {
					      cout << "foo(int)" << endl;
					  }
					  
					  void foo(char*)
					  {
					      cout << "foo(char*)" << endl;
					  }
					  
					  int main()
					  {
					      if (std::is_same<decltype(NULL), decltype(0)>::value) 
					          std::cout << "NULL == 0" << std::endl; 
					      if (std::is_same<decltype(NULL), decltype((void*)0)>::value) 
					          std::cout << "NULL == (void *)0" << std::endl; 
					      if (std::is_same<decltype(NULL), std::nullptr_t>::value) 
					          std::cout << "NULL == nullptr" << std::endl; 
					      foo(0); // will call foo(int)
					      // foo(NULL); // doesn't compile 
					      foo(nullptr); // will call foo(char*) 
					  }
					  ```
				- In simple terms, decltype is used for type derivation, and std::is_same is used to compare the equality of the two types. 
				  ls-type:: annotation
				  hl-page:: 15
				  hl-color:: yellow
				  id:: 63b56e27-4097-48d9-b238-678ba1411163
		- ### constexpr
		  hl-page:: 15
		  ls-type:: annotation
		  id:: 63b56e44-4f13-4a99-a51e-2d70ff0a510f
		  hl-color:: purple
		  hl-stamp:: 1673151294563
		  collapsed:: true
			- ```cpp
			  #include <iostream>
			  #define LEN 10
			  
			  int len_foo() {
			      int i = 2;
			      return i;
			  }
			  constexpr int len_foo_constexpr() {
			      return 5;
			  }
			  
			  // error in c++11
			  // constexpr int fibonacci(const int n) {
			  //     if(n == 1) return 1;
			  //     if(n == 2) return 1;
			  //     return fibonacci(n-1) + fibonacci(n-2);
			  // }
			  
			  // ok
			  constexpr int fibonacci(const int n) {
			      return n == 1 || n == 2 ? 1 : fibonacci(n-1) + fibonacci(n-2);
			  }
			  
			  
			  int main() {
			      char arr_1[10];                      // legal
			      char arr_2[LEN];                     // legal
			  
			      int len = 10;
			      // char arr_3[len];                  // illegal
			  
			      const int len_2 = len + 1;
			      constexpr int len_2_constexpr = 1 + 2 + 3;
			      // char arr_4[len_2];                // illegal, but ok for most of the compilers
			      char arr_4[len_2_constexpr];         // legal
			  
			      // char arr_5[len_foo()+5];          // illegal
			      char arr_6[len_foo_constexpr() + 1]; // legal
			      
			      // 1, 1, 2, 3, 5, 8, 13, 21, 34, 55
			      std::cout << fibonacci(10) << std::endl;
			  
			      return 0;
			  }
			  ```
				- In the above example, char arr_4[len_2] may be confusing because len_2 has been defined as a constant. Why is char arr_4[len_2] still illegal? This is because the length of the array in the C++ standard must be a constant expression, and for len_2, this is a const constant, not a constant expression, so even if this behavior is supported by most compilers, but it is an illegal behavior, we need to use the constexpr feature introduced in C++11, which will be introduced next, to solve this problem; for arr_5, before C++98 The compiler cannot know that len_foo() actually returns a constant at runtime, which causes illegal production.
				  ls-type:: annotation
				  hl-page:: 16
				  hl-color:: yellow
				  id:: 63b57226-29a2-4d3e-8b2e-49ccacca75de
				- 在例子中，len_2不能作为数组定义的参数是因为在C++11中，数组定义的参数需要是常量，而len_2是const 常量，有别于常量，因此不能作为数组定义的参数（但是在vscode、g++中都是可以编译通过的）。
				- 数组的定义是在编译期就要知道大小，而普通的函数返回值是在运行期才知晓，因此不能作为数组定义的参数。
					- Note that most compilers now have their compiler optimizations. Many illegal behaviors become legal under the compiler’s optimization. If you need to reproduce the error, you need to use the old version of the compiler.
					  ls-type:: annotation
					  hl-page:: 16
					  hl-color:: green
					  id:: 63b572c6-b0c8-4561-99be-e79cb7813b0e
				- ==C++11 provides constexpr to let the user explicitly declare that the function or object constructor will become a constant expression at compile time.==
				  hl-page:: 16
				  ls-type:: annotation
				  id:: 63b572eb-bf87-43d4-9802-2262482eef37
				  hl-color:: red
					- `constexpr`关键字让程序员明确知道所修饰的变量或者函数、对象的构造函数将会是一个编译期就知晓的常量表达式
				- In addition, the function of constexpr can use recursion:
				  ls-type:: annotation
				  hl-page:: 16
				  hl-color:: yellow
				  id:: 63b57378-5f7b-49cc-bde1-ae2d93b5ee90
					- 对于`constexpr`可以使用递归
					- ```CPP
					  constexpr int fibonacci(const int n) {
					    return n == 1 || n == 2 ? 1 : fibonacci(n-1) + fibonacci(n-2);
					  }
					  ```
				- Starting with C++14, the constexpr function can use simple statements such as local variables, loops, and branches internally. For example, the following code cannot be compiled under the C++11 standard:
				  ls-type:: annotation
				  hl-page:: 16
				  hl-color:: blue
				  id:: 63b5745b-a1c1-47d4-b74f-69c806b698c8
					- ```CPP
					  constexpr int fibonacci(const int n) { 
					    if(n == 1) return 1; 
					    if(n == 2) return 1; 
					    return fibonacci(n-1) + fibonacci(n-2);
					  }
					  ```
				- To do this, we can write a simplified version like this to make the function available from C++11:
				  ls-type:: annotation
				  hl-page:: 17
				  hl-color:: blue
				  id:: 63b5748b-c032-4be0-9553-eaf90cd43aae
					- ```CPP
					  constexpr int fibonacci(const int n) {
					    return n == 1 || n == 2 ? 1 : fibonacci(n-1) + fibonacci(n-2);
					  }
					  ```
				- ![image.png](../assets/image_1672836267864_0.png)
	- ## 2.2 Variables and initialization
	  hl-page:: 17
	  ls-type:: annotation
	  id:: 63b574b9-d4ce-4230-bed1-1ca6205e48ef
	  hl-color:: yellow
		- ### if-switch
		  ls-type:: annotation
		  hl-page:: 17
		  hl-color:: purple
		  id:: 63b574ea-f0f6-4bc4-9513-c07d4b7badee
		  hl-stamp:: 1673151301395
		  collapsed:: true
			- 传统C++几乎可以在任意位置声明一个变量，但是不能在`if`和`switch`的括号中声明临时变量
			- ```CPP
			  if(int i = 0; i == 0)
			  {
			    cout << "i == 0" << endl;
			  }
			  ```
		- ### Initializer list
		  ls-type:: annotation
		  hl-page:: 18
		  hl-color:: purple
		  id:: 63b6b8c9-4151-4bb3-8393-0adb69299b14
		  hl-stamp:: 1673151304336
			- 传统C++在只能在构造函数等函数中使用初始化列表，而无法在普通函数中使用变量列表。因此C++11中引入了`std::initializer_list`
			- ```cpp
			  #include<iostream>                                                                                                                                                                                                                                                                                                    
			  #include <initializer_list>
			  using std::cout;
			  using std::endl;
			  using std::cin;
			  
			  void foo(std::initializer_list<int>list)
			  {
			      for(std::initializer_list<int>::iterator it = list.begin(); it != list.end(); ++it)
			      {   
			          cout << *it << endl;
			      }   
			  }
			  
			  int main()
			  {
			      foo({0,1,2,3,4,5,6,7,8,9,10});
			  }
			  ```
		- ### Structured binding
		  ls-type:: annotation
		  hl-page:: 20
		  hl-color:: purple
		  id:: 63b6baf0-3aa1-4ff0-a314-385039a6aed4
		  hl-stamp:: 1673151311123
		  collapsed:: true
			- In the chapter on containers, we will learn that C++11 has added a std::tuple container for constructing a tuple that encloses multiple return values. But the flaw is that C++11/14 does not provide a simple way to get and define the elements in the tuple from the tuple, although we can unpack the tuple using std::tie But we still have to be very clear about how many objects this tuple contains, what type of each object is, very troublesome.
			  ls-type:: annotation
			  hl-page:: 20
			  hl-color:: green
			  id:: 63ba2c5a-3a5e-4464-b30a-2c0afd168c57
			  hl-stamp:: 1673151316498
			- 在C++11中可以使用`std::tuple`元组来完成返回多个返回值的任务，但是在C++11/14中，我们必须清楚的知道tuple容器内有多少元素、每个元素的类型，这很麻烦。
			- 在C++17中完善了这个缺点，可以使用结构化绑定来书写代码：
				- ```CPP
				  #include <iostream>
				  #include <tuple>
				  #include <string>
				  
				  std::tuple<int, double, std::string> f() {
				      return std::make_tuple(1, 2.3, "456");
				  }
				  
				  int main() {
				      auto [x, y, z] = f();
				      std::cout << x << ", " << y << ", " << z << std::endl;
				      return 0;
				  }
				  ```
	- ## 2.3 Type inference
	  hl-page:: 20
	  ls-type:: annotation
	  id:: 63ba2f1d-0550-466b-86bb-35158608918e
	  hl-color:: yellow
	  collapsed:: true
		- #### auto
		  ls-type:: annotation
		  hl-page:: 21
		  hl-color:: purple
		  id:: 63ba2f82-26f1-4d06-8ec6-c7b9186bfe99
		  hl-stamp:: 1673151330851
		  collapsed:: true
			- One of the most common and notable examples of type derivation using auto is the iterator
			  ls-type:: annotation
			  hl-page:: 21
			  hl-color:: red
			  id:: 63ba2fd7-5bbd-4820-832b-0efbca2f472b
				- ```CPP
				  for(auto it = vec.begin(); it != vec.end(); ++it)
				  {
				    ...
				  }
				  ```
			- Since C++ 20, auto can even be used as function arguments. Consider the following example:
			  ls-type:: annotation
			  hl-page:: 22
			  hl-color:: yellow
			  id:: 63ba301f-099a-4a05-b655-e03e9f384b41
				- C++20后，`auto`可以作用在函数参数中
				- ```CPP
				  int add(auto x, auto y)
				  {
				    return x+y;
				  }
				  ```
		- #### decltype
		  ls-type:: annotation
		  hl-page:: 22
		  hl-color:: purple
		  id:: 63ba3082-1bf6-4b72-ae6f-bd3ee3714588
		  hl-stamp:: 1673151335509
		  collapsed:: true
			- The decltype keyword is used to solve the defect that the auto keyword can only type the variable. Its usage is very similar to typeof:
			  ls-type:: annotation
			  hl-page:: 22
			  hl-color:: yellow
			  id:: 63ba309a-7ae9-414e-9509-7b0b256c627a
			- Sometimes we may need to calculate the type of an expression, for example:
			  ls-type:: annotation
			  hl-page:: 22
			  hl-color:: yellow
			  id:: 63ba30d4-fa6e-4d9d-9a8e-18626523dbea
				- ```cpp
				  auto x = 1;
				  auto y = 2;
				  decltype(x + y) z;
				  ```
			- Among them, std::is_same<T, U> is used to determine whether the two types T and U are equal.
			  ls-type:: annotation
			  hl-page:: 23
			  hl-color:: yellow
			  id:: 63ba311d-fbed-42ae-be0e-9782d0994538
		- #### tail type inference
		  ls-type:: annotation
		  hl-page:: 23
		  hl-color:: purple
		  id:: 63ba3126-d25f-4fcc-8095-f28c18aed247
		  hl-stamp:: 1673151339229
		  collapsed:: true
			- 在传统C++中，`auto`关键字不能用于推导函数返回值的类型
				- ```cpp
				  template<typename R, typename T, typename U>
				  R add(T x, U y)
				  {
				    return x + y;
				  }
				  ```
			- Such code is very ugly because the programmer must explicitly indicate the return type when using this template function.
			  ls-type:: annotation
			  hl-page:: 23
			  hl-color:: yellow
			  id:: 63ba389b-5f00-49c7-adcc-2cdce0795d0b
			- C++11 also introduces a trailing return type, which uses the auto keyword to post the return type:
			  ls-type:: annotation
			  hl-page:: 23
			  hl-color:: yellow
			  id:: 63ba38bf-1fa8-4303-ae93-0e4249bca39c
				- ```CPP
				  template<typename T,typename U>
				  auto add(T x, U y)->decltype(x + y)
				  {
				    return x + y;
				  }
				  ```
			- 在C++14中得到了进一步优化：
				- ```cpp
				  template<typename T,typename U>
				  auto add(T x, U y)
				  {
				    return x + y;
				  }
				  ```
		- #### decltype(auto)
		  ls-type:: annotation
		  hl-page:: 24
		  hl-color:: purple
		  id:: 63ba3929-8b79-4bc3-a595-75510e8ba016
		  hl-stamp:: 1673151342098
			- 如果我们使用一个函数包裹另一个函数并返回：
			- ```CPP
			  string lookup1();
			  string lookup2();
			  
			  string look_up_a_string _1()
			  {
			    return lookup1();
			  }
			  string look_up_a_string _2()
			  {
			    return lookup2();
			  }
			  ```
			- 在返回的过程中会发生参数的复制，产生临时参数，在C++14之后可以使用`decltype(auto)`来避免参数转发
			- ```CPP
			  decltype(auto) look_up_a_string _1()
			  {
			    return lookup1();
			  }
			  decltype(auto) look_up_a_string _2()
			  {
			    return lookup2();
			  }
			  ```
			-
	- ## 2.4 Control flow
	  hl-page:: 25
	  ls-type:: annotation
	  id:: 63ba3daa-de52-4bc2-83d7-b3b95c1d79dd
	  hl-color:: yellow
	  collapsed:: true
		- ### if constexpr
		  hl-page:: 25
		  ls-type:: annotation
		  id:: 63ba3dba-dc15-4a44-a91d-5543ef562c72
		  hl-color:: yellow
			- `if constenpr`可以决定编译那一个分支，编译之后是没有`if constexpr`的。
			- ```CPP
			  #include <iostream>
			  
			  template<typename T>
			  auto print_type_info(const T& t) {
			      if constexpr (std::is_integral<T>::value) {
			          return t + 1;
			      } else {
			          return t + 0.001;
			      }
			  }
			  
			  // at compiling time
			  // int print_type_info(const int& t) {
			  //     return t + 1;
			  // }
			  // double print_type_info(const double& t) {
			  //     return t + 0.001;
			  // }
			  
			  int main() {
			      std::cout << print_type_info(5) << std::endl;
			      std::cout << print_type_info(3.14) << std::endl;
			  }
			  ```
			- 所以如果在`if constexpr`外再加上`return `语句编译之后就会出现两个return，从而会报错
		- ### Range-based for loop
		  hl-page:: 26
		  ls-type:: annotation
		  id:: 63ba42ce-4c7b-4526-842d-fe6182318404
		  hl-color:: yellow
			- 范围for循环
	- ## 2.5 Templates
	  ls-type:: annotation
	  hl-page:: 26
	  hl-color:: yellow
	  id:: 63ba4305-4410-4486-9921-b5ba5278bc8f
	  hl-stamp:: 1673151254408
		- he philosophy of the template is to throw all the problems that can be processed at compile time into the compile time, and only deal with those core dynamic services at runtime, to greatly optimize the performance of the runtime. Therefore, templates are also regarded by many as one of the black magic of C++.
		  ls-type:: annotation
		  hl-page:: 26
		  hl-color:: purple
		  id:: 63ba448a-acc9-47a5-9192-da94252e071b
		- ### Extern templates
		  hl-page:: 26
		  ls-type:: annotation
		  id:: 63ba4496-f350-4c87-8e8a-aa9a588b8ca5
		  hl-color:: purple
		  hl-stamp:: 1673151650528
		  collapsed:: true
			- In traditional C++, templates are instantiated by the compiler only when they are used.
			  ls-type:: annotation
			  hl-page:: 26
			  hl-color:: green
			  id:: 63ba4640-3a11-40d8-bf24-4c530a374633
				- 模板只有在使用时才会被编译器实例化，也就是说没遇见一次调用模板，就会实例化一次该模板，因此会有大量重复的实例化，从而增加了编译的时间
			- 在C++11中，引入了外部模板扩展原始的模板语法，强制编译器在一个特定的地方实例化模板，允许我们显式指定编译器何时实例化模板
			- ```CPP
			  template class std::vector<bool>; // force instantiation 
			  extern template class std::vector<double>; // should not instantiation in current file
			  ```
		- ### The “>”
		  ls-type:: annotation
		  hl-page:: 27
		  hl-color:: purple
		  id:: 63ba47fc-efa3-4b83-b4f6-d725b8d98413
		- ### Type alias templates
		  ls-type:: annotation
		  hl-page:: 27
		  hl-color:: purple
		  id:: 63ba4869-7cfd-42f5-8e24-3ae0d30bb555
		  collapsed:: true
			- Before you understand the type alias template, you need to understand the difference between“template” and “type”. Carefully understand this sentence: Templates are used to generate types.
			  ls-type:: annotation
			  hl-page:: 27
			  hl-color:: green
			  id:: 63ba48a6-0fab-4684-98ad-af5e8629bf3e
			- C++11 uses using to introduce the following form of writing, and at the same time supports the same effect as the traditional typedef:
			  ls-type:: annotation
			  hl-page:: 27
			  hl-color:: green
			  id:: 63ba4933-d6db-461c-bb6f-5fcf781a7d12
				- C++11引入了`using`关键字，可以支持对模板起别名
			- ```CPP
			  #include <iostream>
			  #include <vector>
			  #include <string>
			  
			  template<typename T, typename U>
			  class MagicType {
			  public:
			      T dark;
			      U magic;
			  };
			  
			  // illegal
			  // template<typename T>
			  // typedef MagicType<std::vector<T>, std::string> FakeDarkMagic;
			  
			  typedef int (*process)(void *);
			  using NewProcess = int(*)(void *);
			  template<typename T>
			  using TrueDarkMagic = MagicType<std::vector<T>, std::string>;
			  
			  int main() {
			      // FakeDarkMagic<bool> me;
			      TrueDarkMagic<bool> you;
			  }
			  ```
		- ### Variadic templates
		  ls-type:: annotation
		  hl-page:: 28
		  hl-color:: purple
		  id:: 63ba4ae6-d6e5-4592-a821-8dbc49e8d0aa
			- `template<typename... Ts> class Magic;`
			  hl-page:: 28
			  ls-type:: annotation
			  id:: 63ba4b32-0c3c-401e-a7a7-7c1a7a184f1a
			  hl-color:: green
			- 实现一个`printf`函数：
				- `template<typename... Args> void printf(const std::string &str, Args... args);`
				  ls-type:: annotation
				  hl-page:: 29
				  hl-color:: green
				  id:: 63ba4be0-3601-4184-89e7-c0458ea55209
					- Then we define variable length template parameters, how to unpack the parameters?
					  ls-type:: annotation
					  hl-page:: 29
					  hl-color:: green
					  id:: 63ba4c33-88ec-4aaf-809a-fc96ade2c9b6
						- First, we can use sizeof... to calculate the number of arguments:
						  ls-type:: annotation
						  hl-page:: 29
						  hl-color:: green
						  id:: 63ba4c35-f273-4f88-8b6f-a236d0826a4d
							- 注意与普通的`sizeof`的区别，后面加上了`...`表示解包
							- ```CPP
							  cout << sizeof...(args) << endl;
							  ```
						- Second, the parameters are unpacked. So far there is no simple way to process the parameter package, but there are two classic processing methods:
						  ls-type:: annotation
						  hl-page:: 29
						  hl-color:: green
						  id:: 63ba4c1b-36c2-4075-9961-e33d1daa992a
							- #### 1. Recursive template function
							  hl-page:: 29
							  ls-type:: annotation
							  id:: 63ba4c57-88a9-401f-b8d2-35b034248447
							  hl-color:: blue
								- 递归模板函数
								- ```CPP
								  #include <iostream>
								  using namespace std;
								  
								  template<typename T0>
								  void printf(T0 value)
								  {
								      cout << value;
								  }
								  
								  template<typename T, typename... Args>
								  void printf(T value, Args... args)
								  {
								      cout << value;
								      printf(args...);
								  }
								  
								  int main()
								  {
								      printf("456",1,"lskajd");
								  }
								  ```
							- #### 2. Variable parameter template expansion
							  ls-type:: annotation
							  hl-page:: 30
							  hl-color:: blue
							  id:: 63ba4e13-a35d-4efd-8efb-59f813dab4be
								- You should feel that this is very cumbersome. Added support for variable parameter template expansion in C++17, 
								  ls-type:: annotation
								  hl-page:: 30
								  hl-color:: green
								  id:: 63ba4e62-87e8-4aed-b9ad-df2b4aaac564
									- ```cpp
									  template<typename T0, typename... T>
									  void printf2(T0 value, T... t)
									  {
									      cout << value;
									      if constexpr(sizeof...(t) > 0)
									          printf2(t...);
									  }
									  ```
							- #### 3. Initialize list expansion
							  ls-type:: annotation
							  hl-page:: 30
							  hl-color:: blue
							  id:: 63ba4f7e-1e09-47c2-b843-1233ab2c5990
								- Recursive template functions are standard practice, but the obvious drawback is that you must define a function that terminates recursion. Here is a description of the black magic that is expanded using the initialization list:
								  ls-type:: annotation
								  hl-page:: 30
								  hl-color:: green
								  id:: 63ba4fc7-e9bb-4d81-86b3-4a8fdce864e0