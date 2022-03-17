# 第 1 章：自动化构建

## 阅读参考资料

- [持续集成](https://baike.baidu.com/item/%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90/6250744)
- [webpack 官网](https://webpack.docschina.org/)
- [gogs 官网](https://gogs.io/)
- [drone 官网](https://www.drone.io/)

## 搭建 gogs + drone 持续集成环境

- 参考：[搭建 gogs + drone 持续集成环境](gogs-drone-ci.md)

## 手动构建电子书

要求：

- 在 gogs 上创建电子书仓库 ebook
- 克隆 ebook 仓库
- 在 ebook 目录下，添加四个 MarkDown 文档，分别是：
- `README.md, ch01.md, ch02.md 和 SUMMARY.md`
- 确定当前 node.js 版本为 v10，`nvm use 10`
- 全局安装 gitbook 工具，`npm i -g gitbook-cli && gitbook --version`
- 在 ebook 目录下构建电子书，`gitbook build`
- 检查 ebook 目录下生成的 `_book` 目录，`tree _book`
- 在 ebook 目录下运行 `browsersync` 启动静态文件服务
- 用浏览器访问该电子书
- 修改电子书的内容，重新构建电子书，检查浏览器中的电子书内容
- 停止 `browsersync` 的运行
- 在 ebook 目录下添加 `Dockerfile`，`Dockerfile` 的代码如下：

```
FROM nginx:alpine
COPY _book /usr/share/nginx/html/
EXPOSE 80
```

- 将电子书构建成 Docker 镜像，`docker build . -t ebook-img:latest --rm=true`
- 运行刚构建好的镜像，`docker run -d --name ebook -p 8080:80 ebook-img:latest`
- 用 Chrome 浏览器查看在线电子书

示例参考：

- [在线实验手册](http://manual.wangding.co/)
- [在线实验手册仓库](https://bitbucket.org/wngding/info-theory-lab-manual/)

## 自动构建电子书

要求：

- 登录 drone 网站，启动 `demo` 仓库的自动化构建
- 在 ebook 目录下，添加 `.drone.yml` 自动化构建脚本文件，代码如下：

```
kind: pipeline
name: default

steps:
- name: build gitbook
  image: node:10.23.3-alpine3.11
  commands:
  - npm config set registry https://registry.npm.taobao.org
  - npm i -g gitbook-cli
  - gitbook build

- name: build docker image
  image: docker:dind
  volumes:
  - name: dockersock
    path: /var/run/docker.sock
  commands:
  - ./clean.sh
  - docker build . -t ebook-img:latest --rm=true
  - docker run -d -p 8080:80 --name=ebook ebook-img:latest

volumes:
- name: dockersock
  host:
    path: /var/run/docker.sock
```

- 在 ebook 目录下，添加 `clean.sh` 脚本文件，并给 clean.sh 脚本**执行权限**
- `clean.sh` 脚本，执行环境清理任务，脚本代码如下：

```bash
#!/bin/sh

id=$(docker ps --filter "name=ebook" -q)

if [ ! -z "$id"  ]; then
  docker stop ebook
  docker rm ebook
  docker rmi ebook-img
fi
```

- 提交代码到 ebook 仓库，推送 ebook 仓库至 gogs
- 浏览 drone 网站，查看自动化构建的输出
- 用 Chrome 浏览器查看自动构建后的电子书

## 矩形计算器 v0.1

要求：

- 在 BitBucket 上创建 rectangle 项目仓库
- 根据输入的矩形的长度和宽度计算矩形的周长和面积
- 使用 H5 内置控件实现
- 解决[浮点舍入误差](https://segmentfault.com/a/1190000013431163)的问题
- 不用考虑数据合法性校验
- 支持科学计数法的数据计算
- 将代码推送到 BitBucket
- 将代码发布到七牛云的对象存储中

示例参考：

- [矩形计算器](http://rectangle.wangding.co)

## HTML 静态代码检查

要求：

- 在 BitBucket 上创建 build-automation 项目仓库
- 阅读 [htmlhint 规则文档](https://segmentfault.com/a/1190000013276858)
- 在 build-automation 仓库，创建 01-htmlhint 文件夹
- 在 01-htmlhint 文件夹中，复制 rectangle 仓库的 index.html、rectangle.css 和 rectangle.js 三个代码文件
- 添加 .htmlhintrc 配置文件，`wget https://sample.wangding.co/spa/htmlhintrc && mv htmlhintrc .htmlhintrc`
- npm 安装 htmlhint 插件
- 执行 `npm test`，实现 HTML 代码静态代码检查
- 执行自动化任务，观察自动化构建执行的效果
- 提交代码到 BitBucket

示例参考：

- [HTML 静态代码检查](https://bitbucket.org/wngding/build-automation/src/master/01-htmlhint/)

## CSS 静态代码检查

要求：

- 阅读 [csslint 规则文档](https://segmentfault.com/a/1190000019732938)
- 在 build-automation 仓库，创建 02-csslint 文件夹
- 在 02-csslint 文件夹中，复制 rectangle 仓库的 index.html、rectangle.css 和 rectangle.js 三个代码文件
- 添加 .csslintrc 配置文件，`wget https://sample.wangding.co/spa/csslintrc && mv csslintrc .csslintrc`
- npm 安装 csslint 插件
- 执行 `npm test`，实现 CSS 代码静态代码检查
- 执行自动化任务，观察自动化构建执行的效果
- 提交代码到 BitBucket

示例参考：

- [CSS 静态代码检查](https://bitbucket.org/wngding/build-automation/src/master/02-csslint/)

## JavaScript 静态代码检查

要求：

- 阅读 [eslint 规则文档](http://eslint.cn/docs/rules/)
- 在 build-automation 仓库，创建 03-eslint 文件夹
- 在 03-eslint 文件夹中，复制 rectangle 仓库的 index.html、rectangle.css 和 rectangle.js 三个代码文件
- 添加 .eslintrc.json 配置文件，`wget https://sample.wangding.co/spa/eslintrc.json && mv eslintrc.json .eslintrc.json`
- npm 安装 eslint 插件
- 执行 `npm test`，实现 JavaScript 代码静态代码检查
- 执行自动化任务，观察自动化构建执行的效果
- 提交代码到 BitBucket

示例参考：

- [JavaScript 静态代码检查](https://bitbucket.org/wngding/build-automation/src/master/03-eslint/)

## 矩形计算器 v0.2

要求：

- 完善 rectangle 项目
- 添加 drone.yml 构建脚本，当推送 rectangle 到 gogs 仓库时，执行以下自动化构建任务
- 对 HTML、CSS 和 JavaScript 静态代码检查
- 静态代码检查通过后，将 rectangle 构建成基于 Nginx 的镜像
- 运行该镜像，暴露到宿主机的 8080 端口
- 查看构建好的镜像
- 查看 rectangle 容器
- 查看 drone 构建服务器的构建日志
- Chrome 浏览器，访问 rectangle 应用

示例参考：

- [矩形计算器 v0.2 代码静态检查](https://bitbucket.org/wngding/rectangle/commits/0893549c0c5ed8abfe3d1077a71cd0325cb5495f)

## 阅读参考资料

- [单元测试准则](https://github.com/yangyubo/zh-unit-testing-guidelines/blob/master/readme.rst)
- [JavaScript 与 QA 工程师（理论篇）](https://github.com/hubvue/nota/issues/26)
- [Jest 官网](https://jestjs.io/)
- [Jest 中文](https://jestjs.io/zh-Hans/)

## 单元测试

要求：

- 在 build-automation 仓库，创建 04-unit-test 文件夹
- 创建被测模块 add.js，被测模块暴露出 add 方法，实现 z = x + y
- 对 add.js 模块，编写单元测试脚本
- 运行 npm test，执行单元测试
- 查看单元测试输出结果
- 进行代码覆盖率测试
- 查看代码覆盖率报告
- 把单元测试脚本改成动态测试

示例参考：

- [单元测试](https://bitbucket.org/wngding/build-automation/src/master/04-unit-test/)

## entropy 的单元测试

要求：

- 在 build-automation 仓库，创建 05-entropy 文件夹
- 获取 [entropy.js](https://bitbucket.org/wngding/nodejs-demo/src/master/24-project/entropy.js) 被测程序
- entropy 程序的功能描述，请参考 [Node.js 大作业](http://nodejs.wangding.co/ch14-project.html)
- 重构 entropy.js 代码，使其易于实施单元测试
- 添加单元测试代码
- 运行单元测试，查看单元测试输出结果
- 查看代码覆盖率报告 

示例参考：

- [entropy 的单元测试](https://bitbucket.org/wngding/entropy)

## 接口测试

要求：

- 在 build-automation 仓库，创建 06-api-test 文件夹
- 添加 app.js 脚本代码，实现矩形计算器的 HTTP API 接口
- 接口规格如下：

```
// request
GET /rectangle?width=20&height=20

// response
{'code': 200, 'reason': '查询成功', result: {'area': 400, 'perimeter': 80}}
```

- 手工测试该接口
- 添加接口自动化测本代码
- 运行 npm test，观察接口测试的效果
- 对接口实现自动化测试

示例参考：

- [HTTP 接口测试](https://bitbucket.org/wngding/build-automation/src/master/06-api-test/)

## 消除依赖

要求：

- 在 build-automation 仓库，创建 07-mock 文件夹
- 获取 `password-rules.js`，`wget https://sample.wangding.co/spa/password-rules.js`
- 获取 `password-verify.js`，`wget https://sample.wangding.co/spa/password-verify.js`
- 在 `password-rules.js` 中添加一个密码长度不少于 6 位的验证规则
- 为 `password-rules.js` 添加单元测试代码
- 为 `password-verifier.js` 添加单元测试代码，消除 `password-rules.js` 的依赖
- 运行单元测试，查看单元测试输出结果

示例参考：

- [消除依赖](https://bitbucket.org/wngding/build-automation/src/master/07-mock/)

## 矩形计算器 v0.3

要求：

- 切换到 rectangle 项目仓库
- 重构 rectangle.js 代码，使其易于实施单元测试
- 编写自动化测试脚本
- 运行 npm test，先做静态代码检查，再做单元测试
- 将代码仓库推送 gogs，用 drone 实现自动化构建
- 浏览器访问，构建好的 rectangle 容器
- 检查 drone 构建日志

示例参考：

- [矩形计算器 v0.3 单元测试](https://bitbucket.org/wngding/rectangle/commits/b3f8f6fcad428ced1c9e2f8d594e488604999248)

## 矩形计算器 v0.4

要求：

- 切换到 rectangle 项目仓库
- 编写 webpack.config.js，对 HTML、CSS 和 JavaScript 代码进行压缩
- 将代码压缩构建任务编写到 .drone.yml 配置脚本中
- 推送修改的代码到 gogs 仓库
- 观察 drone 服务器上的自动化构建日志
- 用 chrome 浏览器查看自动化构建并发布的 rectangle 应用
- 验证应用代码是压缩后的代码

示例参考：

- [矩形计算器 v0.4 实现代码压缩发布](https://bitbucket.org/wngding/rectangle/commits/d24ad8c939ede86cc1455f80512bef4dfda09077)

## 矩形计算器 v0.5

要求：

- 添加页面初始焦点，初始焦点设置为第一个文本框
- 设备自适应，页面在手机上可以正常显示
- 增加必填字段的提示
- 不用考虑数据合法性校验
 
示例参考：
   
- [矩形计算器 v0.5 增强用户体验](https://bitbucket.org/wngding/rectangle/commits/1c926636b4010af747c6c1265e5d48bf7e7b09af)
