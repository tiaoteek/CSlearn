Docker 把应用程序及其依赖，打包在 image 文件里面。只有通过这个文件，才能生成Docker 容器。**image 文件可以看作是容器的模板**。Docker 根据 image 文件生成容器的实例。同一个 image 文件，可以生成多个同时运行的容器实例。

# Docker命令

## image文件

image 是二进制文件。实际开发中，一个 image 文件往往通过继承另一个 image 文件，加上一些个性化设置而生成。举例来说，你可以在 Ubuntu 的 image 基础上，往里面加入 Apache服务器，形成你的 image。

```bash
# 列出本机的所有 image 文件。
$ docker image ls
# 删除 image 文件
$ docker image rm [imageName]
```

image 文件是通用的，为了节省时间，我们应该尽量使用别人制作好的 image 文件，即使要定制，也应该基于别人的 image 文件进行加工，而不是从零开始制作。

为了方便共享，image 文件制作完成后，可以上传到网上的仓库。Docker 的官方仓库 DockerHub 是最重要、最常用的 image 仓库。此外，出售自己制作的 image 文件也是可以的。

```bash
$ docker image pull library/hello-world
```

docker image pull 是抓取 image 文件的命令。library/hello-world 是 image 文件在仓库里面的位置，其中library 是 image 文件所在的组， hello-world 是 image 文件的名字。

由于 Docker 官方提供的 image 文件，都放在library 组里面，所以它的是默认组，可以省略。因此，上面的命令可以写成下面这样。

```bash
$ docker image pull hello-world
```

抓取成功以后，就可以在本机看到这个 image 文件了。

```bash
$ docker image ls
```

现在，运行这个 image 文件。

```bash
$ docker container run hello-world
```

docker container run 命令会从 image 文件，生成一个正在运行的容器实例。
注意， docker container run 命令**具有自动抓取 image 文件的功能**。如果发现本地没有指定的 image 文件，就会从仓库自动抓取。因此，前面的**docker image pull 命令并不是必需的步骤**。

```bash
$ docker container run hello-world
Hello from Docker!
This message shows that your installation appears to be working correctly
... ...
```

输出这段提示以后， hello world 就会停止运行，容器自动终止。有些容器**不会自动终止**，因为提供的是**服务**。

比如，安装运行 Ubuntu 的 image，就可以在命令行体验 Ubuntu 系统。

```bash
$ docker container run -it ubuntu bash
```

对于那些不会自动终止的容器，必须使用docker container kill 命令手动终止。

```bash
$ docker container kill [containID]
```

## container文件

image是软件的模板（类），container是真实运行的容器（实例）

一旦容器生成，就会同时存在两个文件： image 文件和容器文件。而且**关闭容器并不会删除容器文件**，只是容器停止运行而已。

```bash
# 列出本机正在运行的容器
$ docker container ls
# 列出本机所有容器，包括终止运行的容器
$ docker container ls --all
# 新建容器
$ docker container run [imageName]
# 通过containerID终止运行的容器
$ docker container rm [containerID]
```

## 制作个人镜像

1. 创建一个项目，在项目的根目录下，**新建一个文本文件.dockerignore** ，排除不要打包进image的 文件。

2. 在项目的根目录下，**新建一个文本文件 Dockerfile**，写入下面的内容。

```dockerfile
FROM node:8.4	#该 image 文件继承官方的node image,即8.4版本的node
COPY . /app		#将当前目录下的除了排除部分的所有文件，都拷贝进入image文件的/app目录
WORKDIR /app	#指定接下来的工作路径为/app
RUN npm install --registry=https://registry.npm.taobao.org	#命令安装依赖，并打包进入image文件 
EXPOSE 3000		#将容器3000端口暴露出来，允许外部连接这个端口
```

3. 有了 Dockerfile 文件以后，就可以使用docker image build 命令**创建 image 文件**了。

```bash
$ docker image build -t koa-demo .
# 或者
$ docker image build -t koa-demo:0.0.1 .
```

​		-t 参数用来指定 image 文件的名字

