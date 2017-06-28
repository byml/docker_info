

## 简介 {#articleHeader1}

![](/images/docker.jpg)

## 容器 VS 虚拟机

![](https://byml.github.io/docker_info/images/docker-0.jpg)

## 架构

Docker 使用客户端-服务器 \(C/S\) 架构模式，使用远程API来管理和创建Docker容器。Docker 容器通过 Docker 镜像来创建。

![](https://byml.github.io/docker_info/images/docker-1.jpg)

## 特性

Docker的主要特性如下（摘自[Docker：具备一致性的自动化软件部署](http://www.infoq.com/cn/news/2013/04/Docker)\)：

1. 文件系统隔离：每个进程容器运行在完全独立的根文件系统里。
2. 资源隔离：可以使用cgroup为每个进程容器分配不同的系统资源，例如CPU和内存。
3. 网络隔离：每个进程容器运行在自己的网络命名空间里，拥有自己的虚拟接口和IP地址。
4. 写时复制：采用写时复制方式创建根文件系统，这让部署变得极其快捷，并且节省内存和硬盘空间。
5. 日志记录：Docker将会收集和记录每个进程容器的标准流（stdout/stderr/stdin），用于实时检索或批量检索。
6. 变更管理：容器文件系统的变更可以提交到新的映像中，并可重复使用以创建更多的容器。无需使用模板或手动配置。
7. 交互式Shell：Docker可以分配一个虚拟终端并关联到任何容器的标准输入上，例如运行一个一次性交互shell。



