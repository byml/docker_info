##  {#articleHeader1}

## 简介 {#articleHeader1}

[https://docs.docker.com/engine/docker-overview/](https://docs.docker.com/engine/docker-overview/)

Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的Linux 机器上，也可以实现虚拟化。

![](/images/docker.jpg)

## 容器 VS 虚拟机

![](https://byml.github.io/docker_info/images/docker-0.jpg)

## 架构

Docker 使用客户端-服务器 \(C/S\) 架构模式，使用远程API来管理和创建Docker容器。Docker 容器通过 Docker 镜像来创建。

Docker 包括三个基本概念

* 镜像（Image）
* 容器（Container）
* 仓库（Repository）![](/images/docker-architecture.svg)

## 特性

Docker的主要特性如下（摘自[Docker：具备一致性的自动化软件部署](http://www.infoq.com/cn/news/2013/04/Docker)\)：

1. 文件系统隔离：每个进程容器运行在完全独立的根文件系统里。
2. 资源隔离：可以使用cgroup为每个进程容器分配不同的系统资源，例如CPU和内存。
3. 网络隔离：每个进程容器运行在自己的网络命名空间里，拥有自己的虚拟接口和IP地址。
4. 写时复制：采用写时复制方式创建根文件系统，这让部署变得极其快捷，并且节省内存和硬盘空间。
5. 日志记录：Docker将会收集和记录每个进程容器的标准流（stdout/stderr/stdin），用于实时检索或批量检索。
6. 变更管理：容器文件系统的变更可以提交到新的映像中，并可重复使用以创建更多的容器。无需使用模板或手动配置。
7. 交互式Shell：Docker可以分配一个虚拟终端并关联到任何容器的标准输入上，例如运行一个一次性交互shell。

## 原理

Docker核心解决的问题是利用Linux 容器\(LXC\)来实现类似VM的功能，从而利用更加节省的硬件资源提供给用户更多的计算资源。

1. 隔离性 - 每个用户实例之间相互隔离, 互不影响。kernel namespace
2. 可配额/可度量 - 每个用户实例可以按需提供其计算资源，所使用的资源可以被计量。 Control Groups \(cgroups\)
3. 移动性 - 用户的实例可以很方便地复制、移动和重建。AUFS\(AnotherUnionFS\)

![](/images/linux-namespace.png)



采用AUFS作为docker的container的文件系统，能够提供如下好处：

1. 节省存储空间 - 多个container可以共享base image存储
2. 快速部署 - 如果要部署多个container，base image可以避免多次拷贝
3. 内存更省 - 因为多个container共享base image, 以及OS的disk缓存机制，多个container中的进程命中缓存内容的几率大大增加
4. 升级更方便 - 相比于 copy-on-write 类型的FS，base-image也是可以挂载为可writeable的，可以通过更新base image而一次性更新其之上的container
5. 允许在不更改base-image的同时修改其目录中的文件 - 所有写操作都发生在最上层的writeable层中，这样可以大大增加base image能共享的文件内容。



