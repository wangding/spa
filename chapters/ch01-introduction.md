# 课程说明

## 阅读参考资料

- [docker 官网](https://www.docker.com/)
- [docker 笔记](http://note.wangding.co/linux/docker.html)
- [docker 教程](http://c.biancheng.net/docker/)
- [写给前端的 Docker 实战教程](http://pea3nut.blog/e1200)
- [浏览器的工作原理：新式网络浏览器幕后揭秘](https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/)
- [现代浏览器内部揭秘：第一部分](https://wpocs.cn/docs/juejin-wpo/inside-look-at-modern-web-browser-part1.html)
- [现代浏览器内部揭秘：第二部分](https://wpocs.cn/docs/juejin-wpo/inside-browser-part2.html)
- [现代浏览器内部揭秘：第三部分](https://wpocs.cn/docs/juejin-wpo/inside-browser-part3.html)
- [现代浏览器内部揭秘：第四部分](https://wpocs.cn/docs/juejin-wpo/inside-browser-part4.html)

## 安装 Docker

操作步骤如下：

```bash
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum install docker-ce docker-ce-cli containerd.io
sudo yum list docker-ce --showduplicates | sort -r
sudo systemctl start docker
sudo systemctl status docker
sudo systemctl enable docker
docker version
```

## 配置 Docker

操作步骤如下：

```bash
# 以非 root 用户身份使用 docker
sudo usermod -aG docker $USER   # $USER 是当前登录的用户
                                # 此命令执行后，需注销，重新登录，才生效

# 使用阿里 docker 镜像，提高镜像拉取速度
mkdir -p /etc/docker
tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://v0yaxj7c.mirror.aliyuncs.com"]
}
EOF
systemctl daemon-reload
systemctl restart docker
```

## 运行 nginx 容器

操作步骤如下：

```bash
docker run -d \
           --name web \
           -p 8080:80 \
           nginx:alpine
docker ps -a
```
- 用 chrome 浏览器访问 `http://<ip-addr>:8080`
- 应该能看到 nginx 的欢迎页面


