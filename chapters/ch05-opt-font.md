# 第 5 章：优化字体

## 阅读参考资料

- [在字体加载期间避免不可见的文本](https://wpocs.cn/docs/fast-load-time/avoid-invisible-text.html)
- [优化 WebFont 加载和呈现](https://wpocs.cn/docs/fast-load-time/optimize-webfont-loading.html)
- [减小 WebFont 大小](https://wpocs.cn/docs/fast-load-time/reduce-webfont-size.html)

## 取字体子集

操作步骤如下：
- 启动网站 `wd13`，`npx http-server wd13`
- 用 Network 对网站 `wd13` 做桌面性能评测
- 查看瀑布流图，是否看到 `fontawesome-webfont.woff` 字体文件的加载
- 在样式表文件中定位该字体文件，了解该字体文件在网站中的作用
- 查看并记录该字体文件的体积，`ls -al font`
- 其实网站上只使用了该字体文件中的五个字符，而加载整个字体文件得不偿失
- 另外，观察 `picture.css` 文件中定义的各种 `iconXX` 样式，用到也只有五个
- 复制 `wd13` 文件夹，`cp -r wd13 font-opt && cd font-opt`
- 首先，删除 `picture.css` 文件中无用的 `iconXX` 定义，确保网站样式正常
- 比较，优化前后 CSS 文件的大小差异
- 安装 fonttools，`sudo pip3 install fonttools`
- 创建字体子集，`pyftsubset fontawesome-webfont.woff --unicodes=f0ac,f085,f0c3,f029,f164`
- 检查字体子集文件大小，`ls -al`
- 修改字体子集文件名为源字体文件名
- 启动网站 `font-opt`，`npx http-server font-opt`
- 用 Network 对网站 `font-opt` 做桌面性能评测
- 查看瀑布流图，观察 `fontawesome-webfont.woff` 文件的字节数
