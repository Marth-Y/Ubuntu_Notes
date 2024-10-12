- 使用`ifstream`直接读取二进制数据，并将其赋给`char`指针 #CPP/STL/fstream #CPP/STL/vector #文件操作
  id:: 66abb115-bad2-424e-a304-da03b5141f04
  collapsed:: true
	- ```cpp
	  float* ReadBinaryFile(std::string file, int size) {
	      // 可以是任意指针
	    	float* dst = new float[size];
	      std::ifstream ifs(file, std::ios::binary);
	    	// 获取文件大小
	      ifs.seekg(0, std::ios::end);
	      std::streamsize file_size = ifs.tellg();
	      ifs.seekg(0, std::ios::beg);
	     
	      ifs.read(reinterpret_cast<char*>(dst), file_size);
	  
	    	// 输出验证
	      size_t num_floats = file_size / sizeof(float);
	      ifs.close();
	      for (size_t i = 0; i < num_floats; ++i) {
	          std::cout << dst[i] << " ";
	      }
	      std::cout << std::endl;
	      return dst;
	  }
	  
	  	// 也可以是vector<char> vec
	      std::string ori_bin_pth(ori_bin_path);
	      std::ifstream ori_ifs(ori_bin_pth, std::ios::binary);
	      if (!ori_ifs.is_open())
	      {
	          std::cerr << "Failed to open file: " << ori_bin_pth << std::endl;
	          return std::pair<std::vector<char>,std::vector<char>>();
	      }
	      std::vector<char> ori_buffer(std::istreambuf_iterator<char>(ori_ifs), {});
	  ```
- `std::istreambuf_iterator` #CPP/STL/fstream
  collapsed:: true
	- `std::istreambuf_iterator` 是 C++ 标准库中的一个输入迭代器，用于从输入流缓冲区（`std::streambuf`）中读取字符。它通常用于处理文件或字符串流中的字符数据。
	- ((66abb115-bad2-424e-a304-da03b5141f04)) 末尾有示例
-
- `std::count_if`中有：这种方式进行输出 #Learn #CPP/STL/fstream
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