# gogs-drone-ci

搭建 gogs + drone 持续集成系统

## start gogs

```bash
docker run -d \
  -e TZ="Asia/Shanghai" \
  -v /data  \
  --net host \
  --restart=always \
  --name=gogs \
  gogs/gogs:0.11.29
```

- gogs use v0.11.29, latest version webhook not work
- 默认端口为 3000，**使用宿主的 IP 地址**访问 gogs 服务
- 配置 gogs，使用 sqllite 数据库
- 注册创建账户 wangding，第一个账户默认为管理员账户
- 创建空的测试仓库 demo
- 克隆 demo 仓库，`git clone http://192.168.174.133:3000/wangding/demo.git`
- `cd demo && echo 'hello' > a.txt`
- `git add .`
- `git commit -m "add a.txt"`
- `git push`
- 检查 gogs 上的 demo 仓库，有最新的提交

## start drone

```bash
docker run -d \
  -v /data \
  -e DRONE_AGENTS_ENABLED=true \
  -e DRONE_GOGS_SERVER=http://192.168.174.133:3000 \
  -e DRONE_RPC_SECRET=mydrone666 \
  -e DRONE_SERVER_HOST=192.168.174.133:8888 \
  -e DRONE_SERVER_PROTO=http \
  -e DRONE_USER_CREATE=username:wangding,admin:true \
  -e TZ="Asia/Shanghai" \
  -p 8888:80 \
  --restart=always \
  --name=drone \
  drone/drone:1
```

- 注意 DRONE_GOGS_SERVER 和 DRONE_SERVER_HOST 两个参数的 IP 地址，**使用宿主的 IP 地址**
- 端口号是 8888
- 访问 drone 服务，http://192.168.174.133:8888
- 用 gogs 的 wangding 账户登录
- 可以看到 demo 仓库，激活 demo 仓库的自动化构建，**勾选 project setting: trusted**，允许 runner 构建 docker 镜像
- 检查 gogs demo 仓库的 webhook 配置，drone 自动添加了 webhook 配置

## start drone-runner

```bash
docker run -d \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -e DRONE_RPC_PROTO=http \
  -e DRONE_RPC_HOST=192.168.174.133:8888 \
  -e DRONE_RPC_SECRET=mydrone666 \
  -e DRONE_RUNNER_CAPACITY=2 \
  -e DRONE_RUNNER_NAME=runner-docker \
  -e TZ="Asia/Shanghai" \
  -p 9999:3000 \
  --restart=always \
  --name=runner-docker \
  drone/drone-runner-docker:1
```

- 注意 DRONE_RPC_HOST 参数的 IP 地址，**使用宿主的 IP 地址**

