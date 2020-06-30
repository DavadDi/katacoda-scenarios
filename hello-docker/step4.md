通过 docker 设置命令行的方式设置资源的限制

docker cli 命令行可以自己使用参数 `--cpus ` 来限制运行容器的 CPU 核数限制

`docker run  --cpus 1  -ti --rm polinux/stress stress  --cpu 4  --verbose`{{execute T1}} ，等待运行以后，我们在另外一个终端使用 `docker stats` 命令查看

`export CID=$(docker ps|grep stress|awk '{print $1}') `{{execute T1}}

`docker stats $(CID)`{{execute T2}}，`停止`{{execute interrupt T2}}。

然后使用 `top`{{execute}} 命令查看， `停止`{{execute interrupt T2}}。



通过上述的测试，我们发现虽然 `stress` 进程限制了 1 个 CPU，但是使用的时候并不固定在某个 CPU 上，如果想要设置固定在某个 CPU 上可以使用以下命令：

`docker run  --cpus 1 --cpuset-cpus="0"  -ti --rm polinux/stress stress2  --cpu 4  --verbose`{{execute T1}} ，

`export CID=$(docker ps|grep stress2|awk '{print $1}') `{{execute}}

`docker stats ${CID}`{{execute T2}}，`停止`{{execute interrupt T2}}。

然后使用 `top`{{execute T2}} 命令查看， `停止`{{execute interrupt T2}}。

