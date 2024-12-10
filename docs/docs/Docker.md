# 运行启动相关
## 启动用镜像启动一个容器
```bash
docker [OPTIONS] run IMAGE
```

  `-e`：在启动是可以加上这个命令，用于给运行的容器添加环境变量。例如,`http_proxy=127.0.0.1:7890`

  `-p`：指定端口映射，将主机的端口映射到容器的端口。例如，`8080:8080`

  `-v`：挂载主机路径到容器内部路径。例如，`/path/on/host:/path/in/container`



## docker查看容器
ps

```bash
docker ps
```



> `-a`：可以显示包括已经停止的容器  
`-q`：仅显示容器ID
>

container命令组

```bash
docker container ls 或 docker container list：列出运行中的容器。
docker container start [CONTAINER_ID]：启动一个停止状态下的容器。
docker container stop [CONTAINER_ID]：停止一个正在运行的容器。
docker container rm [CONTAINER_ID]：删除一个已经停止的容器。
```



## 运行已经停止的容器
```bash
docker start [container]
```



## 进入容器终端，退出容器终端
```bash
docker exec -it [container] bash
```

```plain
exit
```



## docker拉取一个镜像
```bash
docker pull openjdk:8u111
```



## Docker停止所有容器命令
```bash
docker stop $(docker ps -q)
```



# Docker示例
## Docker安装MySQL
```bash
docker run --name mysql \
    -e MYSQL_ROOT_PASSWORD=123456 \
    -v /path/to/local/data:/var/lib/mysql \
    -p 3306:3306 \
    -d mysql:8.0
```



# Docker基本
## apt安装
```bash
sudo apt install docker.io
```



## 普通用户无法操作docker解决
执行以下命令，并重启系统

```bash
sudo usermod -aG docker $USER
```



## dockerhub配置镜像源
打开，若没有docker文件夹则新建

```bash
nano /etc/docker/daemon.json
```

加入以下文字

> 实际上，下面的docker镜像经常不能用，需要网上搜索的最新的docker镜像
>

```bash
{
    "registry-mirrors": [
        "https://docker.rainbond.cc" 
    ]
}
```



重启docker服务

```bash
sudo systemctl restart docker
```



# Docker配置代理
```bash
{
    "proxies": {
      "default": {
        "httpProxy": "http://127.0.0.1:7890",
        "httpsProxy": "http://127.0.0.1:7890",
        "noProxy": "localhost,127.0.0.1"
      }
    }
  }

```



# Dockerfile构建镜像
创建Dockerfile文件

```bash
nano ./Dockerfile
```



在Dockerfile目录下执行命令

```bash
docker build -t [ImageName]:latest .
```

