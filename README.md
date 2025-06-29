# Docker 命令手册

> 🐳 常用 Docker 命令速查表 | 最后更新: {2025-6-29}



---

## 目录
- [容器生命周期管理](#容器生命周期管理)
- [镜像管理](#镜像管理)
- [容器监控与调试](#容器监控与调试)
- [存储与网络](#存储与网络)
- [Docker Compose](#docker-compose)
- [系统清理](#系统清理)
- [常用组合示例](#常用组合示例)

---

## 容器生命周期管理

### 创建/运行容器
```bash
docker run [OPTIONS] IMAGE [COMMAND]
```
| 选项 | 说明 |
|------|------|
| `-d` | 后台运行（守护模式） |
| `-p 宿主机端口:容器端口` | 端口映射 |
| `-v 宿主机路径:容器路径` | 目录挂载 |
| `--name 名称` | 指定容器名称 |
| `-e 变量名=值` | 设置环境变量 |
| `-it` | 交互式终端（通常配合 `/bin/bash` 使用） |
| `--rm` | 容器退出后自动删除 |
| `--restart always` | 自动重启策略（可选：no/on-failure/unless-stopped） |
| `--network 网络名` | 指定容器网络 |

### 基本操作
```bash
docker start 容器ID或名称        # 启动容器
docker stop 容器ID或名称         # 停止容器（优雅退出）
docker restart 容器ID或名称      # 重启容器
docker pause/unpause 容器ID     # 暂停/恢复容器
docker rm 容器ID或名称          # 删除已停止的容器
docker rm -f 容器ID或名称       # 强制删除运行中的容器
```

---

## 镜像管理
```bash
docker pull 镜像名:标签          # 拉取镜像（默认最新版）
docker push 镜像名:标签         # 推送镜像到仓库
docker images                  # 列出本地镜像
docker rmi 镜像ID或名称        # 删除镜像
docker build -t 镜像名:标签 .   # 构建镜像（需 Dockerfile）
docker history 镜像名          # 查看镜像构建历史
```

---

## 容器监控与调试
### 日志与信息
```bash
docker logs 容器ID或名称       # 查看日志
docker logs -f 容器ID         # 实时日志跟踪
docker inspect 容器ID         # 查看容器详细信息（JSON）
docker stats                  # 实时资源监控（CPU/内存）
docker top 容器ID             # 查看容器内进程
```

### 进入容器
```bash
docker exec -it 容器ID /bin/bash   # 进入运行中的容器（推荐）
docker attach 容器ID              # 附加到容器（退出会导致容器停止）
```

---

## 存储与网络
### 数据卷（Volume）
```bash
docker volume create 卷名       # 创建命名卷
docker volume ls               # 列出所有卷
docker volume inspect 卷名     # 查看卷详情
```

### 网络管理
```bash
docker network ls              # 列出所有网络
docker network create 网络名   # 创建自定义网络
docker network inspect 网络名  # 查看网络详情
```

---

## Docker Compose
```bash
docker compose up -d           # 启动服务栈（后台运行）
docker compose down            # 停止并删除服务栈
docker compose logs -f         # 查看服务日志
docker compose ps              # 查看服务状态
```

---

## 系统清理
```bash
docker system df              # 查看磁盘占用
docker container prune        # 清理所有停止的容器
docker image prune -a         # 清理未使用的镜像
docker system prune           # 清理所有未使用的资源
```

---

## 常用组合示例
### 运行 Nginx 容器
```bash
docker run -d --name my_nginx \
  -p 80:80 \
  -v ./html:/usr/share/nginx/html \
  nginx:alpine
```

### 运行 MySQL 容器
```bash
docker run -d --name mysql_db \
  -p 3306:3306 \
  -e MYSQL_ROOT_PASSWORD=123456 \
  -v mysql_data:/var/lib/mysql \
  mysql:8.0 --character-set-server=utf8mb4
```

### 批量操作
```bash
# 停止所有运行中的容器
docker stop $(docker ps -q)

# 删除所有镜像（慎用！）
docker rmi $(docker images -q)
```

---

## 学习资源
- [官方文档](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Play with Docker](https://labs.play-with-docker.com/)

```


建议将 `{更新日期}` 替换为实际日期，并定期维护更新命令列表。
