- #CPP/STL #CPP/STD
- # 资料
	- [C++: 左值引用(&), 右值引用(&&),万能引用(template &&)详解 与 完美转发(forward) 实现剖析 - woder - 博客园](https://www.cnblogs.com/ishen/p/13771991.html)
	- [一起来学C++ 35.完美转发_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1a1SPYaEBY/?spm_id_from=333.880.my_history.page.click&vd_source=2743cee97cd6d41e92b0735f5f3387e4)
- # 头文件
	- `<utility>`
- # 什么是完美转发
	- 为了能够在多级函数调用中实现移动语义，需要知道参数原有的类型，才能正确调用相应的拷贝构造(赋值）函数或移动构造(赋值）函数。从而引入完美转发
- # 作用
	- 将左值转发为左值或右值，取决于T的类型
		- ```cpp
		  template<class T>
		  void wrapper(T&& arg)
		  {
		      // arg is always lvalue
		      foo(std::forward<T>(arg)); // Forward as lvalue or as rvalue, depending on T
		  }
		  ```
		- 对`wrapper`传递一个**右值string**，则T被推断为string。并且forward传递一个**右值string**给foo函数
		- 对`wrapper`传递一个**非const左值引用string**，则T被推断为非const左值引用string&。并且forward传递一个**非const左值引用string**给foo函数
		- 对`wrapper`传递一个**const左值引用string**，则T被推断为const左值引用string。并且forward传递一个**const左值引用左值string**给foo函数
	- 将右值转发为右值
- # 如何实现？
	- MSVC内简要实现：
		- ```cpp
		  template<typename _Tp> 
		  constexpr _Tp&& forward(typename std::remove_reference<_Tp>::type& __t) noexcept { 
		  	return static_cast<_Tp&&>(__t);
		  }
		  
		  template<typename _Tp> 
		  constexpr _Tp&& forward(typename std::remove_reference<_Tp>::type&& __t) noexcept {
		  	return static_cast<_Tp&&>(__t);
		  }
		  ```
	- 原理：
		- [[CPP/引用]]
		- [[CPP/引用折叠]]
- # 使用示例
	-
-
-
-
-
-
-
-
-
-