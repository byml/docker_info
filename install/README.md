# 安装与配置

安装 Docker

Docker 软件包已经包括在默认的 CentOS-Extras 软件源里。因此想要安装 docker，只需要运行下面的 yum 命令：

`yum install docker-io -y`

直接yum安装，安装成功后查看版本

`docker -v`

启动docker

`service docker start`

设置开机启动

`chkconfig docker on`

配置 Docker

因为国内访问 Docker Hub 较慢, 可以使用腾讯云提供的国内镜像源, 加速访问 Docker Hub

依次执行以下命令

`echo "OPTIONS='--registry-mirror=`[`https://mirror.ccs.tencentyun.com`](https://mirror.ccs.tencentyun.com)`'" >> /etc/sysconfig/docker`

`systemctl daemon-reload`

`service docker restart`

