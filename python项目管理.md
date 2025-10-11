# python项目管理的主要流程

****

### 1、利用venv为每个项目生产隔离的虚拟环境

> 以conda为例子
>
> ```
> conda env list 
> #查看conda创建的所有虚拟环境。
> conda create -n name python=3.1 
> #其中name是自定义的名称，python=3.1是一个格式，对应python环境的kernel版本
> conda activate name
> #虚拟环境的切换
> conda deactivate
> #退出已有的环境
> ```

### 2、用pip install命令安装所需要的包

> 以conda为例子
>
> ```
> pip install -r requirements.txt
> #根据requirements.txt的内容安装所需的包
> pip install package_name
> #安装包
> ```

### 3、复现环境，利用pip freeze命令

> requirements.txt相比pyproject.toml混合了多余的直接和间接依赖，因此可以利用uv

### 4、关于conda的一些指令

> ```
> conda activate env_name
> #激活虚拟环境
> conda remove --name env_name --all
> #删除虚拟环境
> conda remove --name env_name  package_name
> #删除虚拟环境中某个或者某些包
> conda env export --name myenv > myenv.yml
> #获得环境中的所有配置
> conda env create -f  myenv.yml
> #重新还原环境
> conda list
> #查看当前环境中安装了哪些包
> conda search package_name
> #检查当前是否由所需要的包
> conda install package_name
> #安装一个包
> conda install numpy=0.20.3
> #下载特定版本的包
> conda update numpy
> #更新包
> conda uninstall package_name
> #卸载包
> ```
>
> 
