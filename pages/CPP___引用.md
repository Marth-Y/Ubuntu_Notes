- 左值引用
	- ```cpp
	  void f(string& s);
	  
	  string test;
	  f(s);
	  f(string("")); // error
	  ```
	- 左值引用只能绑定左值
- 右值引用
	- ```cpp
	  void f(string&& s);
	  
	  string test;
	  f(s);		  // error
	  f(string(""));
	  ```
	- 右值引用只能绑定到右值
- 常量左值引用
	- ```cpp
	  void f(const string& s);
	  
	  string test;
	  f(s);
	  f(string(""));
	  ```
	- 可以绑定左值，也可以绑定右值
- 模板推导中：万能引用
	- ```cpp
	  template class<T>
	  void f(T&&);
	  ```
	- universal reference，即可以绑定左值也可以绑定右值
	- 模板中的万能引用只发生在模板类型推导的时候，如果没有类型推导，则还是代表右值引用。如：
	- ```cpp
	  template class<T>
	  void f(Wgets&&);//右值引用
	  ```
	- 在万能引用中，编译器有一个规则，如果传入的是左值，则模板类型会被推导成左值引用类型； 传入的是右值，则模板类型就是值的类型
	  background-color:: pink
	- 在万能引用中：
		- 当实参是右值时，模板参数T被推导为实参本身的类型：`string`
		- 当实参是左值时，模板参数T被推导为实参的引用类型：`string&`
	- 例：
		- ```cpp
		  template class<T>
		  void g(T&& t) {
		  	f<T>(t);
		  }
		  
		  string test;
		  g(s);		  // T  为string&
		  实例化：
		  void g<string>(string&& t) {
		  	f<T>(t);
		  }
		  
		  g(string(""));// T  为string
		  实例化：
		  void g<string&>(string& && t) {
		  	f<T>(t);
		  }
		  ```
	- [[CPP/引用折叠]]