## Docker

****

### 1、docker的相关概念

Docker是高效的软件部署技术。

> 相当于容器，包含着程序，依赖库和文件系统

![image-20251010215559696](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20251010215559696.png)

> Docker容器间公用一个系统内核，相比虚拟机更轻更小。

镜像仓库（Docker Registry）

> 镜像是容器的模板，类似软件安装包。
>
> 容器类似于用模具做i出来的糕点。
>
> 也可以比喻为镜像是游戏本体，容器是存档。
>
> Docker仓库用于存放和分享镜像。
>
> Docker的官方仓库[Docker Hub](https://hub.docker.com)

### 2、Docker镜像管理命令

****

#### `docker pull` - 下载镜像

 **功能**: 从Docker仓库下载镜像到本地。

 **镜像构成**: 一个完整的镜像名称包含四部分：`[registry_address/][namespace/]image_name[:tag]`

* `registry_address`: Docker仓库的注册表地址。`-docker.io`表示Docker Hub官方仓库，可省略。

* `namespace`: 命名空间，通常是作者或组织名称。`library`是Docker官方仓库的命名空间，可省略。
* `image_name`: 镜像的名称。
* `tag`: 镜像的标签名，通常表示版本号。`latest`表示最新版本，可省略。

 **示例**:

> `docker pull nginx`: 从Docker Hub官方仓库下载最新版Nginx镜像。
>
> `docker pull docker.n8n.io/n8nio/n8n`: 从N8n的私有仓库下载N8n镜像。

**Docker Hub网站**: https://hub.docker.com是官方仓库，可搜索、查看镜像详情（如官方镜像、版本号、使用说明）。 

#### **Registry (注册表) 与 Repository (镜像库)**:

* **==Registry==**: 整个Docker Hub网站可视为一个Registry。

* **==Repository==**: 一个Repository（如Nginx）存储了同一个镜像的不同版本。

####  **网络问题解决方案 (镜像站配置)**:

   **Linux**: 修改`/etc/docker/daemon.json`文件，添加`"registry-mirrors": ["https://<your-mirror-address>"]`，然后重启Docker服务（`sudo systemctl restart docker`）。

   **Windows/Mac**: 在Docker Desktop的设置中，进入“Docker Engine”配置项，在`registry-mirrors`中添加镜像站地址，点击“Apply & Restart”。

####  `docker images` - 列出本地镜像

**功能**: 列出所有已下载到本地的Docker镜像。

#### `docker rmi` - 删除镜像

 **功能**: 删除本地的Docker镜像。

 **参数**: 可指定镜像名称或ID。

####  镜像CPU架构 (`--platform`)

**背景**: Docker镜像作为软件，在不同的CPU架构下（如AMD64、ARM64）有不同的版本。

**默认行为**: `docker pull`命令默认会自动选择最适合当前宿主机CPU架构的镜像。

**特殊情况**:

对于某些低功耗迷你主机（如香橙派），其CPU架构通常为ARM64，需确认所需镜像是否提供ARM64版本。

 Mac电脑（ARM64架构）的Docker Desktop会使用QEMU模拟X86-64指令集，以兼容部分AMD64镜像，但可能存在兼容性或性能开销。



###  3. Docker容器管理命令

****

#### `docker run` - 创建并运行容器 (最重要命令)

* **功能**: 使用指定的镜像创建并运行一个容器。

* **自动拉取**: 如果本地不存在指定镜像，`docker run`会先自动拉取镜像，再创建并运行容器。

* **`docker ps`**: 查看正在运行的容器。

* 输出信息包括：`Container ID`（容器唯一ID）、`Image`（基于哪个镜像创建）、`Names`（容器名称）。

* **`docker ps -a`**: 查看所有容器（包括正在运行和已停止的）。

##### **`-d` (Detached Mode)**:

* **功能**: 让容器在后台执行，不阻塞当前终端窗口。

* **效果**: 控制台只打印容器ID，容器日志不会直接输出到终端。

##### **`-p` (Port Mapping / 端口映射)**:

* **背景**: Docker容器运行在独立的虚拟网络环境中，默认无法直接从宿主机访问容器内部网络。

* **功能**: 将宿主机的端口映射到容器内部的端口。

* **语法**: `-p <宿主机端口>:<容器内部端口>`（先外后内）。

* **示例**: `-p 80:80`将宿主机的80端口转发到容器内的80端口。

##### **`-v` (Volume Mounting / 挂载卷)**:

* **功能**: 将宿主机的文件目录与容器内的文件目录进行绑定。

* **目的**: 实现数据的**持久化保存**。当容器被删除时，容器内的数据也会被删除，但挂载卷可确保数据保存在宿主机上。

* *类型**:

* *绑定挂载 (Bind Mount)**: 直接将宿主机目录路径写入命令。

* *语法**: `-v <宿主机目录路径>:<容器内部目录路径>`。

* *注意**: 宿主机目录内容会覆盖容器内对应目录的原始内容。

* *命名卷挂载 (Named Volume)**: 让Docker自动创建一个存储空间，并为其命名。

* *创建命名卷**: `docker volume create <卷名称>`。

* *使用命名卷**: `-v <卷名称>:<容器内部目录路径>`。

* *特点**: 命名卷在第一次使用时，Docker会将容器的文件夹内容同步到命名卷进行初始化（绑定挂载无此功能）。

  \* **卷管理命令**:

   \* `docker volume ls`: 列出所有创建过的卷。

   \* `docker volume inspect <卷名称>`: 查看卷的详细信息，包括在宿主机的真实目录。

   \* `docker volume rm <卷名称>`: 删除一个卷。

   \* `docker volume prune`: 删除所有未被任何容器使用的卷。

 \* **`-e` (Environment Variables / 环境变量)**:

  \* **功能**: 向容器内部传递环境变量。

  \* **语法**: `-e <KEY>=<VALUE>`。

  \* **用途**: 常用于配置数据库账号密码等。

  \* **查找**: 可在Docker Hub镜像文档或开源项目的GitHub仓库中查找可用的环境变量。

 \* **`--name` (自定义容器名称)**:

  \* **功能**: 为容器指定一个自定义的、在宿主机上唯一的名称。

  \* **好处**: 方便记忆和管理。

 \* **`-it` (Interactive & TTY / 交互式终端)**:

  \* **功能**: 让控制台进入容器内部，获得一个交互式的命令行环境。

  \* **用途**: 临时调试容器，执行Linux命令。

  \* **语法**: `docker run -it <镜像名称> /bin/bash` (或`/bin/sh`)。

 \* **`--rm` (运行结束后自动删除)**:

  \* **功能**: 当容器停止时，自动将其从宿主机上删除。

  \* **常用组合**: 与`-it`联用，用于临时调试场景。

 \* **`--restart` (重启策略)**:

  \* **功能**: 配置容器停止时的重启行为。

  \* **常用策略**:

   \* `always`: 只要容器停止（包括内部错误崩溃、宿主机断电等），就会立即重启。

   \* `unless-stopped`: 除非手动停止容器，否则都会尝试重启。对于生产环境非常有用，可自动重启因意外停止的容器，而手动停止的容器不会再重启。

\* ### 容器启停与管理

 \* **`docker stop <容器ID或名称>`**: 停止一个正在运行的容器。

 \* **`docker start <容器ID或名称>`**: 重新启动一个已停止的容器。

 \* **参数保留**: 使用`stop`和`start`启停容器时，之前`docker run`时设置的端口映射、挂载卷、环境变量等参数都会被Docker记录并保留，无需重新设置。

 \* **`docker inspect <容器ID或名称>`**: 查看容器的详细配置信息。输出内容复杂，可借助AI辅助分析。

 \* **`docker create <镜像名称>`**: 只创建容器，但不立即启动。若要启动，需后续执行`docker start`命令。

\* ### 容器内部操作与调试

 \* **`docker logs <容器ID或名称>`**: 查看容器的运行日志。

  \* **`-f`**: 滚动查看日志，实时刷新。

 \* **Docker技术原理简述**:

  \* **Cgroups (Control Groups)**: 用于限制和隔离进程的资源使用（CPU、内存、网络带宽等），确保容器资源消耗不影响宿主机或其他容器。

  \* **Namespaces**: 用于隔离进程的资源视图，使得容器只能看到自己内部的进程ID、网络资源和文件目录，而看不到宿主机的。

  \* **本质**: Docker容器本质上是一个特殊的进程，但进入容器内部后，其表现如同一个独立的操作系统。

 \* **`docker exec` - 在容器内部执行命令**:

  \* **功能**: 在一个正在运行的Docker容器内部执行Linux命令。

  \* **语法**: `docker exec <容器ID或名称> <命令>`。

  \* **示例**: `docker exec my_nginx ps -ef`查看容器内进程。

  \* **进入交互式环境**: `docker exec -it <容器ID或名称> /bin/sh`（或`/bin/bash`）可进入容器内部获得交互式命令行环境，进行文件系统查看、进程管理或深入调试。

  \* **注意**: 容器内部通常是极简操作系统，可能缺失`vi`等常用工具，需要自行安装（如Debian系容器使用`apt update`和`apt install vim`）。



\## 5. Dockerfile - 构建镜像的蓝图



\* **定义**: Dockerfile是一个文本文件，详细列出了如何制作Docker镜像的步骤和指令，可类比为制作模具的图纸。

\* **基本结构与指令**:

 \* `FROM <基础镜像>`: 所有Dockerfile的第一行，选择一个基础镜像，表示新镜像在此基础上构建。

 \* `WORKDIR <目录路径>`: 设置镜像内的工作目录，后续命令在此目录下执行。

 \* `COPY <源路径> <目标路径>`: 将宿主机的文件或目录拷贝到镜像内的指定路径。

 \* `RUN <命令>`: 在镜像构建过程中执行的命令（例如安装依赖）。

 \* `EXPOSE <端口号>`: 声明镜像提供服务的端口（仅为声明，非强制，实际端口映射仍由`-p`参数决定）。

 \* `CMD <命令>`: 容器运行时默认执行的启动命令。一个Dockerfile只能有一个`CMD`指令。

 \* `ENTRYPOINT <命令>`: 与`CMD`类似，但优先级更高，不易被`docker run`命令覆盖。

\* **`docker build` - 构建镜像**:

 \* **功能**: 根据Dockerfile构建Docker镜像。

 \* **语法**: `docker build -t <镜像名称>[:<版本号>] <Dockerfile所在目录>`。

 \* **示例**: `docker build -t docker-test .` (在当前目录构建名为`docker-test`的镜像)。

\* **镜像推送至Docker Hub**:

1. **登录Docker Hub**: `docker login`。
2. **重新标记镜像**: `docker tag <本地镜像名称> <你的用户名>/<镜像名称>[:<版本号>]`。推送时镜像名称必须包含用户名作为命名空间。
3. **推送镜像**: `docker push <你的用户名>/<镜像名称>[:<版本号>]`。
4. **验证**: 在Docker Hub网站上可搜索到已推送的镜像，其他用户即可通过`docker pull`下载使用。



\## 6. Docker网络模式



\* ### Bridge (桥接模式)

 \* **默认模式**: 所有容器默认连接到此网络。

 \* **内部IP**: 每个容器被分配一个内部IP地址（通常是`172.17.x.x`开头）。

 \* **通信**: 同一Bridge网络内的容器可以通过内部IP地址互相访问。容器网络与宿主机网络默认隔离，需通过端口映射（`-p`）才能从宿主机访问。

 \* **自定义子网**:

  \* **创建**: `docker network create <子网名称>`。

  \* **加入**: `docker run --network <子网名称> ...`。

  \* **优势**:

   \* 同一子网内的容器可以使用**容器名称**互相访问（Docker内部DNS机制）。

   \* 不同子网之间默认隔离。

\* ### Host (主机模式)

 \* **功能**: Docker容器直接共享宿主机的网络命名空间。

 \* **IP地址**: 容器直接使用宿主机的IP地址。

 \* **端口**: 无需端口映射（`-p`），容器内的服务直接运行在宿主机的端口上，通过宿主机的IP和端口即可访问。

 \* **用途**: 解决一些复杂的网络问题。

 \* **语法**: `docker run --network host ...`。

\* ### None (无网络模式)

 \* **功能**: 容器不连接任何网络，完全隔离。

 \* **语法**: `docker run --network none ...`。

\* **网络管理命令**:

 \* `docker network ls`: 列出所有Docker网络（包括默认的bridge、host、none以及自定义子网）。

 \* `docker network rm <网络名称>`: 删除自定义子网（默认网络不可删除）。



\## 7. Docker Compose - 多容器编排



\* **背景**: 当一个完整的应用由多个模块（如前端、后端、数据库）组成时，若将所有模块打包成一个巨大容器，会导致故障蔓延、伸缩性差。若每个模块独立容器化，则管理多个容器（创建、网络配置）会增加复杂性。

\* **解决方案**: Docker Compose是一种轻量级的容器编排技术，用于管理多个容器的创建和协同工作。

\* **核心**: 使用YAML文件（通常命名为`docker-compose.yml`）定义多服务应用。

\* **YAML文件结构**: 可视为多个`docker run`命令按照特定格式组织在一个文件中。

 \* `services`: 顶级元素，每个服务对应一个容器。

 \* 服务名称（如`mongodb`）: 对应`docker run`中的`--name`，作为容器名的一部分。

 \* `image`: 对应`docker run`中的镜像名。

 \* `environment`: 对应`docker run`的`-e`参数。

 \* `volumes`: 对应`docker run`的`-v`参数。

 \* `ports`: 对应`docker run`的`-p`参数。

 \* **网络**: Docker Compose会自动为每个Compose文件创建一个默认子网，文件中定义的所有容器都会自动加入此子网，并可通过服务名称互相访问。

 \* `depends_on`: 定义容器的启动顺序，确保依赖服务先启动。

\* **AI辅助**: 可借助AI工具生成等价的Docker Compose文件。

\* **Docker Compose命令**:

 \* `docker compose up`: 启动YAML文件中定义的所有服务（容器）。

  \* `-d`: 后台运行。

  \* 会自动创建子网和容器。

 \* `docker compose down`: 停止并删除由Compose文件定义的所有服务和网络。

 \* `docker compose stop`: 仅停止服务，不删除容器。

 \* `docker compose start`: 启动已停止的服务。

 \* `docker compose -f <文件名.yml> up`: 指定非标准文件名的Compose文件进行操作。

\* **适用场景**: Docker Compose适合个人使用和单机运行的轻量级容器编排需求。

\* **与Kubernetes对比**: Kubernetes是企业级服务器集群和大规模容器编排的解决方案，功能更为复杂。



\## 8. 总结



以上内容涵盖了Docker的核心概念、在不同操作系统上的安装方法、常用的镜像与容器管理命令、Dockerfile的编写与镜像构建流程、Docker的多种网络模式，以及轻量级多容器编排工具Docker Compose的使用。这些是理解和应用Docker的关键知识点。