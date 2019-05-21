# 第 1 章：课程说明  

## 阅读参考资料

- [SPA 维基百科定义](https://en.wikipedia.org/wiki/Single-page_application)
- [RIA 维基百科定义](https://en.wikipedia.org/wiki/Rich_Internet_application)
- [Web APP 维基百科定义](https://en.wikipedia.org/wiki/Web_application)
- [浅谈前端集成解决方案](https://github.com/fouber/blog/issues/1)
- [JavaScript 浮点运算精度解决方案](https://segmentfault.com/a/1190000013431163)
- [jQuery API 中文版](https://www.jquery123.com/)
- [IBM web 开发者中心](https://www.ibm.com/developerworks/cn/web/)

## 搭建开发环境

SPA 富应用开发课程所使用的开发环境是基于 CentOS 7 Linux 操作系统的，纯命令行模式的，Node.js 的前端开发环境。首先需要安装 CentOS 7 Linux 虚拟机，其次安装 Node.js 开发环境，最后安装前后端开发辅助工具。具体安装步骤见下面的两种方式：

**方式一：导入虚拟机**

- 下载并安装 vmware workstation Pro 12+（**已经安装 vmware workstation，略过此任务**）  
- 下载并导入 [mocha.ova](http://pan.baidu.com/s/1o8a3E3o) 开发环境  
- 下载并安装 [xshell 6](https://www.netsarang.com/zh/free-for-home-school/)
- 配置 mocha 虚拟机的网卡 IP 地址  
- 配置 mocha 虚拟机的 git 参数，包括：user.name 和 user.email  
- 具体操作请参考：[教学视频](https://ke.qq.com/webcourse/index.html#cid=244604&term_id=100288380&taid=1695519944719228&vid=e1421d3pl7e)
- 上述步骤完成后，需要升级 mocha 虚拟机环境，请按[这个文档](./mocha-dev-env.md)操作

**方式二：从头安装**

- 安装步骤请参考：[Node.js 开发环境搭建](./setup-dev-env.md)
- 安装 CentOS 虚拟机，请参考：[教学视频](http://edu.51cto.com/center/course/lesson/index?id=166501)

## 矩形计算器 v0.1

基本要求：
- 在 GitHub 上创建 rectangle 项目仓库
- 根据输入的矩形的长度和宽度计算矩形的周长和面积
- 使用 H5 内置控件实现
- 解决浮点舍入误差的问题
- 不用考虑数据合法性校验
- 支持科学计数法的数据计算
- 将代码推送到 GitHub 的 rectangle 项目仓库
- 将代码通过 github pages 功能发布上线

示例参考：
- [矩形计算器](https://fe.wangding.in/00-first-app/index.html)
