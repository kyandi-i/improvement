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

