- 模型存bin文件 #Work
  collapsed:: true
	- ```cpp
	    const std::map<std::string, int> channel_map{
	      {"750", 2},
	      {"752", 2},
	      {"753", 1},
	      {"754", 1},
	      {"755", 1},
	      {"776", 1}
	    };
	    for(const auto& it : inference_features) {
	      std::cout << it.second.padding_left << " right " << it.second.padding_right << " width " << it.second.featmap_width << " top " 
	                << it.second.padding_top << " bottom " << it.second.padding_bottom << " height " << it.second.featmap_height << " channel " << it.second.channel << "\n";
	      std::string file_name = std::to_string(frame_id_) + "_" + it.first + ".bin";
	      std::ofstream ofs(file_name, std::ios::binary);
	      size_t size = (it.second.padding_left + it.second.padding_right + it.second.featmap_width) * 
	                    (it.second.padding_top + it.second.padding_bottom + it.second.featmap_height) * it.second.channel * channel_map.at(it.first);
	      ofs.write((char*)(it.second.feature_ptr), size);
	      ofs.close();
	    }
	  ```
- 车道线消失问题分析 #Work #Work/车道线模型解析
  collapsed:: true
	- > 整体思路：先排查简单项，然后从源头开始往下分析
	- 旧项目：
		- 使用的数据是否正常
			- 分析odom是否正常。
			- 内外参是否正常。可以在后处理打印转换矩阵
		- 分析输入的模型结果指针类型是否正常，以及后处理是否用正常类型解析
	- 新适配的项目：
		- 使用的数据是否正常
			- odom是否正常
			- 内外参
		- 模型入图是否正常（记住裁切到模型入图大小）
		- 模型结果是否正常
		- 后处理处理的模型结果指针类型是否正常
		- 模型解析是否正常
- 想了解一下平台怎么检测的内存泄露：nm_monitor_load可执行程序 #Work #Learn
- [[Work/车道线模型解析]]
-