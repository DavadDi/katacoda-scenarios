##  镜像管理

我们可以使用 `docker pull` 命令来从公开的 docker hub 仓库中拉取镜像，公共镜像不需要登录既可以拉取。
`docker pull nginx`{{execute}}

接着我们可以使用 `docker images` 来查看当前系统中拉取到的镜像。
`docker images`{{execute}}

我们可以使用 `docker history nginx` 来查看 *nginx* 镜像的构建历史。

`docker history nginx`{{execute}}

需要想进一步了解 nginx 镜像更加详细的信息可以使用 `docker inspect` 命令进行查看：

`docker inspect nginx`{{execute}}

如果我们计划把当前镜像推动到我们自己的镜像仓库，可以使用 `docker tag` 的命令来对当前镜像添加别名

`docker tag nginx myregestry.com/pub/nginx:latest`{{execute}}

后续我们可以采用 `docker login myregestry.com`，然后使用命令 `docker push myregestry.com/pub/nginx:latest` 把本地镜像推送到我们自己的镜像仓库。



