# GitHub的简单推送流程

***

## 1、首次提交

```
cd ~/.ssh
ls
cat id_rsa.pub
#获取ssh密钥
```



> 电脑在需要的文件夹中打开git bash

> ```
> cd /你的项目路径
> git init
> #初始化
> /新建一个.gitignore 文件
> 内容：
> # Node
> node_modules/
> npm-debug.log
> .env
> 
> # IDE
> .idea/
> .vscode/
> *.swp
> 
> # OS
> .DS_Store
> Thumbs.db
> 
> git add .
> #添加所有文件
> 
> git commit -m 
> #初始提交
> 
> git remote add origin https://github.com/你的用户名/仓库名.git
> #关联远程仓库
> 
> git push -u origin main
> #推送本地内容到远程
> ```
>
> 
>
> 

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