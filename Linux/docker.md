## Usage
### Hello world
```
docker run ubuntu:15.10 /bin/echo "Hello world"
# if the image does not exist, download it from Docker Hub
```
交互式容器  
Args:
- -t: terminal
- -i: interact with STDIN
- -d: 后台运行

```
docker run -i -t ubuntu:15.10 /bin/bash
```
退出容器：`exit` or `CTRL+D`

- `docker ps` 查看运行中的容器
  - CONTAINER ID: 容器 ID。
  - IMAGE: 使用的镜像。
  - COMMAND: 启动容器时运行的命令。
  - CREATED: 容器的创建时间。
  - STATUS: 容器状态。
    - created（已创建）
    - restarting（重启中）
    - running 或 Up（运行中）
    - removing（迁移中）
    - paused（暂停）
    - exited（停止）
    - dead（死亡）
  - PORTS: 容器的端口信息和使用的连接类型（tcp\udp）。
  - NAMES: 自动分配的容器名称。
- `docker ps -a` 查看所有容器
- `docker start <container id>` 启动已停止的容器
- 停止容器 `docker stop <container id>`
- 查看容器log `docker logs <container id>`
- `docker restart <container id>` 重启停止的容器
- 进入容器 `docker attach <container id>`, 退出会导致容器停止
- 进入容器 `docker exec -it <container id> <command>` ，退出不会导致容器停止