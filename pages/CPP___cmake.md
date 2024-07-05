- ==只对命令的简单形式进行介绍==
- 参照《CMake构建实战——项目开发卷》
- find_file #CPP/cmake
	- ```cmake
	  find_file(<结果缓存变量> <文件名> [<候选路径...>])
	  
	  
	  find_file (
	            <VAR>
	            name | NAMES name1 [name2 ...]
	            [HINTS [path | ENV var]... ]
	            [PATHS [path | ENV var]... ]
	            [PATH_SUFFIXES suffix1 [suffix2 ...]]
	            [DOC "cache documentation string"]
	            [REQUIRED]
	  )
	  
	  # find_file NAMES可以指定多个候选文件，但是只会将第一个查找到的文件路径赋给变量
	  find_file(TEST_FILE_PATH NAMES test.cc CMakeLists.txt ".")
	  if(TEST_FILE_PATH)
	      message("TEST_FILE_PATH = ${TEST_FILE_PATH}")
	  else()
	      message("file not found")
	  endif()
	  ```
	- 该命令用于查找<文件名>对应文件的绝对路径，并将其存入<结果缓存变量>中。若其执行前<结果缓存变量>不为空，则该命令不执行，以免重复查找。若想强制查找，则需要编辑CMakeCache.txt，删除对应缓存变量的值。当文件查找失败时，<结果缓存变量>会被赋值为`<结果缓存变量>-NOTFOUND`
	- 失败 ![image.png](../assets/image_1720191197315_0.png)
	- 成功 ![image.png](../assets/image_1720191251547_0.png)
	- `find_file`会从一系列默认搜索路径中查找，`HINTS`或`PATHS`参数可以用于补充搜索的候选路径，该参数同时支持通过ENV指定<候选路径环境变量>，候选路径会从指定的环境变量中读取
	-
- find_package #CPP/cmake
	- 最重要的就是在`.cmake`文件中指定`INCLUDE_DIRS`和`LIBRARY_DIRS`的路径
	- ```cmake
	  # Findonnxruntime.cmake
	  find_path(onnxruntime_INCLUDE_DIR onnxruntime_c_api.h
	    HINTS ENV onnxruntime_ROOT
	    PATH_SUFFIXES include)
	  
	  find_library(onnxruntime_LIBRARY
	    NAMES onnxruntime
	    HINTS ENV onnxruntime_ROOT
	    PATH_SUFFIXES lib)
	  
	  find_file(onnxruntime_VERSION_FILE VERSION_NUMBER
	    HINTS ENV onnxruntime_ROOT)
	  
	  if(onnxruntime_VERSION_FILE)
	    file(STRINGS ${onnxruntime_VERSION_FILE} onnxruntime_VERSION LIMIT_COUNT 1)
	  endif()
	  
	  include(FindPackageHandleStandardArgs)
	  
	  find_package_handle_standard_args(onnxruntime 
	    REQUIRED_VARS onnxruntime_LIBRARY onnxruntime_INCLUDE_DIR 
	    VERSION_VAR onnxruntime_VERSION
	    HANDLE_VERSION_RANGE)
	  
	  if(onnxruntime_FOUND)
	    set(onnxruntime_INCLUDE_DIRS ${onnxruntime_INCLUDE_DIR})
	    set(onnxruntime_LIBRARIES ${onnxruntime_LIBRARY})
	  
	    add_library(onnxruntime::onnxruntime SHARED IMPORTED)
	    target_include_directories(onnxruntime::onnxruntime INTERFACE ${onnxruntime_INCLUDE_DIRS})
	    if(WIN32)
	      set_target_properties(onnxruntime::onnxruntime PROPERTIES 
	        IMPORTED_IMPLIB "${onnxruntime_LIBRARY}")
	    else()
	      set_target_properties(onnxruntime::onnxruntime PROPERTIES 
	        IMPORTED_LOCATION "${onnxruntime_LIBRARY}")
	    endif()
	  endif()
	  
	  # ===============================================================================================================
	  # CMakeLists.txt
	  cmake_minimum_required(VERSION 3.20)
	  project(find-onnxruntime)
	  
	  set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR};${CMAKE_MODULE_PATH}")
	  set(CMAKE_CXX_STANDARD 11) # 设置C++标准为11
	  set(onnx_version 1.10.0) # 根据下载的版本进行设置，本例使用1.10.0版本
	  
	  # 请下载onnxruntime库的压缩包，并解压至该目录中
	  if("$ENV{onnxruntime_ROOT}" STREQUAL "")
	    if(WIN32)
	        set(ENV{onnxruntime_ROOT} "${CMAKE_CURRENT_LIST_DIR}/onnxruntime-win-x64-${onnx_version}")
	    elseif(APPLE)
	        set(ENV{onnxruntime_ROOT} "${CMAKE_CURRENT_LIST_DIR}/onnxruntime-osx-universal2-${onnx_version}")
	    else()
	        set(ENV{onnxruntime_ROOT} "${CMAKE_CURRENT_LIST_DIR}/onnxruntime-linux-x64-${onnx_version}")
	    endif()
	  endif()
	  
	  find_package(onnxruntime 1.10) # 指定依赖的最小版本
	  add_executable(main main.cpp)
	  target_link_libraries(main onnxruntime::onnxruntime)
	  target_compile_definitions(main PRIVATE ORT_NO_EXCEPTIONS)
	  ```
-
-