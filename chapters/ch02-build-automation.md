# 第 2 章：自动化构建

## 阅读参考资料

- 自动化构建：https://en.wikipedia.org/wiki/Build_automation
- 持续集成：https://en.wikipedia.org/wiki/Continuous_integration
- Grunt：https://www.gruntjs.net/
- Travis-CI: https://travis-ci.org/
- Google PageSpeed Insights: https://developers.google.com/speed/pagespeed/insights/
- 站长工具：http://tool.chinaz.com/

## 在线电子书

要求：
- 在 GitHub 上创建 book 仓库
- 在 book 仓库的 master 分支放置电子书的章节和目录的 MarkDown 文档
- 在 book 仓库的 gh-pages 分支放置 gitbook build 后的 HTML 文件
- 电子书的前两章用手动构建，并完成第一次发布上线
- 用 Chrome 浏览器查看在线电子书
- 增加电子书的第三章，继续使用手动构建，并完成第二次发布上线
- 用 Chrome 浏览器查看更新后的电子书
- 体验手动构建的繁琐，考虑哪些构建过程可以自动化完成
- 阅读 [Travis-CI gh-gage 自动部署文章](https://segmentfault.com/a/1190000015274243)
- 配置电子书 book 仓库启用 Travis-CI
- 获取个人 GitHub 账户开发者 API token
- 配置 book 仓库的 Travis-CI 环境变量
- 在 book 仓库的 master 分支，添加 .travis.yml 和 package.json 文件
- 在 book 仓库增加第四章的 MarkDown 文件
- 将 master 分支的变更推送 GitHub 服务器
- 在 Travis-CI 网站查看自动构建脚本执行的情况
- 用 Chrome 浏览器查看自动构建后的电子书

示例参考：
- [实验手册在线电子书](https://manual.wangding.in/)
- [实验手册电子书仓库](https://github.com/wangding/info-theory-lab-manual)

## LESS 预处理

要求：
- 阅读 [grunt-contrib-less 插件文档](https://www.npmjs.com/package/grunt-contrib-less)
- 在 GitHub 上创建 grunt-demo 仓库
- 在 grunt-demo 仓库添加 less 分支
- 在 less 分支添加 index.html 页面和 LESS 样式
- npm 安装 grunt 和 grunt-contrib-less 插件
- 添加 Gruntfile.js，实现 LESS 预处理
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [LESS 预处理](https://github.com/wangding/grunt-demo/tree/less)

## HTML 静态代码检查

要求：
- 阅读 [grunt-htmlhint 插件文档](https://www.npmjs.com/package/grunt-htmlhint)
- 阅读 [htmlhint 规则文档](https://segmentfault.com/a/1190000013276858)
- 在 grunt-demo 仓库添加 htmlhint 分支
- 在 htmlhint 分支复制 rectangle 仓库的 index.html、rectangle.css 和 rectangle.js 三个代码文件
- 添加 .htmlhintrc 配置文件
- npm 安装 grunt 和 grunt-htmlhint 插件
- 添加 Gruntfile.js，实现 HTML 代码静态代码检查
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [HTML 静态代码检查](https://github.com/wangding/grunt-demo/tree/htmlhint)

## CSS 静态代码检查

要求：
- 阅读 [grunt-contrib-csslint 插件文档](https://www.npmjs.com/package/grunt-contrib-csslint)
- 阅读 [csslint 规则文档](https://github.com/CSSLint/csslint/wiki/Rules)
- 在 grunt-demo 仓库添加 csslint 分支
- 在 csslint 分支复制 rectangle 仓库的 index.html、rectangle.css 和 rectangle.js 三个代码文件
- 添加 .csslintrc 配置文件
- npm 安装 grunt 和 grunt-contrib-csslint 插件
- 添加 Gruntfile.js，实现 CSS 代码静态代码检查
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [CSS 静态代码检查](https://github.com/wangding/grunt-demo/tree/csslint)

## JavaScript 静态代码检查

要求：
- 阅读 [grunt-eslint 插件文档](https://www.npmjs.com/package/grunt-eslint)
- 阅读 [eslint 规则文档](http://eslint.cn/docs/rules/)
- 在 grunt-demo 仓库添加 eslint 分支
- 在 eslint 分支复制 rectangle 仓库的 index.html、rectangle.css 和 rectangle.js 三个代码文件
- 添加 .eslintrc.json 配置文件
- npm 安装 grunt 和 grunt-eslint 插件
- 添加 Gruntfile.js，实现 JavaScript 代码静态代码检查
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [JavaScript 静态代码检查](https://github.com/wangding/grunt-demo/tree/eslint)

## 矩形计算器 v0.2

要求：
- 切换到 rectangle 项目仓库
- npm 安装 grunt 和相应的 grunt 插件
- 添加自动化构建脚本 Gruntfile.js
- 对 HTML、CSS 和 JavaScript 代码实现静态代码检查
- 添加 Travis CI 配置脚本，实现代码在 gh-pages 分支的自动发布
- 用 chrome 浏览器查看自动化构建并发布的 rectangle 应用

示例参考：
- [矩形计算器 v0.2 代码静态检查](https://github.com/wangding/rectangle/commit/16066ea1f253e2c7192ac84e4972c441f335148b?diff=split)

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
- [服务端单元测试](https://github.com/wangding/grunt-demo/tree/mocha-be/)

## entropy 的单元测试

要求：
- 在 grunt-demo 仓库，创建 entropy 分支
- 获取 [entropy.js](https://github.com/wangding/nodejs-demo/blob/master/24-project/entropy.js) 被测程序
- entropy 程序的功能描述，请参考 [Node.js 大作业](https://nodejs.wangding.in/task18.html)
- 重构 entropy.js 代码，使其易于实施单元测试
- 添加 mocha 单元测试代码
- 运行 grunt mocha 单元测试，查看单元测试输出结果
- 查看代码覆盖率报告 

示例参考：
- [entropy 的单元测试](https://github.com/wangding/grunt-demo/tree/entropy/)

## 前端代码单元测试

要求：
- 阅读 [grunt-mocha 插件文档](https://www.npmjs.com/package/grunt-mocha)
- 在 grunt-demo 仓库，创建 mocha-fe 分支
- 将 rectangle 仓库中的 index.html、rectangle.js 和 rectangle.css 三个代码文件复制到当前项目仓库的 mocha-fe 分支下
- 重构 rectangle.js 代码，使其易于实施单元测试
- 添加 mocha 单元测试代码
- 运行 grunt mocha 单元测试，查看单元测试输出结果

示例参考：
- [前端代码单元测试](https://github.com/wangding/grunt-demo/tree/mocha-fe/)

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
- [矩形计算器 v0.3 单元测试](https://github.com/wangding/rectangle/commit/cb59c25a4e182f74df6f9ef94f1700fedbc6d05b?diff=split)

## 压缩 HTML 代码

要求：
- 阅读 [grunt-contrib-htmlmin 插件文档](https://www.npmjs.com/package/grunt-contrib-htmlmin)
- 在 grunt-demo 仓库，创建 htmlmin 分支
- 将 rectangle 仓库中的 HTML、CSS 和 JavaScript 代码文件复制到当前项目仓库的 htmlmin 分支下
- npm 安装 grunt 和 grunt-contrib-htmlmin 插件
- 添加 Gruntfile.js，实现 HTML 代码压缩
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [压缩 HTML 代码](https://github.com/wangding/grunt-demo/tree/htmlmin)

## 压缩 CSS 代码

要求：
- 阅读 [grunt-contrib-cssmin 插件文档](https://www.npmjs.com/package/grunt-contrib-cssmin)
- 在 grunt-demo 仓库，创建 cssmin 分支
- 将 rectangle 仓库中的 HTML、CSS 和 JavaScript 代码文件复制到当前项目仓库的 htmlmin 分支下
- npm 安装 grunt 和 grunt-contrib-cssmin 插件
- 添加 Gruntfile.js，实现 CSS 代码压缩
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [压缩 CSS 代码](https://github.com/wangding/grunt-demo/tree/cssmin)

## 压缩 JavaScript 代码

要求：
- 阅读 [grunt-contrib-uglify 插件文档](https://www.npmjs.com/package/grunt-contrib-uglify)
- 在 grunt-demo 仓库，创建 uglify 分支
- 在项目目录下创建 js 目录，并切换到 js 目录
- 运行命令 `wget https://sample.wangding.in/spa/jquery.js` 下载 jquery.js 文件
- npm 安装 grunt 和 grunt-contrib-uglify 插件
- 添加 Gruntfile.js，实现 JavaScript 代码压缩
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [压缩 JavaScript 代码](https://github.com/wangding/grunt-demo/tree/uglify)

## 矩形计算器 v0.4

要求：
- 切换到 rectangle 项目仓库
- 在自动化构建脚本 Gruntfile.js 中添加代码压缩构建任务
- 将代码压缩构建任务编写到 Travis CI 配置脚本中
- 确保自动发布的代码是压缩优化后的代码
- 推送修改的代码到 GitHub 仓库
- 用 chrome 浏览器查看自动化构建并发布的 rectangle 应用
- 验证应用代码是压缩后的代码

示例参考：
- [矩形计算器 v0.4 实现代码压缩发布](https://github.com/wangding/rectangle/commit/4cffc3f00e5e1694f928a4f45771a744424ec673?diff=split)

## 压缩图片

要求：
- 阅读 [grunt-contrib-imagemin 插件文档](https://www.npmjs.com/package/grunt-contrib-imagemin)
- 在 grunt-demo 仓库，添加 imagemin 分支
- 在当前项目目录下创建 images 目录，切换到 images 目录
- 运行命令 `wget https://sample.wangding.in/spa/images.tar` 下载 images.tar 文件
- 运行命令 `tar -xf images.tar` 解压图片文件
- 运行命令 `rm images.tar` 删除压缩文件
- npm 安装 grunt 和 grunt-contrib-imagemin 插件
- 添加 Gruntfile.js，实现图片压缩
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [压缩图片](https://github.com/wangding/grunt-demo/tree/imagemin)

## 打包合并

要求：
- 阅读 [grunt-contrib-concat 插件文档](https://www.npmjs.com/package/grunt-contrib-concat)
- 在 grunt-demo 仓库，添加 concat 分支
- 复制 rectangle v0.4 项目仓库的 HTML、CSS 和 JavaScript 代码
- 添加 Gruntfile.js，实现对 JavaScript 代码的打包合并
- 执行自动化任务，观察自动化构建执行的效果

示例参考：
- [打包合并](https://github.com/wangding/grunt-demo/tree/concat)

## 合并子图

要求：
- 阅读 [grunt-spritesmith 插件文档](https://www.npmjs.com/package/grunt-spritesmith)
- 在 grunt-demo 仓库，添加 sprite 分支
- 在当前项目目录下创建 images 目录，切换到 images 目录
- 运行命令 `wget https://sample.wangding.in/spa/icons.tar`，下载 icons.tar 文件
- 运行命令 `tar -xf icons.tar`，解压 icons.tar
- 运行命令 `rm icons.tar` 删除压缩文件
- 添加 Gruntfile.js，实现子图合并
- 执行自动化任务，观察自动化构建执行的效果
- 在 dist 目录下，添加 `index.html` 文件，引用生成后的 CSS 文件
- 在 dist 目录下，启动 web 静态文件服务
- 在浏览器中查看 index.html 页面效果

示例参考：
- [合并子图](https://github.com/wangding/grunt-demo/tree/sprite)

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
- [HTTP 接口测试](https://github.com/wangding/grunt-demo/tree/http-api-test)

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
- [矩形计算器 v0.5 增强用户体验](https://github.com/wangding/rectangle/commit/ea95d134edb47645a59481eaf00a77e07bc24454?diff=split)
