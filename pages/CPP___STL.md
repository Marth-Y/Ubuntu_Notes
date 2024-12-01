-
- CPP20 #CPP #CPP20
	- std::partial_sum
		- [逐次累加求和，并将结果放入d_first](https://en.cppreference.com/w/cpp/algorithm/partial_sum)
		- ```cpp
		  template< class InputIt, class OutputIt, class BinaryOp >
		  OutputIt partial_sum( InputIt first, InputIt last,
		                        OutputIt d_first, BinaryOp op );
		  ```
-