---
tags: 小知识
---
# git push error  
在使用git向GitHub进行push代码时出现了以下错误：  
![avatar](https://s1.ax1x.com/2020/07/18/UgYoZt.jpg)
**解决方案：**
使用```git pull --rebase origin master```把本地的仓库更新到和GitHub同步
然后再使用```git push -u origin master```把代码push到GitHub上