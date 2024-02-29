- 让自己习惯C++
	- 条款01：视C++为一个语言联邦 #CPP
	- 条款02：尽量以const、enum、inline替换# define #define #const #enum #EffectiveC++ #inline
	  collapsed:: true
		- 1、define不易于编译报错时查看报错信息
			- `#define ASPECT 1.63`
			- 对于编译器而言，会替换掉`ASPECT`，只有 1.63 。导致报错时只会显示1.63，无法定位具体出错的位置。
				- > 之前同事有一次始终编译不过，提示的一个宏有错误，幸好是知道改在哪儿的宏，不然编译器只报宏替换后的错，完全看不懂为什么报错了。
		- 2、define会替换所有位置，占用空间更大。
			- 如：上面定义一个常量宏，会替换所有位置的宏，占用多份儿空间。而定义 const常量只会占用一份的空间
		- 3、define不具备封装性，即：没有`private: #define `这种东西，而`const`、`enum`、`inline`都有 #inline
		- 4、宏函数追求更高的执行效率，但是也会有缺点：
			- `FUN(++a,b)`可能导致a被多次累加
			- 宏函数中需要给每个变量加括号，不然可能导致未定义的行为。
			- 宏函数不具备封装性
		- ==小结==：
			- 对于单纯常量，最好以`const`或者`enum`替换宏。
			- 对于宏函数，最好用`inline`替换。 #inline
	- 条款03：尽可能使用const #EffectiveC++ #const #static
	  collapsed:: true
		- 1、const修饰指针
			- {{embed ((65d604e7-6580-4230-a087-1ca03f46abe3))}}
		- 2、const修饰迭代器
			- STL迭代器const迭代器：`const_iterator` #const #CPP/STL
		- 3、const修饰返回值
			- ```cpp
			  const T operator*(const T& lhs, const T& rhs);
			  
			  T a,b,c;
			  (a * b) = c;   // 避免为a*b赋值
			  ```
		- 4、const成员函数
			- {{embed ((65d605a7-94a5-4469-948d-104a3ebc6f83))}}
			- ==两个成员函数如果只是常量性不同，可以被重载== #重载
				- ```cpp
				  class T {
				  public:
				    const char& operator[](size_t position) const   // const常量会调用
				    { return test[position]; }
				    
				    char& operator[](size_t position)               // 非const常量会调用
				    { return test[position]; }
				  };
				  
				  只要重载operator[]并对不同版本给予不同返回类型，就可以使const和non-const获得不同的处理。
				  ```
			- 成员函数是const有两个流行概念==bitwise constness(physical constness)和logical constness==
				- `bitwise constness`阵营人为：`const`成员函数不可以更改对象内任何`non-static`成员变量。即：不可以更改对象的任何一个`bit`。
					- 但是，如果一个对象有一个指针成员，那么修改指针指向的对象，而指针指向没有变，这就导致编译器认为对象没有改变，它是`bitwise constness`。
				- 因此引出了`logical constness`，一个`const`成员函数可以在客户端侦测不出的情况下，修改它所处理的对象内的某些`bits`。那么如何让客户端编译器侦测不出来，或者说：同意修改呢？
					- 可以利用C++一个与`const`相关的摆动场：`mutable(可变的)`，它可以释放掉`non-static`成员变量的`bitwise constness`约束
					- ```cpp
					  class T{
					  public:
					    mutable bool flag;       // 即使在const成员函数内也可以改变
					    
					    void Change() const {
					      flag = true;           // 现在可以改变了。
					    }
					  };
					  ```
			- 在const和non-const成员函数中避免重复——==运用const成员函数实现non-const== #常量性转除
				- 对`operator[]`分为const和non-const版本是好事儿，但是如果其中加入了大量其他代码，则会导致连个臃肿的函数：
					- ```cpp
					  const char& operator[](size_t position) const {
					    // 边界检查
					    // 日志访问记录
					    // 数据完整性检查
					    return test[position];
					  }
					  
					  char& operator[](size_t position) {
					    // 边界检查
					    // 日志访问记录
					    // 数据完整性检查
					    return test[position];
					  }
					  ```
					- 当然，我们可以将边界检查、日志访问、数据完整性检验等移入一个函数，然后用`operator[]`调用即可减少代码的臃肿，但是还是会有重复调用、两次returen语句重复。更好的方式是使用`常量性转除(casting away constness)`。因为两个重载函数中操作一样，只有返回值不一样。因此可以用non-const调用const版本 #常量性转除
					- ```cpp
					  char& operator[](size_t position) {
					    return const_cast<char&>(          // 将op返回值的const移除。
					      static_cast<const T&>(*this)     // 将*this转为const对象
					      [position]                       // 调用const op[]
					    );
					  }
					  ```
					- 不要用const反向调用non-const实现，因为const承诺不修改其内容，non-const可能会修改内容。
		- > 1. 编译器强制实施bitwise constness，但是你编写程序时应该使用“概念上的常量性(conceptual constness)"
		  2. 当const和non-const成员函数有实质等价实现时，用non-const版本调用const版本避免代码重复
		-
	- 条款04：确定对象被使用前已先被初始化 #EffectiveC++
	  collapsed:: true
		- > 读取未初始化的值会导致未定义的行为。如：一个int变量，某些语境下默认初始化为0，但是另一些语境可能不会被初始化为0.
		- 对于内置类型，必须手动初始化。对于类、结构体，必须在构造函数中将每一个成员初始化。
			- 对于类或结构体： #CPP/初始化列表
				- ```cpp
				  class T {
				  public:
				    T(const list<int>& phone, const string& name){
				      phone_ = phone;
				      name_ = name;
				      number = 0;
				    }
				  private:
				    list<int> phone_;
				    string name_;
				    int number_;
				  };
				  
				  以上只是赋值，不是初始化。这只是让对象带有我所期望的值，不是最佳初始化方法。
				  这个构造函数首先调用成员变量的默认构造为成员变量初始化，
				  然后为成员变量赋上指定的值。默认构造函数所做的初始化都是在浪费时间。
				  
				  C++规定，对象的成员变量的初始化动作发生在进入构造函数本体之前。
				  初始化的发生时间更早，发生于这些成员的默认构造函数被自动调用之时，此时未进入构造函数本体。
				  但是对number_不一定是这样，因为它属于内置类型，
				  不保证一定在你所看到的那个赋值动作的时间点之前获得初值，此处即为：number = 0；
				  
				  初始化最佳方法是使用初始化列表。
				  初始化列表将实参直接传给默认构造函数。
				  T(const list<int>& phone, const string& name)
				  :phone_(pnone)
				  ,name_(name)
				  ,number_(0) // 对于内置类型，其赋值操作和初始化的成本相同，为了一致性也用初始化列表初始化
				  {}
				  此时phone_以phone为初值进行拷贝构造，name_以name为初值进行拷贝构造。
				  甚至默认构造也可以如此实现：
				  T(const list<int>& phone, const string& name)
				  :phone_()
				  ,name_()
				  ,number_(0)
				  {}
				  ```
			- 有的class拥有多个构造函数，每个构造函数都有自己的初始化列表，若这个函数有大量成员变量或基类，则初始化列表有大量重复代码。此时可以将"赋值和初始化表现一样好"的成员变量，改用赋值操作，并将其移入一个`private`函数中供所有构造函数调用。以此来节省代码 #CPP/初始化列表 #CleanCode
		- ==C++成员初始化次序：基类比派生类优先初始化，类中成员变量以其声明次序被初始化== #CPP
		- 不同编译单元内定义的`non-local static`对象 #static
			- ==运用reference-returning 函数防止初始化次序问题==
			- static对象
				- 静态对象，其生命周期从被构造出来直到程序结束为止。因此，栈对象和堆对象都被排除在外。静态对象包括global对象、定义域namespace作用域内的对象、classs内的对象、函数内、file作用域内被声明为static的对象。
				- 其中，函数内的静态对象被称为`local static`对象。
				- 程序结束时，静态对象会被自动销毁，即：其析构函数会在`main()`结束时被自动调用。
			- 编译单元(translation unit)
				- 指产出单一目标文件的那些源码，基本上它是单一源码文件加上其所含入的头文件(`#include`)。
			- 看如下示例：
				- ```cpp
				  class FileSystem {
				  public:
				    std::size_t numDisks() const;
				  };
				  extern FileSystem tfs;                // the file system
				  ```
				- ```cpp
				  class Directory {
				  public:
				    Directory(params);
				  };
				  Directory::Directory(params) {
				    std::size_t disks = tfs.numDisks(); // 使用tfs对象
				  }
				  
				  Directory tempDir(params);
				  ```
				- 此时初始化顺序就显得尤为重要。ths必须在tempDir前初始化。他们是定义在不同编译单元中的`non-local static`对象，如何确定tempDir会在ths前被初始化呢？
				- 无法确定。C++对定义于不同编译单元中的non-local static对象的初始化次序没有明确定义。
					- 有一个`模板隐式具现化`的概念。以后再了解 #TODO
				- 但是有一个小技巧可以完美解决，将non-local static对象搬到专属函数内，在该函数内被声明为static，然后返回一个reference指向它，之后可以调用函数访问，而不直接访问。这就是单例模式的一种实现方式。即：用local static替换non-local static #单例模式
					- ```cpp
					  FileSystem& tfs(){
					    static FileSystem fs;
					    return fs;
					  }
					  
					  Directory& tempDir(){
					    static Directory td;
					    return td;
					  }
					  ```
					- 这个方式的基础在于：C++保证，函数内的local static对象会再“该函数被调用期间”“首次遇见该对象的定义式”时被初始化。
					- 这种方法还有一个好处：就是不调用这个non-local static对象的“仿真函数”，就不会引发构造和析构的成本。
					- 这个函数往往会被频繁调用，因此十分适合声明为`inline`的。 #inline
			- ==任何一种non-const static对象，不论是否local，在多线程环境下“等待某事发生”都会有麻烦，处理这个麻烦的一种做法是：在程序的单线程启动阶段(single-ehreaded startup portion)手动调用所有reference-returning函数，这可以消除与初始化有关的"竞速形势(race conditions)"== #TODO #static #多线程
		- > 1. 手动初始化内置类型，因为C++不保证初始化他们。
		  2. 构造函数使用初始化列表，初始化列表的排列次序与变量的声明次序相同。 #CPP/初始化列表 
		  3. 用local static对象替换non-local static对象。 #static
- 构造、析构、赋值运算
	- 条款05：了解C++默默编写并调用那些函数
		-