​		冒号指定标签，默认的标签就是latest

​		点表示 Dockerfile 文件所在的路径

​	如果运行成功，就可以看到新生成的 image 文件koa-demo 了。

```bash
$ docker image ls
```

4. docker container run 命令会**从 image 文件生成容器**。

```bash
$ docker container run -p 8000:3000 -it koa-demo /bin/bash
# 或者
$ docker container run -p 8000:3000 -it koa-demo:0.0.1 /bin/bash
```

​	**-p 参数：**容器的 3000 端口映射到本机的 8000 端口。
​	**-it 参数：**容器的 Shell 映射到当前的 Shell，然后你在本机窗口输入的命令，就会传入容器。
​	**koa-demo:0.0.1：**image 文件的名字（如果有标签，还需要提供标签，默认是latest 标签）。
​	**/bin/bash：**容器启动以后，内部第一个执行的命令 。这里是启动 Bash，保证用户可以使用 Shell。

有些启动了容器之后还有手动执行一些命令，可以用CMD执行。

RUN 命令与CMD 命令的区别在哪里？

- RUN 命令在 image 文件的构建阶段执行，执行结果都会打包进入 image 文件；
- CMD 命令则是在容器启动后执行。
- 一个 Dockerfile 可以包含多个RUN 命令，但是只能有一个CMD 命令。

指定了CMD 命令以后， docker container run 命令就不能附加命令了（比如前面的/bin/bash ），否则它会覆盖CMD 命令。

## 其他有用的命令



```bash
# 启动已经生成、已经停止运行的容器文件
$ docker container start [containerID]

# 用来终止容器运行
$ docker container stop [containerID]

# 用来查看 docker 容器的输出
$ docker container logs [containerID]

# 进入一个正在运行的 docker 容器
$ docker container exec -it [containerID] /bin/bash

# 从正在运行的 Docker 容器里面，将文件拷贝到本机。
$ docker container cp [containID]:[/path/to/file] .

```





# 使用docker镜像

## 安装docker可视化管理工具(`portainer`)

1. 拉取镜像

   ```bash
   $ sudo docker pull portainer/portainer-ce
   ```

2. 启动**portainer**

   ```bash
   $ sudo docker volume create portainer_data
   $ sudo docker run -d -p 9000:9000 --name portainer \
   --restart always -v /var/run/docker.sock:/var/run/docker.sock \
   -v portainer_data:/data portainer/portainer-ce
   ```

   > 打开9000端口 sudo ufw allow 9000    

## 安装nextcloud

在终端执行以下命令，拉取 Nextcloud 镜像：

```bash
$ docker pull nextcloud
```

拉取到的 Nextcloud 镜像的 tag 是 `latest`，显示以下信息即表示拉取成功：

```
Using default tag: latest
latest: Pulling from library/nextcloud
bc51dd8edc1b: Pull complete
a3224e2c3a89: Pull complete
```

执行以下命令，启动 Nextcloud 容器：

```bash
$ docker run -d --restart=always --name nextcloud -p 80:80 nextcloud
```

简单解释一下上述命令：

- docker run ：启动一个容器
- -d：后台运行容器
- --restart=always：Docker 重启的时候容器也会重启
- --name nextcloud：命名容器的 name 为 nextcloud，可以替代容器 id 使用
- -p 80:80：将容器的 80 端口映射到服务器的 80 端口
- nextcloud：要启动的镜像名称

执行之后会显示一个类似下面的长串字符，表示启动成功：

```
526306c7a591205f6d2cd417384571b358e738e3c8b52c16c1fc6f1893c8535f
```

也可以使用下面命令查看容器是否正常运行：

```bash
$ docker ps
```

如果显示以下内容，表明容器已经在运行中了：

```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                               NAMES
619d34210996        nextcloud           "/entrypoint.sh apac…"   1 hours ago        Up 1 hours         0.0.0.0:80->80/tcp                  nextcloud
```

 

## Docker 安装 Nginx

```bash
$ docker pull nginx:latest

$ docker images


```

