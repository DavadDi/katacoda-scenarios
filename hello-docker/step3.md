新建 docker 目录，并生成 `hello.txt` 文件。
`mkdir docker && cd docker && echo 'Hello' > hello.txt && cat hello.txt`{{execute}} 

通过命令行生成对应的 dockerfile 文件。
`echo -e "FROM nginx\nCOPY ./hello.txt /\nRUN cat /hello.txt" > Dockerfile`{{execute}} 

查看 dockerfile 文件内容。
`cat Dockerfile`{{execute}} 

通过 `docker build` 命令来创建镜像。
`docker build -t nginx-hello:v1 .`{{execute}} 

接着我们可以使用 `docker images` 来查看构建好的镜像。
`docker images`{{execute}}

我们也可以直接运行查看我们自己的镜像是否已经包含了 hello.txt 文件。
`docker run -d  -p 8080:80 nginx-hello:v1`{{execute}}

`export CID=$(docker ps|grep nginx-hello '{print $1}') `{{execute}} 导出 nginx 容器想的 ID。

查看我们自己添加到镜像中的 hello.txt 文件。
`docker exec -ti ${CID}  cat /hello.txt`{{execute}}
