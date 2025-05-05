# 应用
- ## 实现if直接判等
	- ### 1.1 重载一个转换指针
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
	- ### 1.2 重载operator bool
		- ```cpp
		  operator bool() {
		    if (empty_) {
		      return false;
		    }
		    return true;
		  }
		  ```
- ## 四则运算
	- 乘法运算 `operator*`
	- ((6818b4fd-9951-4e45-b2d8-c8c58d802031))
- ## 隐式转换问题
	- ((6786923d-c431-4115-81d6-94b9f802f53d))
- ## 类的设计
	- ((6786923d-6ce9-4bcc-9c76-af435a355194))
- ## 资源管理
	- ((6786923d-897e-4740-9877-868ca1dc03f8))
-