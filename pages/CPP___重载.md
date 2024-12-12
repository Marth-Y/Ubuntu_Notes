# 应用
- ## 实现if直接判等
	- ### 重载一个转换指针
		- ```cpp
		  class T{
		  struct dummy{};  
		  public:
		    // 实现if中判空。
		    // 这里的实现逻辑其实很简单，dummy就是一个随便定义的类型，或者这里operator转成其他类型都可以实现if 判空
		    // 因为在if 中会调用一次这个转换以便于与0或者nullptr判等。
		    operator const dummy *() const{
		      if (empty_)
		        {
		          return nullptr;
		        }
		      return reinterpret_cast<const dummy *>(val_);
		  }
		    bool empty_;
		    char* val_;
		  };
		  
		  int main(){
		  	T t;
		    	if (t) {}
		  }
		  ```
	- ### 重载operator bool
		- ```cpp
		  operator bool() {
		    if (empty_) {
		      return false;
		    }
		    return true;
		  }
		  ```
-
-