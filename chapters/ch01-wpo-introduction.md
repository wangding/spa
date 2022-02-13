# 第 1 章：性能优化概述

**注意**：  
- 如无特别说明，后续操作的对象都是 `wpo-demo` 仓库
- 下载代码仓库，`git clone https://bitbucket.org/wngding/wpo-demo.git`
- 安装项目依赖，`cd wpo-demo && npm install`

## 阅读参考资料

- [压缩 CSS](https://wpocs.cn/docs/lighthouse-performance/unminified-css.html)
- [压缩 JavaScript](https://wpocs.cn/docs/lighthouse-performance/unminified-javascript.html)
- [启用文本压缩](https://wpocs.cn/docs/lighthouse-performance/uses-text-compression.html)
- [使用 imagemin 压缩图像](https://wpocs.cn/docs/fast-load-time/use-imagemin-to-compress-images.html)

## 用 Network 评估网站性能

操作步骤如下：
- 启动 `wd01` 网站，`npx http-server wd01`
- 用 chrome 浏览器访问 `http://<ip-addr>:8080/`
- 在 Network 面板，设置 `Disable cache` 以及 `Fast 3G` 节流
- 在 Network 面板，设置 `Start recording network log`
- `F5` 刷新网站页面，观察瀑布流图，能够描述出资源加载的顺序
- 根据 Network 面板下的统计信息，对网站的性能有所了解
- 对 Network 面板截图保存
- 关闭 `wd01`，`CTRL + C`
- 启动 `wd01-optimized` 网站，`npx http-server wd01-optimized`
- `F5` 刷新网站页面
- 用 Network 面板观察性能优化前后网站加载速度的差异
- 查看 `wd01-optimized` 目录下的静态资源文件与 `wd01` 目录下的区别

## 压缩代码

操作步骤如下：
- 复制 `wd01` 为 `minify` 目录，`cp -r wd01 minify`
- 进入 `minify` 目录，`cd minify`
- 利用 `minifier` 压缩 CSS 代码，`cd css && npx minifier -o styles.min.css styles.css`
- 查看压缩前后 CSS 文件大小的差异，`ls -lh`
- 同样道理，利用 `minifier` 压缩 JS 代码
- 利用 `html-minify` 压缩 HTML 代码
- 修改 `index.html` 使用压缩后的 CSS 和 JS 代码
- 启动 `minify` 网站，`npx http-server minify`
- 用 Network 面板观察性能优化前后网站加载速度的差异

## 压缩图片

操作步骤如下：
- 用 [tinyPNG](https://tinypng.com/) 对 `minify/img` 目录下的图片文件进行压缩优化
- 观察图片压缩前后文件尺寸的差距
- 下载压缩优化后的图片，替换 `img` 目录下的原始图片
- 启动 HTTP 静态文件服务，`npx http-server minify`
- 用 Network 面板观察性能优化前后网站加载速度的差异

## HTTP 传输的 GZip 压缩

操作步骤如下：
- 压缩 `minify` 目录下的 `index.html`，`gzip index.html`
- 查看压缩后的结果，`ls`
- 启动 HTTP 静态文件服务，`npx http-server minify -g`
- `-g` 参数启用 gzip 压缩
- 用 Network 面板观察性能优化前后网站加载速度的差异
- 在 Network 面板下，勾选 `Use Large request rows` 选项
- `F5` 刷新网站页面，观察 `index.html` 页面传输的字节数与实际字节 数的差异
- 为什么 `index.html` 传输的字节数小于实际字节数？
- 查看 `index.html` 页面的 HTTP 请求头和响应头，能否找到 gzip 压缩编码的头字段？
- 观察 CSS 和 JS 资源传输的字节数和实际字节数
- 为什么传输的字节数大于实际字节数？
- 查看这些资源的 HTTP 请求头和响应头，能否找到 gzip 压缩编码的头字段？

## nginx 启用 GZip 压缩

操作步骤如下：
- 还原 `index.html.gz` 压缩文件，`gzip -d index.html.gz`
- 启动 nginx 容器
```bash
docker run -d \
           --name web \
           -p 8080:80 \
           -v <minified-absolute-dir>:/usr/share/nginx/html/ \
           nginx:alpine
```
- 通过 chrome 浏览器查看网站，`http://<ipaddr>:8080`
- 在 Network 面板下，观察资源的 HTTP 传输字节数和实际字节数
- HTTP 数据传输中是否发生 GZip 压缩？
- 以 bash 交互的方式，进入 nginx 容器，`docker exec -it web /bin/sh`
- 查看网站内容，`cd /usr/share/nginx/html && ls`
- 修改 nginx 配置文件，启用 GZip 压缩，`cd /etc/nginx && vi nginx.conf`
- 重启 nginx 服务，`nginx -s reload`
- `F5` 刷新网站页面，观察 `index.html` 页面传输的字节数与实际字节 数的差异，发现只有 `index.html` 文件做了压缩
- 继续修改 `nginx.conf`，添加如下配置：
```
gzip_min_length 1024;
gzip_types application/javascript text/css text/xml;
```
- 了解 GZip 更多的配置参数，请阅读：[ngx_http_gzip_module](https://nginx.org/en/docs/http/ngx_http_gzip_module.html)
- 重启 nginx 服务，`nginx -s reload`
- `F5` 刷新网站页面，观察是否所以静态资源得到了压缩
