- main函数 #main #argc #argv
  collapsed:: true
	- main函数原型：`int main(int argc, char* argv[]);`
	- `argc`是命令行参数数目，`argv`是指向参数的各个指针所构成的数组
	- 当内核执行C程序时，在调用main前先调用一个特殊的启动例程。可执行文件将此启动例程指定为程序的起始地址——由连接编辑器设置，而连接编辑器则由C编辑器调用。启动例程从内核取得命令行参数和环境变量值，然后为按上述方式调用main函数做好安排。 #环境变量 #启动例程
		- 启动例程会使从main返回后立即调用exit函数，若用C代码表示(实际上该例程常用汇编语言编写)，则它调用main函数的形式可能是：`exit(main(argc, argv));`
- 命令行参数 #exec #argc #argv #main
  collapsed:: true
	- 当执行一个程序时，调用exec的进程可将命令行参数传递给该新程序。这是UNIX shell的一部分常规操作。
	- ```cpp
	  #include <stdlib.h>
	  #include <stdio.h>
	  
	  
	  
	  int main(int argc, char* argv[]) {
	      int i;
	      for (i = 0; i < argc; ++ i) {
	          printf("argv[%d]:%s\n", i, argv[i]);
	      }
	  }
	  
	  
	  (base) ubuntu@VM-16-2-ubuntu:~/My_Code/zhihu$ ./test arg1 TEST foo
	  argv[0]:./test
	  argv[1]:arg1
	  argv[2]:TEST
	  argv[3]:foo
	  
	  ISO C和POSIX.1都要求argv[argc]是一个空指针。因此也可以这样写循环：
	  for (i = 0; argv[i] != NULL; ++ i)
	  ```