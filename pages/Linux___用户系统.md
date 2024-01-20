- Linux用户子系统 #Linux/用户系统
  collapsed:: true
	- 用户分为：
		- 特权用户（超级用户、根用户）：root-->拥有所有权限
		- 普通用户
			- sudoers
				- 可以使用`sudo`临时拥有特权用户的权限
				- 安装OS时默认创建的就是sudoers
			- 其他用户
	- 查看所有用户的方式：`cat /etc/passwd`
		- `ubuntu:x:1000:1000:ubuntu:/home/ubuntu:/bin/bash`以`:`分割
			- x：密码（已废弃）
			- 第一个1000：用户id
			- 第二个1000：用户组id
			- `/home/ubuntu`：家目录
			- `/bin/bash`：shell
	- 添加用户：`useradd`
		- `useradd luyimin`
		- 添加后：
			- `luyimin:x:1002:1002::/home/luyimin:/bin/sh`
				- 没有自动创建家目录，使用-m参数
				- 默认的shell程序是sh，使用-s参数
				- `sudo useradd -m -s /bin/bash luyimin`
					- -s和bash不能分开。
	- 删除用户：`userdel`
		- `userdel luyimin`
			- 但是删除的时候不会删除用户文件和家目录。要加-r
			- `sudo userdel luyimin -r`
	- 切换用户`su`
		- s：switch
		- u：user
		- su会以栈形式保存切换的用户，就像浏览器的前进后退一样。
	- 退出切换`exit`，和`su`组成栈结构
	- 设置用户密码`passwd`
		- `sudo passwd username`
		- 可以使用其更改root密码
	- 修改sudoers
		- `sudo vim /etc/sudoers`
		- ```cpp
		  # User privilege specification
		  root    ALL=(ALL:ALL) ALL
		  
		  # Members of the admin group may gain root privileges
		  %admin ALL=(ALL) ALL
		  
		  # Allow members of group sudo to execute any command
		  %sudo   ALL=(ALL:ALL) ALL
		  
		  ```
-