- lambda实现原理 #CPP/重载
	- 重载调用运算符
	- ```cpp
	  #include <cstdio>
	  
	  int main()
	  {
	    int val = 10;
	    auto lambda = [val]() {
	    	return val + 10;
	    };
	    auto t = lambda();
	  }
	  ```
	- ```cpp
	  #include <cstdio>
	  
	  int main()
	  {
	    int val = 10;
	      
	    class __lambda_6_17
	    {
	      public: 
	      inline int operator()() const
	      {
	        return val + 10;
	      }
	      
	      private: 
	      int val;
	      public: 
	      // inline /*constexpr */ __lambda_6_17(__lambda_6_17 &&) noexcept = default;
	      __lambda_6_17(int & _val)
	      : val{_val}
	      {}
	      
	    };
	    
	    __lambda_6_17 lambda = __lambda_6_17(__lambda_6_17{val});
	    int t = lambda.operator()();
	    return 0;
	  }
	  
	  ```
	- 智能指针是将指针转化为对象，lambda是将函数指针转化为对象进行管理。
	- lambda底层原理就是定义了一个类，在其中实现operator()的重载，然后定义一个匿名对象，从而实现。