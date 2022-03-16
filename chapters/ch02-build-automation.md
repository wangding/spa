# 第 2 章：自动化构建

## 阅读参考资料

- [持续集成](https://baike.baidu.com/item/%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90/6250744)
- [webpack 官网](https://webpack.docschina.org/)
- [GTmetrix](https://gtmetrix.com/)
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

基本要求：
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
- 添加 .htmlhintrc 配置文件
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
- 添加 .csslintrc 配置文件
- npm 安装 csslint 插件
- 执行 `npm test`，实现 CSS 代码静态代码检查
- 执行自动化任务，观察自动化构建执行的效果
- 提交代码到 BitBucket

示例参考：
- [CSS 静态代码检查](https://bitbucket.org/wngding/build-automation/src/master/02-csslint/)

## JavaScript 静态代码检查

要求：
- 阅读 [eslint 规则文档](http://eslint.cn/docs/rules/)
- 在 build-automation 仓库，创建 eslint 文件夹
- 在 eslint 文件夹中，复制 rectangle 仓库的 index.html、rectangle.css 和 rectangle.js 三个代码文件
- 添加 .eslintrc.json 配置文件
- npm 安装 eslint 插件
- 执行 `npm test`，实现 JavaScript 代码静态代码检查
- 执行自动化任务，观察自动化构建执行的效果
- 提交代码到 BitBucket

示例参考：
- [JavaScript 静态代码检查](https://bitbucket.org/wngding/build-automation/src/master/03-eslint/)

## 矩形计算器 v0.2

要求：
- 完善 rectangle 项目
- 添加 drone.yml 构建脚本
- 推送 rectangle 到 gogs 仓库，后自动执行自动化构建
- 首先，对 HTML、CSS 和 JavaScript 代码实现静态代码检查
- 静态代码检查通过后，将 rectangle 构建成基于 Nginx 的镜像
- 运行该镜像，暴露到宿主机的 8080 端口
- 查看构建好的镜像
- 查看运行 rectangle 的容器
- 查看 drone 构建服务器的构建日志
- 用 chrome 浏览器，查看自动化构建并发布运行的 rectangle 应用

示例参考：
- [矩形计算器 v0.2 代码静态检查]()

## 阅读单元测试参考资料

- 单元测试准则：https://github.com/yangyubo/zh-unit-testing-guidelines/blob/master/readme.rst
- 编写可测试的 JavaScript 代码：http://blog.jobbole.com/67560/
- JavaScript 与 QA 工程师（理论篇）：https://github.com/hubvue/nota/issues/26
- 自动化、跨浏览器的 JavaScript 单元测试：https://www.zcfy.cc/article/learning-how-to-set-up-automated-cross-browser-javascript-unit-testing-mdash-philip-walton
- Mocha 官网：https://mochajs.org/
- Mocha 中文文档：https://segmentfault.com/a/1190000011362879
- Chai 官网：https://www.chaijs.com/
- Istanbul 官网：https://istanbul.js.org/
- Istanbul 教程：http://www.ruanyifeng.com/blog/2015/06/istanbul.html
- Sinon 官网：https://sinonjs.org/
- Sinon 指南：https://www.zcfy.cc/article/sinon-tutorial-javascript-testing-with-mocks-spies-stubs-422.html

## 服务端代码单元测试

要求：
- 阅读 [grunt-mocha-cli 插件文档](https://www.npmjs.com/package/grunt-mocha-cli)
- 阅读 [grunt-mocha-istanbul 插件文档](https://www.npmjs.com/package/grunt-mocha-istanbul)
- 在 grunt-demo 仓库，创建 mocha-be 分支
- 创建被测模块 add.js，被测模块暴露出 add 方法，实现 z = x + y
- 对 add.js 模块，编写 mocha 单元测试脚本
- 执行 mocha 命令，运行单元测试，查看单元测试输出结果
- 进行代码覆盖率测试
- 查看代码覆盖率报告
- 添加 grunt 插件支持，实现 grunt mocha 单元测试
- 添加 grunt 插件支持，实现 grunt 代码覆盖率测试

示例参考：
- [服务端单元测试](https://gitee.com/wangding/grunt-demo/tree/mocha-be/)

## entropy 的单元测试

要求：
- 在 grunt-demo 仓库，创建 entropy 分支
- 获取 [entropy.js](https://gitee.com/wangding/nodejs-demo/blob/master/24-project/entropy.js) 被测程序
- entropy 程序的功能描述，请参考 [Node.js 大作业](http://nodejs.wangding.co/ch14-project.html)
- 重构 entropy.js 代码，使其易于实施单元测试
- 添加 mocha 单元测试代码
- 运行 grunt mocha 单元测试，查看单元测试输出结果
- 查看代码覆盖率报告 

示例参考：
- [entropy 的单元测试](https://gitee.com/wangding/grunt-demo/tree/entropy/)

## 前端代码单元测试

要求：
- 阅读 [grunt-mocha 插件文档](https://www.npmjs.com/package/grunt-mocha)
- 在 grunt-demo 仓库，创建 mocha-fe 分支
- 将 rectangle 仓库中的 index.html、rectangle.js 和 rectangle.css 三个代码文件复制到当前项目仓库的 mocha-fe 分支下
- 重构 rectangle.js 代码，使其易于实施单元测试
- 添加 mocha 单元测试代码
- 运行 grunt mocha 单元测试，查看单元测试输出结果

示例参考：
- [前端代码单元测试](https://gitee.com/wangding/grunt-demo/tree/mocha-fe/)

## HTTP 接口测试

要求：
- 阅读 [grunt-run 插件文档](https://www.npmjs.com/package/grunt-run)
- 在 grunt-demo 仓库，添加 http-api-test 分支
- 添加 app.js 脚本代码，实现矩形计算器的 HTTP API 接口
- 接口 URL：`http://localhost:8080/rectangle?width=20&height=20`
- 接口返回信息格式：`{'code': 200, 'reason': '查询成功', result: {'area': 400, 'perimeter': 80}}`
- npm 安装 grunt、chai、grunt-mocha-cli 和 grunt-run 插件
- 创建 test 文件夹
- 在 test 文件夹，添加接口测试自动化测本代码
- 测试矩形计算器接口
- 添加 Gruntfile.js，实现接口 Web 服务的启动和关闭
- 实现对矩形计算器 HTTP API 接口的自动化测试
- 运行 grunt 命令，观察自动化测试的效果

示例参考：
- [HTTP 接口测试](https://gitee.com/wangding/grunt-demo/tree/http-api-test)

## 矩形计算器 v0.3

要求：
- 切换到 rectangle 项目仓库
- 重构 rectangle.js 代码，使其易于实施单元测试
- 添加 Mocha + Chai 单元测试代码
- 在自动化构建脚本 Gruntfile.js 中添加单元测试构建任务
- 将静态代码检查和单元测试任务添加到 npm test 脚本中 
- 添加 Travis CI 配置脚本，实现代码在 gh-pages 分支的自动发布
- 用 chrome 浏览器查看自动化构建并发布的 rectangle 应用

示例参考：
- [矩形计算器 v0.3 单元测试](https://gitee.com/wangding/rectangle/commit/cb59c25a4e182f74df6f9ef94f1700fedbc6d05b?diff=split)

## 压缩 HTML 代码

要求：
- 阅读 [grunt-contrib-htmlmin 插件文档](https://www.npmjs.com/package/grunt-contrib-htmlmin)
- 在 grunt-demo 仓库，创建 htmlmin 分支
- 将 rectangle 仓库中的 HTML、CSS 和 JavaScript 代码文件复制到当前项目仓库的 htmlmin 分支下
- npm 安装 grunt 和 grunt-contrib-htmlmin 插件
- 添加 Gruntfile.js，实现 HTML 代码压缩
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [压缩 HTML 代码](https://gitee.com/wangding/grunt-demo/tree/htmlmin)

## 压缩 CSS 代码

要求：
- 阅读 [grunt-contrib-cssmin 插件文档](https://www.npmjs.com/package/grunt-contrib-cssmin)
- 在 grunt-demo 仓库，创建 cssmin 分支
- 将 rectangle 仓库中的 HTML、CSS 和 JavaScript 代码文件复制到当前项目仓库的 htmlmin 分支下
- npm 安装 grunt 和 grunt-contrib-cssmin 插件
- 添加 Gruntfile.js，实现 CSS 代码压缩
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [压缩 CSS 代码](https://gitee.com/wangding/grunt-demo/tree/cssmin)

## 压缩 JavaScript 代码

要求：
- 阅读 [grunt-contrib-uglify 插件文档](https://www.npmjs.com/package/grunt-contrib-uglify)
- 在 grunt-demo 仓库，创建 uglify 分支
- 在项目目录下创建 js 目录，并切换到 js 目录
- 运行命令 `wget https://sample.wangding.co/spa/jquery.js` 下载 jquery.js 文件
- npm 安装 grunt 和 grunt-contrib-uglify 插件
- 添加 Gruntfile.js，实现 JavaScript 代码压缩
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [压缩 JavaScript 代码](https://gitee.com/wangding/grunt-demo/tree/uglify)

## 矩形计算器 v0.4

要求：
- 用 GTmetrix 工具对自己的矩形计算器 v0.3 应用进行性能评价，将评分结果截图保存
- 切换到 rectangle 项目仓库
- 在自动化构建脚本 Gruntfile.js 中添加代码压缩构建任务
- 对 HTML、CSS 和 JavaScript 代码进行压缩
- 将代码压缩构建任务编写到 Travis CI 配置脚本中
- 确保自动发布的代码是压缩优化后的代码
- 推送修改的代码到 GitHub 仓库
- 用 chrome 浏览器查看自动化构建并发布的 rectangle 应用
- 验证应用代码是压缩后的代码
- 用 GTmetrix 工具对自己的矩形计算器 v0.4 应用进行性能评价，将评分结果截图保存
- 比较前后两个评分

示例参考：
- [矩形计算器 v0.4 实现代码压缩发布](https://gitee.com/wangding/rectangle/commit/4cffc3f00e5e1694f928a4f45771a744424ec673?diff=split)

## 电子书网站性能优化

要求：
- 用 GTmetrix 工具对自己的[电子书网站](http://spa.wangding.co/chapters/ch02-build-automation.html#%E5%9C%A8%E7%BA%BF%E7%94%B5%E5%AD%90%E4%B9%A6)进行性能评价，将评分结果截图保存
- 切换到电子书项目仓库
- 在自动化构建脚本 Gruntfile.js 中添加代码压缩构建任务
- 对 `_book` 目录下的  HTML、CSS 和 JavaScript 代码进行压缩
- 将代码压缩构建任务编写到 Travis CI 配置脚本中
- 确保自动发布的代码是压缩优化后的代码
- 推送修改的代码到 GitHub 仓库
- 用 chrome 浏览器查看自动化构建并发布的电子书网站
- 用 GTmetrix 工具对自己的电子书网站进行性能评价，将评分结果截图保存
- 比较前后两个评分

示例参考：
- [在线实验手册](http://manual.wangding.co/)

## 压缩图片

要求：
- 阅读 [grunt-contrib-imagemin 插件文档](https://www.npmjs.com/package/grunt-contrib-imagemin)
- 在 grunt-demo 仓库，添加 imagemin 分支
- 在当前项目目录下创建 images 目录，切换到 images 目录
- 运行命令 `wget https://sample.wangding.co/spa/images.tar` 下载 images.tar 文件
- 运行命令 `tar -xf images.tar` 解压图片文件
- 运行命令 `rm images.tar` 删除压缩文件
- npm 安装 grunt 和 grunt-contrib-imagemin 插件
- 添加 Gruntfile.js，实现图片压缩
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [压缩图片](https://gitee.com/wangding/grunt-demo/tree/imagemin)

## 打包合并

要求：
- 阅读 [grunt-contrib-concat 插件文档](https://www.npmjs.com/package/grunt-contrib-concat)
- 在 grunt-demo 仓库，添加 concat 分支
- 复制 rectangle v0.4 项目仓库的 HTML、CSS 和 JavaScript 代码
- 添加 Gruntfile.js，实现对 JavaScript 代码的打包合并
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [打包合并](https://gitee.com/wangding/grunt-demo/tree/concat)

## 矩形计算器 v0.5

要求：
- 阅读 [grunt-contrib-copy 插件文档](https://www.npmjs.com/package/grunt-contrib-copy)
- 阅读 [grunt-contrib-clean 插件文档](https://www.npmjs.com/package/grunt-contrib-clean)
- 阅读 [grunt-usemin 插件文档](https://www.npmjs.com/package/grunt-usemin)
- npm 安装 grunt-contrib-copy，grunt-contrib-clean，grunt-usemin 三个插件
- 用 grunt 对 rectangle.js 和 calc.js 两个脚本文件打包后压缩为 dist/bundle.min.js
- 用 grunt 自动修改 index.html 文件，使用 bundle.min.js
- 用 grunt 清理构建过程中的临时文件
- 增加网站图标，Chrome 开发者工具的控制台窗口，不要输出错误
- 添加页面初始焦点，初始焦点设置为第一个文本框
- 计算结果文本框不可编辑
- 设备自适应，页面在手机上可以正常显示
- 增加必填字段提示
- 不用考虑数据合法性校验
- 将 master 分支的代码变更推送 GitHub
- 用 Chrome 浏览器观察自动化构建并发布的 rectangle 应用
- 自动化构建包括：静态代码检查、单元测试和代码打包压缩优化

示例参考：
- [矩形计算器 v0.5 增强用户体验](https://gitee.com/wangding/rectangle/commit/ea95d134edb47645a59481eaf00a77e07bc24454?diff=split)
