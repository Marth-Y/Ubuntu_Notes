- {{renderer :mermaid_6791b6c2-33be-494c-8007-27b12b6c1239, 3}}
	- ```mermaid
	  flowchart TD
	  A[Decodefrrespaceandcrosswalk] -->|遍历所有点| B(sigmoid)
	  B -->|阈值0.5| D[筛选前景点]
	  D --> E[计算连通域 cv::FindContours]
	  E --> F{freespace or crosswalk}
	  F -->|freespace| G[获取最大连通域]
	  F -->|cross walk| H[NMS,获取超过阈值的所有连通域]
	  G --> I[取边界]
	  H --> J[取所有边界]
	  I --> K[边界转点集]
	  J --> K
	  K --> R[坐标系转换，转body系]
	  
	  ```
-
-
-