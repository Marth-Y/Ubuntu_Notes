- git push #Git
	- `git remote add origin <仓库地址>`
	- 这样就可以推送到远程仓库
- git pull #Git
	- `git branch --set-upstream-to=origin/main`
	- 将pull关联到远程仓库的main分支
- git remote -v #Git
	- 查看远程仓库信息
	- ```cpp
	  lane_fusion git:(am62a_0618) git remote -v                
	  origin  git@git.nullmax.net:nullmax-dev/vision-perception/lane_fusion.git (fetch)
	  origin  git@git.nullmax.net:nullmax-dev/vision-perception/lane_fusion.git (push)
	  ```
	- 之后可以使用 `git remote set-url origin git@git.nullmax.net:nullmax-dev/vision-perception/lane_fusion.git`更改
-