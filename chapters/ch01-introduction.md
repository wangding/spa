# 课程说明

## 阅读参考资料

- [SPA 定义](https://baike.baidu.com/item/SPA/17536313#viewPageContent)
- [RIA 定义](https://baike.baidu.com/item/RIA%E6%8A%80%E6%9C%AF/4601040?fr=aladdin)
- [Web APP 定义](https://baike.baidu.com/item/web%20app)
- [JavaScript 浮点运算精度解决方案](https://segmentfault.com/a/1190000013431163)

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
- 安装 CentOS 虚拟机，请参考：[教学视频](https://www.bilibili.com/video/BV1Bw411o712?p=2)

## 配置开发环境

**4.1 配置 git 参数**

- 配置 git 的 user.name 和 user.email 参数，否则 `git commit` 不能正常工作
- 运行命令 `git config --list`，查看当前的 git 配置信息
- 如果没有配置 user.name 和 user.email 参数，请执行下面的操作
- 运行命令 `git config --global user.email "Your Email"`，配置 user.name 参数
- 运行命令 `git config --global user.name "Your Name"`，配置 user.email 参数
- 注意，上面两个命令需要把双引号中的文字改成具体的姓名和邮箱
- 运行命令 `git config --list`，查看刚配置的 git 参数

**4.2 配置默认的 node.js 版本**

- 虚拟机中用 nvm 安装了 node.js 三个版本：8, 10 和 12，运行 `nvm list` 命令，可以查看到这些信息
- 运行 `nvm use` 命令，可以切换到 node.js 三个版本中的任意一个
- nvm 默认的 node.js 版本是 8.11，意味着如果运行 `nvm use 12`，将 node.js 版本切换到 12，但是 linux 重启后，node.js 版本会自动恢复到 8.11
- 运行命令 `nvm alias default 12.18`，将 node.js 的默认版本设为 12.18

## 熟悉开发环境的使用

- 熟悉[开发环境的使用](http://nodejs.wangding.co/env-manual.html)
- 熟悉常用的 [linux 命令用法](http://note.wangding.co/linux/centos.html)
- 熟悉 [Git 命令](http://note.wangding.co/office/git.html)的用法
- 熟悉 [vim 的用法](http://note.wangding.co/office/vim.html)

## 矩形计算器 v0.1

基本要求：
- 在 [BitBucket](https://bitbucket.org/) 上创建 rectangle 项目仓库
- 根据输入的矩形的长度和宽度计算矩形的周长和面积
- 使用 H5 内置控件实现
- 解决[浮点舍入误差](https://segmentfault.com/a/1190000013431163)的问题
- 不用考虑数据合法性校验
- 支持科学计数法的数据计算
- 将代码发布上线到[七牛云](https://www.qiniu.com/)

示例参考：
- [矩形计算器](http://rectangle.wangding.co/)
