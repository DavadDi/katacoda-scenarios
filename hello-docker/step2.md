基于上一个场景中我们拉取的镜像，可以通过命令 `docker run` 来运行一个 container。

`docker run -ti -p 8080:80 nginx sh `{{execute}}

其中 `-ti` 是 `tty` 和 `inactive` 的缩写。`-p` 是把 container 的端口 `80` 导出到本机的 `8080` 端口。

通过上述命令，我们就已经登录到了 contianer 实例中。通过执行

`exit `{{execute}} 命令退出当前容器。

如果我们需要把运行的 container 启动到后台可以使用 `-d`。

`docker run -d nginx `{{execute}}

运行到后台以后，我们可以使用 `docker ps` {{execute}} 查看已经运行的 container 实例。

通过这个命令我们会获取到当前运行 container 的 ID 编号，接着我们可以使用 `docker exec` 命令登录到容器内部。

`export CID=$(docker ps|grep nginx|awk '{print $1}') sh`{{execute}} 导出 nginx 容器想的 ID。

登录到 Container 里面内部：
`docker exec -ti ${CID}  sh`{{execute}}，`exit`{{execute}} 退出容器。



如果我们想要在运行容器的时候挂载本地的目录，我们可以使用以下命令新建立一个目录：

`mkdir data && cd data && echo 'Hello' > hello.txt && cat hello.txt`{{execute}}  

运行一个容器 container，把当前 `data` 目录挂载到容器 container 内部的 `/data` 目录，首先我们需要导出当前目录 `export PWD=$(pwd)`{{execute}}，然后把当前目录中的 `data` 目录挂载到容器中，

`docker run -ti -v ${PWD}/data:/data nginx sh `{{execute}}，在进入到容器实例以后执行命令查看：

`cd /data && cat hello.txt`{{execute}}，然后在容器 container 里面执行 `echo "World" >> hello.txt`{{execute}} 并查看文件 `cat /data/hello.txt`{{execute}}， 然后退出容器 container `exit`{{execute}}。我们在当前宿主机上查看文件内容：

`cat data/hello.txt`{{execute}}。会发现我们在容器内部修改的文件内容，在退出容器以后仍然存在。

