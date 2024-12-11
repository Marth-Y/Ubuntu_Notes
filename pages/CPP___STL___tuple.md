- `std::tuple` #CPP/STL #CPP/STL/tuple
	- C++17及以上：#CPP17 #CPP20
		- ```cpp
		  #include <iostream>
		  #include <tuple>  // 包含 std::tuple
		  #include <string>
		  
		  int main() {
		      // 创建一个 std::tuple 实例
		      std::tuple<int, double, std::string> t = {42, 3.14, "hello"};
		  
		      // 使用结构化绑定解包元素
		      auto [first, second, third] = t;
		  
		      // 输出解包后的元素
		      std::cout << "First element: " << first << std::endl;
		      std::cout << "Second element: " << second << std::endl;
		      std::cout << "Third element: " << third << std::endl;
		  
		      return 0;
		  }
		  ```
	- 使用`std::get<index>`
		- ```cpp
		  #include <iostream>
		  #include <tuple>  // 包含 std::tuple
		  #include <string>
		  
		  int main() {
		      // 创建一个 std::tuple 实例
		      std::tuple<int, double, std::string> t = {42, 3.14, "hello"};
		  
		      // 访问第一个元素
		      int firstElement = std::get<0>(t);
		      std::cout << "First element: " << firstElement << std::endl;
		  
		      // 访问第二个元素
		      double secondElement = std::get<1>(t);
		      std::cout << "Second element: " << secondElement << std::endl;
		  
		      // 访问第三个元素
		      std::string thirdElement = std::get<2>(t);
		      std::cout << "Third element: " << thirdElement << std::endl;
		  
		      return 0;
		  }
		  ```
	- 也可以使用std::tie解包std::tuple #CPP/STD
		- ```cpp
		  #include <iostream>
		  #include <tuple>  // 包含 std::tuple 和 std::tie
		  #include <string>
		  
		  int main() {
		      // 创建一个 std::tuple 实例
		      std::tuple<int, double, std::string> t = {42, 3.14, "hello"};
		  
		      // 使用 std::tie 解包元素
		      int first;
		      double second;
		      std::string third;
		      std::tie(first, second, third) = t;
		  
		      // 修改解包后的元素
		      first = 100;
		      second = 2.718;
		      third = "world";
		  
		      // 输出修改后的元素
		      std::cout << "Modified first element: " << first << std::endl;
		      std::cout << "Modified second element: " << second << std::endl;
		      std::cout << "Modified third element: " << third << std::endl;
		  
		      return 0;
		  }
		  ```