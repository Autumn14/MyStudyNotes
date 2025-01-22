# Docker学习

## 1.下载和安装

**开启 Hyper-V 和容器功能**

- 打开 “控制面板”，选择 “程序和功能”。
- 点击 “启用或关闭 Windows 功能”。
- 勾选 “Hyper-V” 和 “容器”，然后点击 “确定”，系统会自动安装所需组件并重启。

**安装 Docker Desktop**

- **下载**：访问 Docker 官方下载页面，下载适用于 Windows 的 Docker Desktop 安装程序。
- **安装**：运行下载的安装程序，按照提示完成安装。安装完成后，Docker Desktop 会自动启动。
- **验证安装**：打开 PowerShell 或命令提示符，输入以下命令验证 Docker 是否安装成功：

```powershell
docker --version
```

## 2.基本概念

- **镜像（Image）**：是一个只读的模板，包含了运行应用程序所需的所有文件和配置信息，类似于虚拟机的镜像。
- **容器（Container）**：是镜像的运行实例，就像一个轻量级的虚拟机，可以独立运行应用程序。
- **仓库（Registry）**：用于存储和分发 Docker 镜像，Docker Hub 是 Docker 官方的公共仓库。

## 3.常用命令操作

镜像操作：

```powershell
# 从 Docker Hub 拉取镜像，这里以 Ubuntu 为例
docker pull ubuntu

# 查看本地所有镜像
docker images

# 删除本地镜像
docker rmi ubuntu
```

容器操作：

```powershell
# 基于镜像创建并启动一个容器，-it 表示交互式终端，/bin/bash 是启动后执行的命令
docker run -it ubuntu /bin/bash

# 查看正在运行的容器
docker ps

# 查看所有容器（包括已停止的）
docker ps -a

# 停止运行中的容器
docker stop <容器 ID 或名称>

# 启动已停止的容器
docker start <容器 ID 或名称>

# 删除容器
docker rm <容器 ID 或名称>
```

## 4.构建自定义镜像

创建一个名为 `Dockerfile` 的文件，示例内容如下：

```
# 使用基础镜像
FROM ubuntu

# 安装必要的软件包
RUN apt-get update && apt-get install -y curl

# 设置工作目录
WORKDIR /app

# 复制文件到容器中
COPY . /app

# 定义启动命令
CMD ["bash"]
```

在包含 `Dockerfile` 的目录下，使用以下命令构建镜像：

```powershell
docker build -t my-ubuntu-image .
```

这里 `-t` 用于指定镜像的名称和标签， `.` 表示使用当前目录下的 `Dockerfile`。
