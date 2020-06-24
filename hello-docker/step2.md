### 前台启动容器

基于上一个场景中我们拉取的镜像，可以通过命令 `docker run` 来运行一个 container。

`docker run -ti nginx sh `{{execute}}

其中 `-ti` 是 `tty` 和 `inactive` 的缩写。

通过上述命令，我们就已经登录到了 contianer 实例中。通过执行

`exit `{{execute}} 命令退出当前容器。



### 后台启动容器

如果我们需要把运行的 container 启动到后台可以使用 `-d`。

`docker run -d  -p 8090:80 nginx `{{execute}}  `-p` 是把 container 的端口 `80` 导出到本机的 `8090` 端口。

> katacoda 网络底层做了一定的限制，需要在 Terminal 的 + 号选择端口预览。

运行到后台以后，我们可以使用 `docker ps`{{execute}} 查看已经运行的 container 实例。

通过这个命令我们会获取到当前运行 container 的 ID 编号，接着我们可以使用 `docker exec` 命令登录到容器内部。

`export CID=$(docker ps|grep nginx|awk '{print $1}') `{{execute}} 导出 nginx 容器想的 ID。



### 登录到容器

登录到 container 里面内部：
`docker exec -ti ${CID}  sh`{{execute}}，`exit`{{execute}} 退出容器。



### 查看日志

我们还可以使用 `docker logs` 查看日志。

`docker logs -f  ${CID}`{{execute}}。`停止`{{execute interrupt T1}}。



### 文件通信

同时，我们还可以采用 `docker cp` 把当前文件 copy 到 container 的目录中或者从 container 目录中 copy 出来。

```bash
docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
```

`echo 'Hello' > hello.txt && cat hello.txt`{{execute}}，然后使用 cp 命令 `docker cp hello.txt ${CID}:/`{{execute}}，查看容器中的文件 `docker exec -ti ${CID}  cat /hello.txt`{{execute}}。

