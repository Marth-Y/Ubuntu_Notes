# 如何实现只能在堆上或者只能在栈上初始化的对象？
	- ## 只能在堆上
		- ### V1
			- 1. 禁止使用构造、拷贝构造、赋值运算符函数
			- 2. 创建一个static的函数创建对象
			- 3. 创建一个destroy函数析构对象(V2)
		- ### V2
			- 换一个角度，每个构造类函数在最后都需要调用析构函数，因此可以直接私有化析构函数
			  logseq.order-list-type:: number
		- ### V3 最佳实践
			- 上面两种方法使用的时候都需要创建，并手动删除。可以使用智能指针自动回收
			- 使用智能指针，传入删除器
		- ### 其他
			- 疑问：为什么不在析构中直接delete自己？
				- 首先：析构被私有化了，因此无法调用到
				- 其次：析构调用delete。delete有两步操作
					- 调用对象的析构函数。
					- 释放对象占用的内存。
					- 因此可能会导致无限递归调用。
				- 最后，就算加一些tag规避无限调用，但是当第二次进入析构判断tag的时候，因为这个对象已经析构了，会导致未定义的行为。
	- ## 只能在栈上
		- 在堆上生成对象有两种：
			- 1. 使用new关键字。
			- 2.使用malloc函数。malloc函数调用流程是先申请空间，之后调用placement new函数来调用构造函数，因此需要禁用定位new
		- 因此需要禁用：new、new[]、placement new
	- ## 代码
		- ```cpp
		  #include <iostream>
		  using namespace std;
		  
		  // 1. 如何定义只能在堆上生成的对象
		  // 1.1 构造函数私有化：：构造函数、拷贝构造、赋值运算符.
		  //     1.1.1:析构函数是所有构造类函数都需要调用的，，因此换个角度可以私有化析构函数
		  // 1.2 提供一个静态成员函数来创建对象
		  
		  class HeapOnlyV1 {
		   private:
		    // 私有化构造函数，禁止在栈上创建对象
		    HeapOnlyV1() { cout << "HeapOnly constructor called." << endl; }
		    HeapOnlyV1(const HeapOnlyV1&) = delete;             // 禁止拷贝构造
		    HeapOnlyV1& operator=(const HeapOnlyV1&) = delete;  // 禁止赋值运
		   public:
		    static HeapOnlyV1* create() {
		      return new HeapOnlyV1();  // 在堆上创建对象
		    }
		  };
		  
		  class HeapOnlyV2 {
		   private:
		    HeapOnlyV2() { cout << "HeapOnlyV2 constructor called." << endl; }
		    ~HeapOnlyV2() {
		      cout << "HeapOnlyV2 destructor called." << endl;
		    }  // 私有化析构函数
		    HeapOnlyV2(const HeapOnlyV2&) = delete;             // 禁止拷贝构造
		    HeapOnlyV2& operator=(const HeapOnlyV2&) = delete;  // 禁止赋值运算符
		   public:
		    static HeapOnlyV2* create() {
		      return new HeapOnlyV2();  // 在堆上创建对象
		    }
		    void destroy() {
		      delete this;  // 提供一个成员函数来释放内存
		    }
		  };
		  
		  #include <memory>
		  class HeapOnlyV3 {
		   private:
		    HeapOnlyV3() { cout << "HeapOnlyV3 constructor called." << endl; }
		    ~HeapOnlyV3() {
		      cout << "HeapOnlyV3 destructor called." << endl;
		    }  // 私有化析构函数
		    HeapOnlyV3(const HeapOnlyV3&) = delete;             // 禁止拷贝构造
		    HeapOnlyV3& operator=(const HeapOnlyV3&) = delete;  // 禁止赋值运算符
		   public:
		    static std::unique_ptr<HeapOnlyV3, void (*)(HeapOnlyV3*)> create() {
		      return {new HeapOnlyV3(), [](HeapOnlyV3* ptr) {
		                ptr->destroy();
		              }};  // 在堆上创建对象并提供自定义删除器
		    }
		    void destroy() {
		      delete this;  // 提供一个成员函数来释放内存
		    }
		  };
		  
		  // 2. 如何使用只能在栈上生成的对象
		  // 2.1 在堆上生成对象有两种：1. 使用new关键字。2.
		  // 使用malloc函数。malloc函数调用流程是先申请空间，之后调用placement
		  // new函数来调用构造函数
		  /**
		   * 因此需要禁用：new、new[]、placement new
		   */
		  
		  class StackOnly {
		   public:
		    StackOnly() { cout << "StackOnly constructor called." << endl; }
		    ~StackOnly() { cout << "StackOnly destructor called." << endl; }
		    void* operator new(size_t) = delete;             // 禁止使用new . 禁用new的时候就会把placement new也禁用掉，但是为了防止歧义，最后还是下面再写一次禁用
		    void* operator new[](size_t) = delete;           // 禁止使用new[]
		    void* operator new(size_t, void* ptr) = delete;  // 禁止使用placement new
		  };
		  
		  int main() {
		    {
		      // v1
		      HeapOnlyV1* obj = HeapOnlyV1::create();
		      // 注意：这里没有释放内存，实际使用中需要手动释放
		      delete obj;  // 释放内存
		    }
		    {
		      // v2
		      HeapOnlyV2* obj = HeapOnlyV2::create();
		      obj->destroy();  // 记得释放内存
		    }
		    {
		      // v3:最佳实践：：使用智能指针实现
		      auto obj = HeapOnlyV3::create();
		      // 使用智能指针自动管理内存
		    }
		    {
		      // StackOnly: 只能在栈上生成对象
		      StackOnly obj;  // 正确：在栈上创建对象
		      // StackOnly* p = new StackOnly();  // 错误：禁止使用new
		      // StackOnly* p2 = (StackOnly*)malloc(sizeof(StackOnly));  // 错误：禁止使用malloc
		    }
		    return 0;
		  }
		  ```