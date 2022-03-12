# 第 6 章：优化 JavaScript

## 参考资料

- [使用 PRPL 模式实现即时加载](https://wpocs.cn/docs/fast-load-time/apply-instant-loading-with-prpl.html)
- [通过代码拆分减少 JavaScript 负载](https://wpocs.cn/docs/fast-load-time/reduce-javascript-payloads-with-code-splitting.html)
- [删除未使用的代码](https://wpocs.cn/docs/fast-load-time/remove-unused-code.html)
- [缩小和压缩网络有效负载](https://wpocs.cn/docs/fast-load-time/reduce-network-payloads-using-text-compression.html)
- [为现代浏览器提供现代代码以加快页面加载速度](https://wpocs.cn/docs/fast-load-time/serve-modern-code-to-modern-browsers.html)
- [发布、传输和安装现代 JavaScript 以实现更快的应用程序](https://wpocs.cn/docs/fast-load-time/publish-modern-javascript.html)
- [CommonJS 如何让您的捆绑包变得更大](https://wpocs.cn/docs/fast-load-time/commonjs-larger-bundles.html)
- [第三方 JavaScript 性能](https://wpocs.cn/docs/fast-load-time/third-party-javascript.html)
- [识别慢速第三方 JavaScript](https://wpocs.cn/docs/fast-load-time/identify-slow-third-party-javascript.html)
- [高效加载第三方 JavaScript](https://wpocs.cn/docs/fast-load-time/efficiently-load-third-party-javascript.html)
- [使用 Web Workers](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Workers_API/Using_web_workers)

## 消除渲染阻塞

操作步骤如下：
- 启动网站 `wd15`，`npx http-server wd15`
- Chrome 浏览器打开 devtools 的 console 面板
- 输入 `wd15` 网站地址，观察浏览器页面的变化
- 观察页面上有文字出现时，console 面板打印的时长信息
- 查看 `wd15` 网站代码，思考为什么页面的文字出现会等待很长时间
- 修改 `index.html` 页面，将 `<script>` 代码放到 `<body>` 的最下面
- 重新启动 `wd15`，观察网站页面的变化以及 console 面板的时长信息
- 在 `<script>` 开始标签中添加 `defer` 布尔属性
- 重新启动 `wd15`，观察网站页面的变化以及 console 面板的时长信息
- 思考 javascript 代码对页面渲染的阻塞效果

## 动画 jank

操作步骤如下：
- 启动网站 `wd04`, `npx http-server wd04`
- Chrome 浏览器打开 devtools 的 Performance 面板，停靠在右侧
- 点击 Performance 面板的 `Record` 按钮，然后点击页面上的方块
- 当方块运动到页面下方时，停止 `Record`
- 在 Performance 面板中观察动画的 FPS 信息，思考动画是否发生 jank
- 复制 `wd04` 代码为 `jank`，`cp -r wd04 jank && cd jank`
- 把 `wd15` 下的 `calc.js` 复制到 `jank` 目录下
- 修改 `calc.js`，只保留 `fb` 函数的声明，其余代码注释掉
- 修改 `index.html`，引入 `calc.js` 代码，并在 `click` 事件中，调用 `fb(44)`
- 保存代码，启动 `jank` 网站
- 重复前面的操作，观察 `jank` 网站动画的 FPS，思考动画是否发生 jank
- 思考动画发生 jank 的原因

## Webworker

操作步骤如下：
- 复制 `jank` 网站为 `webworker`，`cp -r jank webworker && cd webworker`
- 修改 `calc.js` 代码，启用注释的代码
- 修改 `index.html`，去掉 `calc.js` 代码的引入
- 修改 `onclick` 事件响应代码，在 `onclick` 事件中，创建 `fb` webworker 线程
- 保存代码，启动 `webworker` 网站
- 使用 Performance 面板，观察动画的 FPS，思考动画是否发生 jank
- 观察 Webworker 线程的执行和主线程的关系

## 批量操作 DOM

操作步骤如下：
- 运行网站 `wd16`，`npx http-server wd16`
- Chorme 浏览器打开 devtools 的 console 面板，停靠在右侧
- 访问 `wd16` 网站，在 console 面板，执行下面的代码，进行基准测试

```javascript
// 单独操作  dom
console.time('m1');
genDom1(10000);
console.timeEnd('m1');

// 批量操作 dom
console.time('m2');
genDom2(10000);
console.timeEnd('m2');
```

- `m1` 测试后，刷新页面，测试 `m2`
- 每次测试后，记录 console 面板的数据
- 总共测试三轮
- 根据测试数据，思考哪种操作 DOM 的方式性能更好
- 查看 `wd16` 代码，掌握批量处理 DOM 的代码编写思路
- 访问 `wd16` 网站的 `react.html` 页面
- 刷新三次，记录 console 面板的数据
- 跟上面 `m1` 和 `m2` 的数据比对
