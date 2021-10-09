# 镜像
## 查找镜像
`docker search <image name>`
## 获取镜像
`docker pull <image name>`
## 镜像列表
`docker image ls`

列表包含了 `仓库名`、`标签`、`镜像 ID`、`创建时间` 以及 `所占用的空间`。

一个需要注意的问题是，`docker image ls` 列表中的镜像体积总和并非是所有镜像实际硬盘消耗。由于 Docker 镜像是多层存储结构，并且可以继承、复用，因此不同镜像可能会因为使用相同的基础镜像，从而拥有共同的层。由于 Docker 使用 Union FS，相同的层只需要保存一份即可，因此实际镜像硬盘占用空间很可能要比这个列表镜像大小的总和要小的多。

你可以通过 `docker system df` 命令来便捷的查看镜像、容器、数据卷所占用的空间。
# 容器
## 新建并启动
当利用 `docker run` 来创建容器时，Docker 在后台运行的标准操作包括：

-   检查本地是否存在指定的镜像，不存在就从 [registry](/docker_practice/repository) 下载
    
-   利用镜像创建并启动一个容器
    
-   分配一个文件系统，并在只读的镜像层外面挂载一层可读写层
    
-   从宿主主机配置的网桥接口中桥接一个虚拟接口到容器中去
    
-   从地址池配置一个 ip 地址给容器
    
-   执行用户指定的应用程序
    
-   执行完毕后容器被终止

后台执行：添加-d参数实现

## 启动已终止程序
`docker container start`
## 停止容器
`docker container stop`
## 重启容器
`docker container restart`
## 进入容器
`docker exec -it `
## 清理容器
`docker container rm `
清理所有处于终止状态的容器
`docker contailer prune`

# 镜像与容器的区别
镜像（`Image`）和容器（`Container`）的关系，就像是面向对象程序设计中的 `类` 和 `实例` 一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。

# 坑
注意要映射端口 不然无法启动
研究一下容器与镜像的区别