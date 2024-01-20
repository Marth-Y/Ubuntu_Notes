- man手册 #Linux/常用命令 #Linux/搜索
  collapsed:: true
	- ```cpp
	       1   Executable programs or shell commands
	       2   System calls (functions provided by the kernel)
	       3   Library calls (functions within program libraries)
	       4   Special files (usually found in /dev)
	       5   File formats and conventions, e.g. /etc/passwd
	       6   Games
	       7   Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7)
	       8   System administration commands (usually only for root)
	       9   Kernel routines [Non standard]
	  ```
- pwd #Linux/常用命令
  collapsed:: true
	- `print working directory`：打印当前工作目录
- cd #Linux/常用命令 #Linux/文件系统/目录操作 #Linux/目录
  collapsed:: true
	- 改变当前目录
	- cd /：切换到根目录
	- cd ~：切换到用户的家目录
	- cd .：当前目录，`.`代表当前目录
	- cd ..：返回上级目录，`..`代表上一层目录
	- cd -：切换到上一次目录
		- env查看环境变量
		- 最后一行OLDPWD环境变量记录了上一次访问的目录
- rmdir #Linux/常用命令 #Linux/文件系统/目录操作 #Linux/目录
  collapsed:: true
	- `rmdir - remove empty directories`，只能删除空的文件夹，防止误删数据
- mkdir #Linux/常用命令 #Linux/文件系统/目录操作 #Linux/目录
  collapsed:: true
	- 可以一次性创建多个文件夹