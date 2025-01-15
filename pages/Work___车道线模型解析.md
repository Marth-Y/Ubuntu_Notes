- {{renderer :mermaid_6787b92b-1842-4bbf-a383-b40e9e01a021, 3}}
	- ```mermaid
	  flowchart TD
	   A[SetFeatureBuffer] -->|转换模型结果指针| B(Detector)
	   B --> C(polyfit lane)
	   B --> D(type)
	   B --> E(color)
	  ```
- # SetFeatureBuffer
	- ![[模型布局]]
	- SetFeatureBuffer中会将平台传过来的模型原始结果做指针的偏移，等数据的计算。
		- 包括
			- 模型结果指针ptr
			- 偏移量step，也就是一个channel的大小。
				- 其实就是front_far+front_near的模型输出的大小，是为了在后面取模型结果的时候做偏移用的。
			- 类型data_type，结果指针的数据类型
			- 宽高，模型原始输出的大小
		- ```cpp
		        const int map_type_index = map_infos_.at(cam_pos).map_index_info.map_type_index;
		        auto &ft_map_info = inference_features.at(map_infos_.at(cam_pos).map_id_info.map_type_id);
		        int ftm_h = ft_map_info.featmap_height + ft_map_info.padding_top + ft_map_info.padding_bottom;
		        int ftm_w = ft_map_info.featmap_width + ft_map_info.padding_left + ft_map_info.padding_right;
		        uint32_t step = std::max<uint32_t>(ftm_h * ftm_w , ft_map_info.padding_ch);
		  	  // 这里offset只是偏移掉front_far的，得到指向第一个channel front_near结果的指针。step才是后面偏移到第二个位置的关键信息大小
		        int offset = (cam_pos == common::CAMERA_FRONT_NEAR)? (ft_seg_ptr_offset + ft_map_info.padding_top) : ft_map_info.padding_top;
		        auto &host_ft_info = dst[map_type_index];
		        host_ft_info.ptr = ft_map_info.feature_ptr + offset * ftm_w * FeatureDataSize(ft_map_info.data_type);
		        host_ft_info.width = ftm_w;
		        host_ft_info.height = slice_rect.height;
		        host_ft_info.step = step * 2;
		        host_ft_info.scale = ft_map_info.scale;
		        host_ft_info.data_type = ft_map_info.data_type;
		        host_ft_info.rect = common::Rect(ft_map_info.padding_left, 0, slice_rect.width, slice_rect.height);
		        host_ft_info.argmax_channels=type_color_do_argmax_in_detector?ft_map_info.channel:1;
		  ```
- # Real Decode
	- 基于前面转换后的基础上真正decode lane和edge
	- ## 一、用valid输出对车道线进行合法筛选
		- ```cpp
		  template <class T>
		  void LaneDecoder::CheckValidAndSoftmax(const T *valid_data_ptr, const FeatureMapInfo &uf_feature_map_info, std::vector<std::vector<common::Point3f>> &lane_uf_pts) {
		    for (int c = 0; c < uf_lane_channels_; ++c) {
		      if (valid_data_ptr[c * 2] >= valid_data_ptr[c * 2 + 1]) {
		         continue;
		      }
		      std::vector<common::Point3f> pts;
		      UltraFastSoftmaxByDataType(uf_feature_map_info, c, pts, true);
		      lane_uf_pts.emplace_back(pts);
		    }
		  }
		  ```
	- ## 二、对一个channel的车道线做softmax
		- 对一个channel的每一行做一次softmax，得到一个点：
			- ```cpp
			  输入：
			    const uint32_t width = feature_map_info.width;
			    const uint32_t height = feature_map_info.height;
			    const uint32_t step = feature_map_info.step;
			    const float scale = feature_map_info.scale;
			    const common::Rect &rect = feature_map_info.rect;
			  
			  template<class T>
			  void LaneDecoder::UltraFastSoftmax(const T *feature_map_data_ptr,
			                                     const float scale, const uint32_t width,
			                                     const uint32_t height,
			                                     const common::Rect &rect,
			                                     const common::EigenArray &grid_idx,
			                                     std::vector<common::Point3f> &out,
			                                     const float &prb_thresh,
			                                     const bool &fill) {
			    Eigen::Map<const Eigen::Matrix<T, Eigen::Dynamic, Eigen::Dynamic, Eigen::RowMajor>>
			        input(feature_map_data_ptr, height, width);
			    Eigen::MatrixXd::Index maxRow, maxCol;
			    for (int h = input.rows() - 1; h >= 0; --h) {
			      int y = UFv_[h];
			      const Eigen::Array<T, Eigen::Dynamic, Eigen::Dynamic, Eigen::RowMajor>
			          &anchor = input.row(h).segment(rect.x, rect.width);
			      double max = anchor.maxCoeff(&maxRow, &maxCol);
			      if (maxCol < anchor.cols() - 1) {
			        const common::EigenArray &tmp =
			            (anchor.leftCols(anchor.cols() - 1).template cast<float>() / scale).exp();
			        const common::EigenArray &softmax = tmp / tmp.sum();
			        // almost 3 sigma from 1w frames
			        int exp_col = int((softmax * grid_idx).sum() + 0.5);
			        float prb = softmax(exp_col);
			        if (prb < prb_thresh) {
			          if (fill) {
			            out.emplace_back(common::Point3f(-1.f, y, 0.f));
			          }
			          continue;
			        }
			        float x = ((softmax * grid_idx).sum() + 0.5) *
			                  (net_input_width_ / uf_lane_grid_nums_);
			        out.emplace_back(common::Point3f(x, y, prb));
			      } else if (fill) {
			        out.emplace_back(common::Point3f(-1.f, y, 0.f));
			      }
			    }
			  }
			  ```
- > 完全可以自己实现一个cpp的单帧解析版本了，而且目前也确实有这个需求。有的新平台上面需要一个方便移植的解析工具 #Learn #Work
-
-