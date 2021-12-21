Docker 属于 Linux 容器的一种封装，提供简单易用的容器使用接口。Docker 将应用程序与该程序的依赖，打包在一个文件里面。运行这个文件，就会生成一个虚拟容器。程序在这个虚拟容器里运行，就好像在真实的物理机上运行一样。有了 Docker，就不用担心环境问题。

[Docker的ubuntu版本官方安装](https://docs.docker.com/engine/install/ubuntu/)

[Docker的RHEL版本官方安装](https://docs.docker.com/engine/install/rhel/)

快速安装方式：

   ```bash
$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh --mirror Aliyun
#$ sudo sh get-docker.sh --mirror AzureChinaCloud
   ```

 执行这个命令后，脚本就会自动的将一切准备工作做好，并且把 Docker 的稳定(stable)版本安装在系统中。

安装完成后，运行下面的命令，验证是否安装成功。

```bash
$ docker version
# 或者
$ docker info
```

Docker 需要用户具有 sudo 权限，为了避免每次命令都输入sudo ，可以把用户加入Docker 用户组（官方文档）。

```bash
$ sudo usermod -aG docker $USER
```

Docker 是服务器----客户端架构。命令行运行docker 命令的时候，需要本机有 Docker 服务。如果这项服务没有启动，可以用下面的命令启动（官方文档）。
```bash
# service 命令的用法
$ sudo service docker start

# systemctl 命令的用法
#启动
$ sudo systemctl start docker
#重启
$ sudo systemctl restart docker
#开机启动
$ sudo systemctl enable docker
```

设置docker国内镜像

```bash
$ sudo nano /etc/docker/daemon.json
```

添加如下内容

```json
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
```

> **Docker**是一个开源的应用容器引擎，基于[Go语言](https://link.juejin.cn?target=https%3A%2F%2Fwww.runoob.com%2Fgo%2Fgo-tutorial.html)并遵从**Apache2.0**协议开源。 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的**Linux**机器上，也可以实现虚拟化。 容器是完全使用沙箱机制，相互之间不会有任何接口,更重要的是容器性能开销极低。

   > 警告：切勿在没有配置 Docker APT 源的情况下直接使用 apt 命令安装 Docker.

