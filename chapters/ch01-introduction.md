# 第 1 章：课程说明

## 阅读参考资料

- [SPA 定义](https://baike.baidu.com/item/SPA/17536313#viewPageContent)
- [RIA 定义](https://baike.baidu.com/item/RIA%E6%8A%80%E6%9C%AF/4601040?fr=aladdin)
- [Web APP 定义](https://baike.baidu.com/item/web%20app)
- [浅谈前端集成解决方案](https://github.com/fouber/blog/issues/1)
- [JavaScript 浮点运算精度解决方案](https://segmentfault.com/a/1190000013431163)
- [jQuery API 中文版](https://www.jquery123.com/)
- [IBM web 开发者中心](https://developer.ibm.com/zh/technologies/web-development/)

## 搭建开发环境

**方式一：导入虚拟机（推荐）**

- 下载并安装 vmware workstation Pro 15+（**已经安装 vmware workstation，跳过此步**）
- 下载 [mocha 虚拟机](http://pan.baidu.com/s/1o8a3E3o)压缩文件
- 解压缩 mocha 虚拟机
- 用 vmware workstation，打开解压后的 mocha 虚拟机
- 启动 mocha 虚拟机
- 登录 mocha 虚拟机，用户名：wangding，密码：ddd
- 配置 mocha 虚拟机的网卡 IP 地址，具体操作请参考：[教学视频](https://www.bilibili.com/video/bv1iy4y1y7hm)
- 确保在 mocha 虚拟机中，`ping www.baidu.com` 可以正常执行
- 下载并安装 [xshell 6](https://www.netsarang.com/zh/free-for-home-school/)
- 用 XShell 链接 mocha 虚拟机
- 配置 mocha 虚拟机的 git 参数，包括：user.name 和 user.email
- 在 GitHub 或码云创建测试仓库，确保 git 可以向远程仓库提交代码

**方式二：从头安装**

- 安装步骤请参考：[Node.js 开发环境搭建](setup-dev-env.html)
- 安装 CentOS 虚拟机，请参考：[教学视频](http://edu.51cto.com/center/course/lesson/index?id=166501)

## 熟悉开发环境的使用

- 熟悉[开发环境的使用](http://nodejs.wangding.co/env-manual.html)
- 熟悉常用的 [linux 命令用法](http://note.wangding.co/linux/centos.html)
- 熟悉 [Git 命令](http://note.wangding.co/office/git.html)的用法
- 熟悉 [vim 的用法](http://note.wangding.co/office/vim.html)

## 矩形计算器 v0.1

基本要求：
- 在 GitHub 上创建 rectangle 项目仓库
- 根据输入的矩形的长度和宽度计算矩形的周长和面积
- 使用 H5 内置控件实现
- 解决[浮点舍入误差](https://segmentfault.com/a/1190000013431163)的问题
- 不用考虑数据合法性校验
- 支持科学计数法的数据计算
- 将代码推送到 GitHub 的 rectangle 项目仓库
- 将代码通过 github pages 功能发布上线

示例参考：
- [矩形计算器](https://wangding.github.io/rectangle/)
