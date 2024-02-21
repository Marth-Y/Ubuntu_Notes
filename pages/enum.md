- `the enum hack`补偿 #enum #static #const
	- 当你在class编译期间需要使用一个class静态常量值时，编译器不允许"static 整数型 class 常量”完成“in class初值设定”的时候，可以用`the enum hack`补偿的方法。
		- ```cpp
		  class GamePlayer {
		    private:
		    	enum { NumTurns = 5 };
		      int scores[NumTurns];
		  };
		  ```
	- "the enum hack" 令 `NumTurns`成为5的一个记号名称。
	- `ths enum hack`的行为某方面比较像`#define`而不是`const`。如取`const`的地址是合法的，但取一个enum的地址不合法。，而取一个`#define`的地址也不合法。
	  logseq.order-list-type:: number
		- 如果你不想让别人获得 pointer 或 reference指向你的某个整数常量，enum 可以实现这个约束。
		  logseq.order-list-type:: number
	- `the enum hack`在许多代码中都有使用，需要看到时能够认识。且`enum hack`是`template metaprogramming`模板元编程的基础技术。
	  logseq.order-list-type:: number
-