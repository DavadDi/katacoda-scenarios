Hello OverlayFS!

OverlayFS 是联合文件系统的一种实现。OverlayFS 在linux主机上只有两层，一个目录在下层，用来保存镜像(docker)，另外一个目录在上层，用来存储容器信息。在 OverlayFS 中，底层的目录叫做 lowerdir，顶层的目录称之为 upperdir，对外提供统一的文件系统为 merged。 当需要修改一个文件时，使用 CoW 将文件从只读的Lower 复制到可写的 Upper 进行修改，结果也保存在 Upper 层。在Docker中，底下的只读层就是 image，可写层就是 Container。



![img](https://www.do1618.com/wp-content/uploads/2020/06/overlayfs.jpeg)



我们可以手工体验一下整体的工作流程：

* 新建目录和初始化

  * `mkdir low upper work`{{execute}}
  * `ls -hl`{{execute}}
  * `echo 'lower' > low/lower.txt`{{execute}}
  * `echo 'upper' > upper/upper.txt`{{execute}}

* 创建 merged 目录

  * `mkdir merged`{{execute}}
  * `mount -t overlay overlay -olowerdir=./low,upperdir=./upper,workdir=./work ./merged`{{execute}}
  * `tree`{{execute}}

* 修改 lower.txt 文件内容

  * `cd merged`{{execute}}
  * `echo Hello >> lower.txt`{{execute}}
  * `tree`{{execute}}
  * `cat ../low/lower.txt`{{execute}}

* 删除文件 lower.txt 

  * `delete lower.txt`{{execute}}
  * `tree`{{execute}}
  * `cat ../low/lower.txt`{{execute}}

  

