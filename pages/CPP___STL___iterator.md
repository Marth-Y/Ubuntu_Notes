- ofstream_iterator #CPP/STL/fstream #CPP/STL/iterator
	- 可以使用`ofstream_iterator`：这种方式进行输出
		- ```cpp
		  constexpr std::array v{1, 2, 3, 4, 4, 3, 7, 8, 9, 10};
		  std::cout << "v: ";
		  std::copy(v.cbegin(), v.cend(), std::ostream_iterator<int>(std::cout, " "));
		  std::cout << '\n';
		  ```
		- 输出原理：
			- `ostream_iterator`：定义了一个迭代器类，其内存了一个输出流的地址以及分隔符（默认为空）
				- 可以参考 [construct](https://en.cppreference.com/w/cpp/iterator/ostream_iterator/ostream_iterator)
				- 使用`copy`，将容器中的元素逐个拷贝给迭代器类，因此会调用迭代器类的拷贝赋值函数：
					- ```cpp
					  ostream_iterator& operator=(const _Tp& __value) {
					    *_M_stream << __value;
					    if (_M_string) {
					      *_M_stream << _M_string;
					    }
					    return *this;
					  }
					  ```
				- 将其输出并检查是否有分隔符。
		- 因此，同理可以使用其做文件的读写
			- ```cpp
			  ofstream ofs("./test.txt");
			  string te = "this is a test!";
			  std::ostream_iterator<char> oo(ofs);
			  std::copy(te.begin(), te.end(), oo);
			  ```
-