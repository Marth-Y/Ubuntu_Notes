- 模型存bin文件 #Work
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
-