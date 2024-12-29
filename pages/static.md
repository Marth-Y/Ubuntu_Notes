- 生命周期和初始化时机
	- 局部静态对象在程序的执行路径第一次经过对象时初始化，直到程序终止才被销毁，在此期间，即使局部静态对象所在函数块运行结束也不会对它有影响。
	-
- 类中静态常量 #static #const
	- ```cpp
	  class GamePlayer {
	    private:
	    	static const int NumTurns = 5;
	      int scores[NumTurns];
	  };
	  ```
	- 以上是一个声明式，而非定义式，通常C++要求你对任何使用的任何东西提供一个定义式。
	- 如果它是一个class的专属静态常量且为整数类型(如：int、char、bool)，则需要特殊处理。只要不取他们的地址，可以声明并使用它们而无需提供定义式。如果要取地址，或者编译器必须要有定义式，则需要显示提供定义式：`const int GamePlayer::NumTurns;`
	  logseq.order-list-type:: number
		- 将这个式子放入实现文件中，由于常量在声明时已经赋值了，所以在上面的定义式不再设置初值。=="in-class 初值设定"==
		  logseq.order-list-type:: number
		- 如果有的旧编译器不允许声明式初始化初值，或者static不是整型，则在定义式设初值即可。
		  logseq.order-list-type:: number
-