- std::enable_shared_from_this #CPP/智能指针 #CPP/newdelete
  title:: CPP/智能指针
  collapsed:: true
	- ## std::enable_shared_from_this使用场景
	- 在很多场合，经常会遇到一种情况，如何安全的获取对象的this指针，一般来说我们不建议直接返回this指针，可以想象下有这么一种情况，返回的this指针保存在外部一个局部/全局变量，当对象已经被析构了，但是外部变量并不知道指针指向的对象已经被析构了，如果此时外部使用了这个指针就会发生程序奔溃。既要像指针操作对象一样，又能安全的析构对象，很自然就想到，智能指针就很合适！
	- 那么智能指针如何使用呢？现在我们来看一段代码。
		- ```cpp
		  #include <iostream>
		  #include <memory>
		  
		  class Widget{
		  public:
		      Widget(){
		          std::cout << "Widget constructor run" << std::endl;
		      }
		      ~Widget(){
		          std::cout << "Widget destructor run" << std::endl;
		      }
		  
		      std::shared_ptr<Widget> GetSharedObject(){
		          return std::shared_ptr<Widget>(this);
		      }
		  };
		  
		  int main()
		  {
		      std::shared_ptr<Widget> p(new Widget());
		      std::shared_ptr<Widget> q = p->GetSharedObject();
		  
		      std::cout << p.use_count() << std::endl;
		      std::cout << q.use_count() << std::endl;
		  
		      return 0;
		  }
		  ```
	- 编译运行后程序输出如下：
		- ```cpp
		  Widget constructor run
		  1
		  1
		  Widget destructor run
		  Widget destructor run
		  22:06:45: 程序异常结束。
		  ```
	- 从输出我们可以看到，调用了一次构造函数，却调用了两次析构函数，很明显这是不正确的。而std::enable_shared_from_this正是为了解决这个问题而存在。
	- ## std::enable_shared_from_this原理和实战
	- 前面我们说使用std::enable_shared_from_this能解决安全获取this指针的问题。在使用之前，我们先来了解下std::enable_shared_from_this是什么？为什么能解决这个问题？`std::enable_shared_from_this`定义如下：
		- ```cpp
		  template<class _Tp>
		  class _LIBCPP_TEMPLATE_VIS enable_shared_from_this
		  {
		      mutable weak_ptr<_Tp> __weak_this_;
		  protected:
		      _LIBCPP_INLINE_VISIBILITY _LIBCPP_CONSTEXPR
		      enable_shared_from_this() _NOEXCEPT {}
		      _LIBCPP_INLINE_VISIBILITY
		      enable_shared_from_this(enable_shared_from_this const&) _NOEXCEPT {}
		      _LIBCPP_INLINE_VISIBILITY
		      enable_shared_from_this& operator=(enable_shared_from_this const&) _NOEXCEPT
		          {return *this;}
		      _LIBCPP_INLINE_VISIBILITY
		      ~enable_shared_from_this() {}
		  public:
		      _LIBCPP_INLINE_VISIBILITY
		      shared_ptr<_Tp> shared_from_this()
		          {return shared_ptr<_Tp>(__weak_this_);}
		      _LIBCPP_INLINE_VISIBILITY
		      shared_ptr<_Tp const> shared_from_this() const
		          {return shared_ptr<const _Tp>(__weak_this_);}
		  
		  #if _LIBCPP_STD_VER > 14
		      _LIBCPP_INLINE_VISIBILITY
		      weak_ptr<_Tp> weak_from_this() _NOEXCEPT
		         { return __weak_this_; }
		  
		      _LIBCPP_INLINE_VISIBILITY
		      weak_ptr<const _Tp> weak_from_this() const _NOEXCEPT
		          { return __weak_this_; }
		  #endif // _LIBCPP_STD_VER > 14
		  
		      template <class _Up> friend class shared_ptr;
		  };
		  ```
	- `std::enable_shared_from_this`是模板类，内部有个_Tp类型weak_ptr指针，调用shared_from_this成员函数便可获取到_Tp类型智能指针，从这里可以看出，_Tp类型就是我们的目标类型。再来看看std::enable_shared_from_this的构造函数都是protected，因此不能直接创建std::enable_from_shared_from_this类的实例变量，只能作为基类使用。因此使用方法如下代码所示：
		- ```cpp
		  #include <iostream>
		  #include <memory>
		  
		  class Widget : public std::enable_shared_from_this<Widget>{
		  public:
		      Widget(){
		          std::cout << "Widget constructor run" << std::endl;
		      }
		      ~Widget(){
		          std::cout << "Widget destructor run" << std::endl;
		      }
		  
		      std::shared_ptr<Widget> GetSharedObject(){
		          return shared_from_this();
		      }
		  };
		  
		  int main()
		  {
		      std::shared_ptr<Widget> p(new Widget());
		      std::shared_ptr<Widget> q = p->GetSharedObject();
		  
		      std::cout << p.use_count() << std::endl;
		      std::cout << q.use_count() << std::endl;
		  
		      return 0;
		  }
		  ```
	- 这里为什么要创建智能指针p而不是直接创建裸指针p？根本原因在于std::enable_shared_from_this内部的weak_ptr，若只是创建裸指针p，那么p被delete后仍然面对不安全使用内部this指针问题。因此p只能被定义为智能指针。当p被定义为shared_ptr智能指针后，p指针引用计数是1(weak_ptr不会增加引用计数)，再通过shared_from_this获取内部this指针的智能指针，则p的引用计数变为2。
	- 现编译运行输出如下：
		- ```cpp
		  Widget constructor run
		  2
		  2
		  Widget destructor run
		  ```
	- 正确的返回了智能指针，p和q的引用计数都是2，且只调用了一次构造函数和析构函数，不会错误的析构对象多次。
	-
-