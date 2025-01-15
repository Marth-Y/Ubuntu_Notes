- BTL状态 #各项目状态
	- 0730：车道线重新标定，[外参文件](https://yhikd4my59.feishu.cn/docx/RLBMdemF9olglxx7bc4ce2RLnVc)
		- ~~车道线异常，障碍物不显示。~~路面模糊导致
	- TODO X86回放无法跑通，结果异常。需要修复
	- 0811：车道线表现正常，但是BTL规控画龙。目前感觉是BTL规控问题。
	- 0815：文彧去芜湖体验eyeq和BTL。BTL是我们感知+BTL规控。
		- 采集了r150的弯道人开数据、直道居中数据、cutin相关数据。
		- eyeq体验下来eq的车80速度体验非常好…完全没有画龙，连轻微的方向盘修正都没有
	- 0821：BTL车道线给的没问题，需要BTL规控改
	- 1025：BTL规控说我们弯道曲率给的太大，我看下来符合预期。
- 分支
	- ```cpp
	  [lane_perception]
	  commit b1e19dd6cd4f33a635a3b04636aa85a9da47c84d (HEAD -> am62a_sdk_9.2, tag: 2408_refactor)
	  Author: luyimin <luyimin@nullmax.ai>
	  Date:   Wed Jul 31 13:56:20 2024 +0800
	  
	      Set switch of replay with pb
	  
	  [lane_fusion]
	  commit 1a25267cfe41fe1dca3d7042fd3d427053820e62 (HEAD -> am62a_sdk_9.2)
	  Author: sunhuibo <sunhuibo@nullmax.ai>
	  Date:   Mon Aug 5 17:59:53 2024 +0800
	  
	      turn height estimation off
	  
	  [common]
	  commit 41c910be0d09fa978b2e8432cd1613177d688cdd (HEAD -> BTL_sdk_9.2, origin/BTL_sdk_9.2)
	  Author: zhuwenyu <zhuwenyu@nullmax.ai>
	  Date:   Mon Jul 15 13:44:41 2024 +0800
	  
	      fix SlopeDiffStd input param type bug
	  
	  ```