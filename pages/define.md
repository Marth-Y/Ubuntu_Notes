- 可变参数宏
	- ```cpp
	  // 定义宏 T(...) 为 _VARGS
	  #define T(...) _VARGS(__VA_ARGS__)
	  
	  // 定义一个处理可变参数的函数
	  void _VARGS(const char* fmt, ...) {
	      va_list args;
	      va_start(args, fmt);
	      vprintf(fmt, args);
	      va_end(args);
	  }
	  
	  ```