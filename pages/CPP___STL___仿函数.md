- `std::function`
	- 绑定普通函数
	- 绑定成员函数
		- 需要额外传入一个对象指针，让其知道是那个对象去调用成员函数。
			- ```cpp
			  using namespace std::placeholders;
			  class Foo{
			  public:
			      void test_func(int i) {};
			  private:
			      function<void(int)> test = std::bind(&Foo::test_func, this, _1);
			  };
			  ```
		- 也可以使用`std::mem_fn`获取成员函数、数据的指针 #CPP/STD
			- ```cpp
			  // std::mem_fn可以获取函数指针、数据指针
			  Foo fo;
			  auto ptr_func = std::mem_fn(&Foo::test_func);
			  function<void(int)> test = std::bind(ptr_func, &fo, _1);
			  
			  auto data_ptr = std::mem_fn(&Foo::data);
			  ```