# uv管理python

uv的下载方式

```
curl -LsSf https://astral.sh/uv/install.sh | sh
#macOS/Linux
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
#Windows
```

---

相关命令

```
###基本操作
1|uv --version
#查看uv的版本信息

2|uv python list
#查看系统中可用的python脚本

3|uv python install 3.11
#安装特定版本python

4|uv python uninstall 3.13
#卸载已安装的python版本

5|uv python upgrade
#升级python版本

6|uv python pin 3.11
#将项目的python版本锁定为3.11
（此操作将会在目的项目的根目录下创建一个.python-version文件，记录当前使用的python版本）

7|uv init name 
#初始化一个名为name的项目
（此操作会自动添加.gitignore,.python-version,main.py,pyproject.toml,readme.md文件）

###管理虚拟环境
1|uv venv
#创建并且激活虚拟环境

2|source.venv/bin/activate
#激活环境（macOS/Linux）

3|.venv\scripts\activate
#激活环境（Windows）

###项目管理依赖
1|uv add requests
#添加request库作为项目依赖

2|uv lock
#锁定依赖

3|uv run script,py
#运行项目

4|uv init --app myapp
#使用--app来建立应用程序式的专案，会在myapp/目录中建立src/myapp/的结构，并且包含_main_.py作为程式进入点。

5|uv init --lib mylib
#建立可封装的函式库（可以被import）

6|uv init --python 3.12
#指定使用特定python版本

###操作脚本
1|uv init --script myscript.py
#使用--script建立独立的python脚本档案，会在档案顶部加入特殊依赖区块，让脚本可以独立管理自己的依赖，脱离被完整专案结构的约束

2|uv init --script myscript.py --python 3.12
#指定python版本要求，会加入requires-python设定

3|uv run --with click myscript.py
#执行脚本时临时加载额外的依赖

4|uv add --script myscript.py click
#添加依赖到脚本中。可被remove

###管理项目依赖
1|uv sync
#根据pyproject.toml和requirement.txt安装所有依赖

2|uv version
#check版本号，读取pyproject.toml的version

3|uv add requests httpx
#新增依赖套件

4|uv remove requests
#移除依赖套件

5|uv add --add pytest ruff
#加入开发依赖

6|uv run pytest
#在项目的虚拟环境中执行已经安装的命令列工具

7|uv tree
#显示依赖树状结构

8|uv lock --upgrade
#更新所有依赖到最新版本，不修改pyproject.toml的版本要求

9|uv add -r requirements.txt
#从现有的.txt档案中读取并加入所有套件到专案中，方便从旧专案迁移

###对于uv
1|uv help
#对于uv的说明文件

2|uv self version
#显示当前uv版本号

3|uv self update
#更新uv到最新版本
```

