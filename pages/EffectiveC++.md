- 让自己习惯C++
	- 条款01：视C++为一个语言联邦 #cpp
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
				- 因此引出了`logical constness`，一个`const`成员函数可以在客户端侦测不出的情况下，修改它所处理的对象内的某些`bits`。那么如何让客户端编译器侦测不出来，或者说：同意修改呢？ #mutable
					- 可以利用C++一个与`const`相关的摆动场：`mutable(可变的)`，它可以释放掉`non-static`成员变量的`bitwise constness`约束 #mutable
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
	- 条款05：了解C++默默编写并调用那些函数 #cpp #构造 #析构 #赋值运算符函数 #EffectiveC++
	  collapsed:: true
		- 空类
			- ==空类会被编译器声明一个拷贝构造、赋值运算符、析构、默认构造函数，所有都是public且inline的，唯有当这些函数被调用的时候才会被编译器创建出来。== #inline
			- 默认析构是non-virtual的，除非基类自身声明有虚析构，此时默认析构的虚属性来自基类。
			- 默认拷贝构造和赋值运算符函数，只是单纯的将每一个non-static成员变量拷贝到目标对象，默认拷贝会调用非内置类型的拷贝，对内置类型会直接拷贝。
			- 这四个函数，任意手动声明了一个，编译器则不再创建默认的。
			- 赋值运算符函数 #赋值运算符函数
				- 如果类中定义了引用类型成员变量或const类型成员变量，由于其值不能改变，编译器生成的赋值运算符不知道怎么做，因此不会生成默认的赋值运算符函数。如果基类赋值运算符函数是`private`的，编译器不会为派生类生成默认赋值运算符函数，因为编译器为派生类生成的默认赋值运算符函数想象中可以处理基类部分的成员变量，但是派生类无权调用基类的private函数。（基类部分直接调用基类的赋值运算符，但是是private的，所以不生成）
	- 条款06：若不想使用编译器自动生成的函数，就该明确拒绝 #EffectiveC++ #cpp #构造 #析构 #赋值运算符函数
	  collapsed:: true
		- 有时候一个类要求其不能被拷贝。则为了避免自动生成拷贝构造、赋值运算符函数，则可以显式的将其声明为private的(不实现定义)，从而使外部无法调用，阻止拷贝，而内部和友元函数调用没有定义的拷贝函数会发生链接错误(无法通过编译)。`collect2: error: ld returned 1 exit status`
			- C++的iostream就是如此阻止拷贝。
			- 也可以利用派生类不能调用基类private函数的特点，声明一个基类，然后继承基类：
				- ```cpp
				  class Uncopyable {
				  protected:
				      Uncopyable() {}
				      ~Uncopyable() {}
				  private:
				      Uncopyable(const Uncopyable&);
				      Uncopyable& operator=(const Uncopyable&);
				  };
				  ```
		- > 为驳回编译器自动提供的函数，可以将对应的成员函数声明为private并且不予实现。使用像Uncopyable这样的基类也可以。 #构造 #赋值运算符函数
	- 条款07：为多态基类声明virtual析构函数 #析构 #虚函数 #多态
	  collapsed:: true
		- 考虑多态情况：基类指针指向派生类，需要释放指针时，直接delete基类指针。此时基类是非虚析构函数，则通常只会释放基类成员空间，而派生类的成员则未释放，造成一个诡异的“局部销毁”对象，导致内存资源泄露。消除的方法很简单，将基类析构函数声明为virtual的，则派生类析构函数会覆盖基类析构函数，从而使成员都得到释放。==任何类只要带有虚函数都几乎确定应该也有一个虚析构函数==
		- 也不能无端的为没有虚函数的类声明虚析构函数，因为虚函数实现需要虚表，导致对象末尾会有虚表指针，从而改变了对象的大小（不再是成员变量大小的和）。影响代码的移植性，如C语言没有虚表指针的实现。
		- STL容器都没有实现虚析构函数，因此需要注意继承STL容器后用delete基类指针造成局部销毁。
		- 纯虚析构函数 #纯虚析构函数
			- 包含纯虚函数的抽象类不能被实体化。因此有时希望拥有抽象类，又没有任何纯虚函数，则可以将析构函数声明为纯虚析构函数。这个类则为抽象类，且不用担心析构问题。提示：必须为这个纯虚析构函数提供一份定义，编译器会在派生类的析构函数中创建一个对基类`~AWOV`的调用动作，所以必须提供一份定义，不然链接器会报错。
			- ```cpp
			  class AWOV {
			  public:
			    virtual ~AWOV() = 0;
			  };
			  AWOV::~AWOV() {}
			  ```
			- 析构函数运作方式：最深层的派生类的析构函数最优先调用（像一个出栈操作），然后依次运行其每一个基类的的析构函数。 #析构
			- 构造函数运行方式：从顶层基类开始向下依次调用构造函数构造。 #构造
		- > 1. 带多态性质的基类应该声明一个虚析构函数。如果类带有任何虚函数，它就应该拥有一个虚析构函数。 #多态 #析构 #虚函数
		  2. 类的设计目的如果不是为了作为基类或者实现多态，则不应该声明虚析构函数。
	- 条款08：别让异常逃离析构 #析构 #异常 #TODO
	  collapsed:: true
		- 我对异常不熟悉，此后再回看
	- 条款09：绝不在构造和析构过程中调用virtual函数 #构造 #析构 #虚函数
	  collapsed:: true
		- ==你不该在构造函数和析构函数期间调用虚函数，因为这样的调用不会带来你预想的结果，就算有，你也不会高兴，这是与java不同的一个地方==
		- 看如下示例：
			- ```cpp
			  #include <iostream>
			  using namespace std;
			  
			  class Transaction {
			  public:
			      Transaction() {
			          logTransaction();
			      }
			      virtual void logTransaction() const = 0;
			  };
			  
			  class BuyTransaction:public Transaction {
			  public:
			      virtual void logTransaction() const;
			  };
			  
			  class SellTransaction:public Transaction {
			  public:
			      virtual void logTransaction() const;
			  };
			  
			  
			  int main() {
			      BuyTransaction b;
			  }
			  ```
			- 当创建b时，会优先调用基类构造函数初始化基类成员部分，此时派生类部分还不存在。因此调用的虚函数是基类部分的版本，而不是派生类的。
				- 如果在构造基类时，允许调用派生类函数，那么可以明确的，派生类函数几乎肯定会使用派生类成员变量，而此时派生类成员变量还没有初始化，因此C++不允许这种操作。
				- 析构同理，当派生类析构后，派生类成员变量被视为不存在，基类中调用派生类函数不合法
			- 如果基类的虚函数有实现，那么构造和析构中的虚函数调用就会走基类版本，因此导致一些bug。==唯一能够避免这种问题的做法是：确定构造函数和析构函数(在对象被创建和销毁期间)都没有调用虚函数，而他们调用的所有函数也都服从这一约束。==
			- 那么如何保证每次一有Transaction继承体系上的对象被创建，就会有适当版本的函数被调用呢？一种做法是在Transaction中将logTransaction函数改为non-virtual的，然后要求派生类构造函数传递必要的信息给基类构造函数，基类便可以安全的调用non-virtual的 logTransaction。
				- ```cpp
				  class Transaction {
				  public:
				      explicit Transaction(const string& logInfo) {
				          logTransaction(logInfo);
				      }
				      void logTransaction(const string& logInfo) const;
				  };
				  
				  class BuyTransaction:public Transaction {
				  public:
				      BuyTransaction(const string& parameters)
				      :Transaction(createLogString(parameters)) {}
				  private:
				      static string createLogString(const string& parameters);
				  };
				  
				  ```
				- 即：==无法使用virtual函数从基类向下调用，而在构造期间，你可以令派生类将必要的构造信息向上传递至基类构造函数==
				- 使用静态成员函数createLogString创建参数向基类传递：利用辅助函数创建一个值传给基类比较方便、可读。令其为static的，就不会意外指向“早期对象尚未构建完成时未初始化的成员变量” #static
	- 条款10：令`operator=返回一个reference to *this` #赋值运算符函数
	  collapsed:: true
		- 为了实现连等，需要返回一个reference.
		- `T& operator=(const T& rhs);`
	- 条款11：在`operator=`中处理“自我赋值” #赋值运算符函数
	  collapsed:: true
		- “自我赋值”发生在对象被赋值给自己时。
			- 有明显的自我赋值：`vec = vec;`，也有潜在的难以识别的自我赋值：`a[i] = a[j];`、`*px = *py;`、`*pointer = reference;`
			- ```cpp
			  T& operator=(const T& rhs) {
			    delete p;
			    p = new Bitmap(*rhs.p);	//使用p的复件，即：新new一个空间
			    return *this;
			  }
			  ```
				- 如果是自我赋值，则`delete p`就已经销毁对象了。
		- 传统做法是藉由`operator=`最前面的一个“证同测试”达到“自我赋值”的检验目的：
			- ```cpp
			  T& operator=(const T& rhs) {
			    if (this == &rhs) return *this;
			    delete p;
			    p = new Bitmap(*rhs.p);
			    return *this;
			  }
			  ```
			- 这种做法具备“自我赋值安全性”，但是不具备“异常安全性”，如果后面的new发生异常(内存不足、拷贝异常等)，最终p会指向一块未知区域(delete掉了)，后续无法安全的删除它们，甚至无法安全的读取它们。
		- 更好的做法：这样兼顾了异常安全性。（往往operator=具备了一场安全性，就会自动获得自我赋值安全性）
			- ```cpp
			  T& operator=(const T& rhs) {
			    Bitmap* pOrig = p;			//记住原来的p
			    p = new Bitmap(*rhs.p);		//令p指向*p的一个副本,即：重新new一个空间
			    delete pOrig;					//删除原来的pOrig
			    return *this;
			  }
			  ```
			- 现在即使new异常，p也会指向原来的位置。保持原状。这段代码也能处理自我赋值，因为创建了一个副本。但是他不高效。
			- 如果“自我赋值”发生频率高，可以将证同测试加回来
		- 另一个确保异常安全和自我赋值安全的方法是：copy and swap技术：
			- ```cpp
			  class Widget {
			    void swap(Widget& rhs); // 交换rhs和*this的数据
			    Widget& operator=(const Widget& rhs) {
			      Widget temp(rhs);	  // 为rhs制作一份副本
			      swap(tmp);			  // 将*this数据和上述复件的数据交换
			      return *this;
			    }
			  };
			  
			  上面利用了一个临时变量，可以用by value的方式更加精简：
			  
			    Widget& operator=(Widget rhs) { // pass by value
			      swap(rhs);
			      return *this;
			    }
			  ```
		- > 确保对象自我赋值时，operator=有良好行为，其中技术包括证同测试、精心周到的语句顺序、copy and swap
		  确定任何函数如果操作一个以上对象，而其中多个对象是同一个对象时，其行为仍然正确。
	- 条款12：赋值对象时勿忘其每一个成分 #赋值运算符函数
	  collapsed:: true
		- 拷贝函数包括拷贝构造函数、赋值运算符函数
		- 复制所有local(本类中)成员变量
		  logseq.order-list-type:: number
		- 调用所有基类内的适当的拷贝函数
		  logseq.order-list-type:: number
			- ```cpp
			  class Base {
			  public:
			    Base(const Base& rhs);
			    Base& operator=(const Base& rhs);
			  };
			  class Dre1:public Base {
			  public:
			    Dre1(const Dre1& rhs)
			    :Base(rhs) {}					// 指定调用基类的拷贝构造函数，不然会调用默认构造
			    Dre1& operator=(const Dre1& rhs) {
			      Base::operator=(rhs);		// 对基类成分进行拷贝
			    }
			  };
			  ```
		- 注意不要为了代码精简，而让拷贝函数互相调用。
			- 如果为了消除代码重复，可以在private中定义一个`init`函数，将公共部分放入其中。
		- > 拷贝函数应该确保赋值对象内的所有成员变量以及所有基类部分
		  不要尝试以某个拷贝函数实现另一个拷贝函数，应该将功能机能放进第三个函数中，并由两个拷贝函数共同调用
- 资源管理
	-
-
-
-