# Docker

## 镜像

`docker images`:查看本地已拉取的镜像列表。

`docker load -i myimage.tar`:从压缩文件加载 Docker 镜像到本地 Docker 镜像仓库。

## 容器

```shell
docker run -d --shm-size=32g --runtime=nvidia --privileged --name my_container -v local/:/workspace image:tag sleep infinity
```

- `-e` : 向容器传递环境变量
  - `UID=$(id -u)` : 获取当前用户的 UID , 传递给 Docker 容器
  - `GID=$(id -g)` : 获取当前用户的 GID , 传递给 Docker 容器
- `-d` : 启动容器并让它在后台运行
- `--shm-size` : 设置共享内存的大小。
- `--runtime` : 用于 GPU 支持
- `--privileged` : 给予容器更多的特权，通常用于需要访问主机硬件的应用。
- `--name` : 为容器指定一个名称。
- `-v` : 挂载主机的卷（目录）到容器内
- `sleep infinity` : 让容器进入永久睡眠状态，直到手动停止
- `-it` : 使容器保持交互模式（-i 表示交互，-t 为分配伪终端）。通常用于进入容器终端。

```shell
docker run -it --rm -v ${PWD}:/workspace image bash
```

```shell
docker run -d --gpus all --shm-size=32g --privileged --name test -v /home/ai/code:/code /bin/bash
```
