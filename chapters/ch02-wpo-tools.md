# 第 2 章：性能评估工具

## 用 Network 观察页面加载过程

操作步骤如下：
- 用 chrome 打开 `https://wpocs.cn` 网站
- 用 Network 面板，查看网站加载的过程
- 思考对于某一种静态资源，浏览器加载的完整过程是什么？
- 在瀑布图的时间条上悬停，查看某资源加载各个阶段的耗时，看看资源加载分几个大的阶段，每个阶段又有哪些小的阶段
- 思考是否每种资源加载的过程都是完全相同的？
- 用 chrome 浏览上一章的电器维修网站
- 用 Network 面板，查看网站加载的过程
- 观察 `index.html` 页面加载的响应头中的字段 `Connetction: Keep-Alive` 和 `Keep-Alive: timeout=5`
- 思考 `Keep-Alive` 的作用，为网站性能优化带来的好处
- 了解 `TTFB` 性能指标描述的内容，网站性能优化，应该提高 `TTFB` 还是减少 `TTFB`
- 在纸上把浏览器加载静态资源的各个阶段画下来

## 用 Ligthouse 测评网站性能

操作步骤如下：
- 使用 Lighthouse 对以下两个企业网站做性能评测
  - 云袭网络：`http://www.yunxi.cn/`
  - 航星永志：`https://www.hasng.cn/`
- 设置 Lighthouse 只测评网站性能，并选择桌面设备测评
- 查看测评报告，了解网站有哪些可以做性能优化的方面
- 用 Lighthouse 对自己感兴趣的网站做性能评测
- 将评测数据保存到本地磁盘
- 思考六个性能指标的含义

## 用 Performance 了解网站渲染过程

操作步骤如下：
- 使用 Performance 对[云袭网络](http://www.yunxi.cn/)做性能评测
- 通过 Performance 的信息，观察和印证浏览器的工作原理
- 通过 Performance 的信息，观察和印证页面渲染的过程
- 思考 Performance 的火焰图，水平方向和垂直方向各代表什么
- 观察 Performance 和 Network 信息是否对应
- 通过 Performance 观察浏览器的四类活动：
  - 加载（蓝色）
  - 脚本（黄色）
  - 渲染（紫色）
  - 绘制（绿色）

## JavaScript 基准测试

操作步骤如下：
- 启动 `wd01` 网站，`npx http-server wd01`
- 在 chrome 的控制台面板下，做两种 DOM 查询：
  - jQuery DOM 查询：`$('.logo')[0]`
  - H5 内置查询方法：`document.querySelector('.logo')`
- 确认查到了电器维修网站的 logo
- 用 `console.time` 和 `console.timeEnd` 方法做基准测试
- 比较 jQuery DOM 查询和 H5 内置查询方法，哪个速度更快
- 在控制台执行代码：
```javascript
console.time('jQuery');
$('.logo');
console.timeEnd('jQuery');
console.time('H5-selector');
document.querySelector('.logo');
console.timeEnd('H5-selector');
```
- 多执行几次，观察每次执行的时长是否相同，快慢的结论有变化吗？

## 用 WebpageTest 做性能评测

操作步骤如下：
- 用 [WebpageTest](https://webpagetest.org/) 在全球不同地点，对 `http://spa.wangding.co` 网站做性能评估
  - 浏览器第一个标签页，Advanced 选择：北美，城市随意，其他默认
  - 浏览器第二个标签页，Advanced 选择：亚洲，北京，其他默认
- 点击 `Start Test` 按钮
- 观察两个不同地点对同一个网站，性能指标有何差异
- 思考是什么原因导致的
- 用 WebpageTest 对自己感兴趣的网站做性能测试，可以调整测试的参数，包括：
  - 地点
  - 设备
  - 性能模型
  - 网络速度
  - 浏览器型号，等
- 查看测试报告，除了性能指标，可以查看瀑布图
