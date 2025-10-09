# GitHub的简单推送流程

***

## 1、首次提交

> 电脑在需要的文件夹中打开git bash

> ```
> git clone 仓库地址
> #链接仓库
> git bash
> #查看仓库状态
> git add -A
> git commit -m "操作名"
> git push -u origin main
> #推送
> git log
> #日志信息
> ```

### 2、修改更新

> 回到本地仓库位置（文件夹）打开git bash

> ```
> git pull
> #拉取更新
> git add -A
> git commit -m "操作名"
> git push -u origin main
> #推送
> ```