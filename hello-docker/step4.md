通过 docker 设置命令行的方式设置资源的限制，并通过 cpuset 将容器负载绑定到特定的 cpu 核上；



## 设置 CPU 核数限制

docker cli 命令行可以自己使用参数 `--cpus ` 来限制运行容器的 CPU 核数限制

`docker run  --cpus 1  -d --rm polinux/stress stress  --cpu 4  --verbose`{{execute T1}} ，等待运行以后，我们新建一个终端 T2 使用 `docker stats` 命令查看

`export CID=$(docker ps|grep stress|awk '{print $1}') `{{execute T1}}

`docker stats ${CID}`{{execute T1}}，`停止`{{execute interrupt T1}}

然后使用 `top`{{execute}} 命令查看， `停止`{{execute interrupt T1}}

> top 默认不展示全部 cpu 核数占用情况，可以使用数字 1 键展示



停止当前运行的测试 `stress`，停止{{execute interrupt T1}}，停止并删除运行的容器实例。

`export CID=$(docker ps|grep stress|awk '{print $1}') `{{execute T1}}

停止容器 `docker stop ${CID} `{{execute T1}}



## 绑定 CPU 核数运行

>  kata实验室有限制，建议本地验证

通过上述的测试，我们发现虽然 `stress` 进程限制了 1 个 CPU，但是使用的时候并不固定在某个 CPU 上，如果想要设置固定在某个 CPU 上可以使用以下命令：

`docker run  --cpus 1 --cpuset-cpus="0"  -d --rm polinux/stress stress  --cpu 4  --verbose`{{execute T1}} ，

然后使用 `top`{{execute}} 命令查看， `停止`{{execute interrupt T1}}

