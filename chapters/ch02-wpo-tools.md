# 第 2 章：性能评估工具

## 用 Network 观察页面加载过程

操作步骤如下：
- 用 chrome 打开 `https://wpocs.cn` 网站
- 在 Network 选项卡查看网站加载的过程
- 思考对于某一种静态资源，浏览器加载的完整过程是什么？
- 通过 Network 选项卡，点击
- 关闭 HTTP 静态文件服务，`CTRL + C`
- `optimized` 为性能优化后的网站
- 启动 HTTP 静态文件服务，`npx http-server optimized`
- `F5` 刷新网站页面
- 用 Network 选项卡观察性能优化前后网站加载速度的差异

