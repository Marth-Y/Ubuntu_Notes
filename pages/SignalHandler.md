- 常见的错误信号处理是使用==栈回溯==的方法将接收到信号时的栈信息完全保存下来
- Linux上 [[typesence server]] 使用系统调用__UnwindBacktrace方法实现的
	- 类图 [Error_Handler | Visual Paradigm Online](https://online.visual-paradigm.com/w/zqhshvxu/diagrams/#diagram:workspace=zqhshvxu&proj=0&id=2&type=ClassDiagram)
	-
- [栈回溯](https://cloud.tencent.com/developer/article/1518094) #core_dump #栈 #SignalHandler
  collapsed:: true
	- linux内核栈回溯debug
	- 栈回溯实现方法之一：
		- ```cpp
		  #include <iostream>
		  #include <fstream>
		  #include <sstream>
		  #include <string>
		  #include <vector>
		  #include <map>
		  #include <execinfo.h>
		  #include <signal.h>
		  using namespace std;
		  
		  void print_backtrace(int signo)
		  {
		      int n;
		      int i;
		      char **s;
		      void *buff[50];
		  
		      n = backtrace((void **)&buff, sizeof(buff) / sizeof(void *));
		      s = backtrace_symbols(buff, n);
		      if (s == NULL)
		      {
		          return;
		      }
		      for (i = 0; i < n; i++)
		      {
		          printf("%s\n", s[i]);
		      }
		      free(s);
		  }
		  
		  void call_abort()
		  {
		      abort();
		  }
		  
		  int main()
		  {
		      signal(SIGABRT, print_backtrace);
		      call_abort();
		  }
		  ```
-