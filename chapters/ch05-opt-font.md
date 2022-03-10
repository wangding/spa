# 第 5 章：优化字体

## 阅读参考资料

- [在字体加载期间避免不可见的文本](https://wpocs.cn/docs/fast-load-time/avoid-invisible-text.html)
- [优化 WebFont 加载和呈现](https://wpocs.cn/docs/fast-load-time/optimize-webfont-loading.html)
- [减小 WebFont 大小](https://wpocs.cn/docs/fast-load-time/reduce-webfont-size.html)

## 使用 Webfont

操作步骤如下：
- 启动网站 `wd13`，`npx http-server wd13`
- 思考页面使用何种字体
- 修改 `index.html`，在网站页面中使用 `liguofu.ttf` 字体
- 查看改后的网站页面，其中文字是否为手写体

## 压缩字体

- 安装字体转换工具，`npm install`
- 将 TTF 格式字体转换成 WOFF 格式，`npx ttf2woff liguofu.ttf liguofu.woff`
- 比较 TTF 格式和 WOFF 格式字体文件的尺寸，`ls -lh`
- 修改 `index.html`，在网站页面中使用 WOFF 字体
- 查看改后的网站页面，其中文字是否为手写体
- 将 TTF 格式字体转换成 WOFF2 格式，`cat liguofu.ttf | npx ttf2woff2 >> liguofu.woff2`
- 比较 TTF 格式、WOFF 格式和 WOFF2 格式字体文件的尺寸，`ls -lh`
- 修改 `index.html`，在网站页面中使用 WOFF2 字体
- 查看改后的网站页面，其中文字是否为手写体

## 观察 FOIT 和 FOUT 现象

- 在 wd13 网站中使用 WOFF 字体，确保页面中的文字是手写体
- 修改 `index.html`，在 `@font-face` 代码段中添加 `font-display: block;` 属性
- 启动 wd13 网站，`npx http-server wd13`
- 在 Network 面板设置网络限流 Fast 3G 和 Capture screenshots，刷新页面
- 观察是否出现 FOIT 现象
- 修改 `index.html`，在 `@font-face` 代码段中添加 `font-display: swap;` 属性
- 刷新网站，观察是否出现 FOUT 现象

## 取字体子集

操作步骤如下：
- 启动网站 `wd14`，`npx http-server wd14`
- 用 Network 对网站 `wd14` 做桌面性能评测
- 查看瀑布流图，是否看到 `fontawesome-webfont.woff` 字体文件的加载
- 在样式表文件中定位该字体文件，了解该字体文件在网站中的作用
- 查看并记录该字体文件的体积，`ls -al font`
- 其实网站上只使用了该字体文件中的五个字符，而加载整个字体文件得不偿失
- 另外，观察 `picture.css` 文件中定义的各种 `iconXX` 样式，用到也只有五个
- 复制 `wd14` 文件夹，`cp -r wd14 font-opt && cd font-opt`
- 首先，删除 `picture.css` 文件中无用的 `iconXX` 定义，确保网站样式正常
- 比较，优化前后 CSS 文件的大小差异
- 安装 fonttools，`sudo pip3 install fonttools`
- 创建字体子集，`pyftsubset fontawesome-webfont.woff --unicodes=f0ac,f085,f0c3,f029,f164`
- 检查字体子集文件大小，`ls -al`
- 修改字体子集文件名为源字体文件名
- 启动网站 `font-opt`，`npx http-server font-opt`
- 用 Network 对网站 `font-opt` 做桌面性能评测
- 查看瀑布流图，观察 `fontawesome-webfont.woff` 文件的字节数
