# 基础 #lua
	- 注释 #lua
	  collapsed:: true
		- ```lua
		  --- 单行注释
		  --[[
		  	多行注释
		  ]]
		  ```
	- `print` #lua
	  collapsed:: true
		- ```lua
		  print("Hello World")
		  Hello World
		  
		  print("Hello World", "I am cool")
		  Hello World (table) I am cool
		  
		  print("Hello" .. "I am cool")
		  '..' means concat them
		  HelloI am cool
		  ```
	- Variables & Data Types #lua
	  collapsed:: true
		- ```lua
		  main.lua
		    nil (= null)
		    number 1 2 -11 9.89
		    string "asdasda" 'sadasd'
		    boolean true false
		    tables (arr)
		    local name = nil
		    print(name) ---nil
		    ---local：局部变量，不能在本文件之外使用
		    GlobalVar = 10
		    ---正常定义的(首字母大写)，全局变量。可在文件外使用
		    可以+ _G：_G.GlobalVar 表明这是全局变量
		  local f = [[
		    test
		    wdasdad
		    asdas
		    asdasdasdadsadsad
		  ]] ---string
		  
		  ---定义多个变量
		  local one, two, three = "one", 2, false
		  ```
	- string #lua
		- ```lua
		  ---在字符串变量前+#，意味着获取变量的长度
		  x = "hello world"
		  print(#x) --- 11
		  x = #"hello world"
		  print(x) --- 11
		  
		  ---转string
		  local num = 20
		  local str = tostring(num)
		  print(type(num), type(str))
		  ---number string
		  
		  
		  ```
-
-