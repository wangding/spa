# 第 8 章：其他

## 阅读参考资料

- [内容分发网络](https://wpocs.cn/docs/fast-load-time/content-delivery-networks.html)
- [CDN 是什么？](https://www.bilibili.com/video/BV15K4y1E77r)
- [HTTP2 是什么？](https://www.bilibili.com/video/BV1Sw411d7oE)
- [HTTP cache](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Caching)
- [Web 缓存系列](http://www.alloyteam.com/2012/03/web-cache-1-web-cache-overview/)

## HTTP/2.0

操作步骤如下：
- 对以下三个网站，用 Chrome 浏览器 devtools 的 Network 面板做性能测评
  - HTTP/1.0 网站：https://h0.adamliu.net/
  - HTTP/1.1 网站：https://h1.adamliu.net/
  - HTTP/2.0 网站：https://h2.adamliu.net/
- 在 Network 面板验证三个网站的 HTTP 协议的版本
- 对比三个网站：总请求数量，请求的资源大小，传输数据的大小，消耗的时长
- 查看 h0 网站的 ConnectionID，ConnectionID 是否各不相同？说明什么问题？
- 查看 h1 网站的 ConnectionID，ConnectionID 是否各不相同？说明什么问题？
- 查看 h2 网站的 ConnectionID，ConnectionID 是否各不相同？说明什么问题？

## Nginx 实现 HTTP/2.0

操作步骤如下：
- 在 `wpo-demo` 目录下创建 Key 文件夹，`mkdir key && cd key`
- 在 `key` 文件夹下生成自签名证书，`openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout selfsigned.key -out selfsigned.crt`
- **注意**，生成证书的过程，需要提供一些证书的信息，**每个字段尽量不要为空**
- 启动 Nginx 容器

```bash
docker stop `docker ps -aq`
docker rm `docker ps -aq`
docker run -d \
         --name web \
         -p 8080:80 \
         -p 8888:443 \
         -v <wd17-dir>:/usr/share/nginx/html \
         -v <key-dir>:/key \
         nginx:alpine
docker ps -a
```

- 浏览器访问：`http://<ip-addr>:8080`，出现 B 站图标，Network 面板有 530 个请求，说明网站挂载正常
- 交互模式连接 nginx 容器，`docker exec -it web /bin/sh`
- 检查 key 目录下的证书，`ls /key`，如果有两个证书文件，说明证书目录挂载正常
- 修改 Nginx 配置文件，`vi /etc/nginx/conf.d/default.conf`
- 添加 SSL 证书配置和 HTTP2 的配置

```bash
listen       443 ssl http2;
server_name  localhost;

ssl_certificate      /key/selfsigned.crt;
ssl_certificate_key  /key/selfsigned.key;
```

- 保存配置文件，重新加载 Nginx 配置文件，`nginx -s reload`
- 浏览器访问：`https://<ip-addr>:8888`
- Network 面板检查 HTTP 协议版本，以及连接的数量

## 用 Koa 框架实现 HTTP/2.0

操作步骤如下：
- 确认 koa2 可用，`koa2 --help`
- 如果命令找不到，安装 `koa-generator`，`npm i -g koa-generator`
- 否则，跳过上面的安装步骤
- 创建 `wd18` koa 脚手架项目，`koa2 -e wd18 && cd wd18`
- 安装项目依赖，`npm i`
- 运行 `wd18`，`npm start`
- 浏览器访问 `wd18`，通过 Network 面板，确认 HTTP 协议版本
- 创建证书文件夹，`mkdir key && cd key`
- 创建自签名证书，注意，给证书提供一些有用信息

```bash
openssl genrsa 1024 > key.pem
openssl req -x509 -new -key key.pem > key-cert.pem
```

- 修改 `wd18` 项目代码，`vi bin/www`

```javascript
// 原代码
var http = require('http');
// 改为
const http = require('http2');
const fs = require('fs');

// 原代码
var server = http.createServer(app.callback());

// 改为
const server = http.createSecureServer({
  key: fs.readFileSync('./key/key.pem'),
  cert: fs.readFileSync('./key/key-cert.pem')
}, app.callback());
```

- 保存代码，运行网站，`npm start`
- 浏览器访问 `wd18`，通过 Network 面板，确认 HTTP 协议版本
- 把 `wd17` 目录内容复制到 `wd18`，`cp -r wd17/* wd18/public/
- 浏览器访问 `wd18`

## HTTP 缓存

操作步骤如下：
- 完善 `wd19` 项目，首先实现强制缓存
- 通过 Network 面板，检查缓存的效果
- 实现协商缓存，用 Network 面板，检查缓存效果
