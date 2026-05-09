# Docker

## Install

```bash
sudo apt update && sudo apt upgrade -y

curl -fsSL https://get.docker.com | sudo sh
```

## Commands

| 命令                               | 作用说明               |
| -------------------------------- | ------------------ |
| docker version                   | 查看 Docker 版本信息     |
| docker info                      | 查看 Docker 系统信息     |
| docker images                    | 查看本地镜像列表           |
| docker ps                        | 查看正在运行的容器          |
| docker ps -a                     | 查看所有容器             |
| docker pull nginx                | 拉取镜像               |
| docker build -t myapp .          | 根据 Dockerfile 构建镜像 |
| docker run nginx                 | 运行容器               |
| docker run -d nginx              | 后台运行容器             |
| docker run -p 80:80 nginx        | 端口映射运行容器           |
| docker run --name web nginx      | 指定容器名称             |
| docker run -v ./data:/data nginx | 挂载数据卷              |
| docker exec -it 容器名 bash         | 进入容器终端             |
| docker logs 容器名                  | 查看容器日志             |
| docker logs -f 容器名               | 实时查看日志             |
| docker stop 容器名                  | 停止容器               |
| docker start 容器名                 | 启动已停止容器            |
| docker restart 容器名               | 重启容器               |
| docker rm 容器名                    | 删除容器               |
| docker rmi 镜像名                   | 删除镜像               |
| docker inspect 容器名               | 查看容器详细信息           |
| docker stats                     | 查看容器资源使用情况         |
| docker cp 文件 容器名:/路径             | 复制文件到容器            |
| docker network ls                | 查看网络列表             |
| docker volume ls                 | 查看数据卷列表            |
| docker compose up                | 启动 compose 服务      |
| docker compose up -d             | 后台启动 compose 服务    |
| docker compose down              | 停止并删除 compose 服务   |
| docker compose restart           | 重启 compose 服务      |
| docker compose logs              | 查看 compose 日志      |
| docker compose ps                | 查看 compose 容器状态    |
| docker system df                 | 查看 Docker 磁盘占用     |
| docker system prune              | 清理无用资源             |
| docker container prune           | 清理停止的容器            |
| docker image prune               | 清理无用镜像             |
| docker volume prune              | 清理无用数据卷            |
| docker network prune             | 清理无用网络             |