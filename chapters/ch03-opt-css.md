# 第 3 章：优化 CSS

## 阅读参考资料

- [延迟加载非关键 CSS](https://wpocs.cn/docs/fast-load-time/defer-non-critical-css)
- [压缩 CSS](https://wpocs.cn/docs/fast-load-time/minify-css)
- [提取关键 CSS (Critical CSS)](https://wpocs.cn/docs/fast-load-time/extract-critical-css)
- [使用媒体查询优化 CSS 背景图像](https://wpocs.cn/docs/fast-load-time/optimize-css-background-images-with-media-queries)

## 简写 CSS

操作步骤如下：
- 复制 `wd01/start` 文件夹为 `shorthand`，`cp -r start shorthand`
- 检查 `css/styles.css` 代码中是否使用简写，`grep -n "margin\|padding\|border" css/styles.css`
- 用 `postcss` 工具和 `postcss-merge-longhand` 插件，完成 CSS 代码的简写重构
- **注意**：`postcss-merge-longhand` 只处理 CSS 代码中的 `margin`, `padding` 和 `border` 三种简写
- 安装 `postcss` 和插件，`npm i -D postcss-cli postcss-merge-longhand`
- 编写 `postcss` 的配置文件 `postcss.config.js`
```javascript
module.exports = {
    plugins: [
        require('postcss-merge-longhand')()
    ]
}
```
- 运行命令，`npx postcss styles.css -o styles.short.css`
- 检查优化前后 CSS 文件大小的变化，`ls -lh`
- 检查优化前后 CSS 文件行数的变化，`wc -l styles.css styles.short.css`
- 比较优化前后 CSS 文件的具体变化，`vimdiff style.css styles.short.css`
- 运行修改后的网站，`npx http-server shorthand`
- 确保网站的样式和修改之前没有变化

## 使用浅选择器

操作步骤如下：
- 复制 `wd01/start` 文件夹为 `shallow`，`cp -r start shallow`
- 检查 `css/styles.css` 代码中是否使用浅选择器，`grep -n "{" css/styles.css`
- 手工修改几个选择器为浅选择器
- 运行修改后的网站，`npx http-server shallow`
- 确保网站的样式和修改之前没有变化

## 去掉不用的 CSS

操作步骤如下：
- 复制 `wd01/start` 文件夹为 `unused`，`cp -r start unused`
- 安装 `uncss` 工具，`npm i -D uncss`
- 运行网站，`npx http-server unused`
- 运行 `uncss` 工具，`npx uncss http://localhost:8080 > out.css`
- 备份原有的 CSS 代码文件，`mv styles.css styles.css.bak`
- 修改 `out.css` 文件名，并放到 `css` 目录下，`mv out.css styles.css`
- 重新运行网站，观察优化后的网站样式是否正常
- 比较优化前后两个 CSS 文件的差异，`vimdiff styles.css styles.css.bak`
- **注意**：`uncss` 工具不是很智能，可能会误删除一些有用的代码，使用时一定要仔细测试
- 运行 `wd02` 网站，`npx http-server wd02`
- 运行 `uncss` 工具，`npx uncss http://localhost:8080 > out.css`
- 比较优化前后两个 CSS 文件的差异，`vimdiff styles.css out.css`
- 观察有用的 CSS 代码是否被误删除

## 去掉冗余的 CSS

操作步骤如下：
- 复制 `wd01/start` 文件夹为 `redundance`，`cp -r start redundance`
- 安装 `csscss` 工具，`gem install csscss`
- 运行 `csscss` 工具分析 `wd01/start` 网站的 CSS 冗余代码，`csscss styles.css -v --no-match-shorthand`
- 根据分析的冗余代码修改原有的 CSS 代码文件
- 对修改后的 CSS 代码，用 `csscss` 再次分析，直到没有冗余代码为止
- 比较修改后的 CSS 代码与源文件的行数，`wc -l wd01/start/css/styles.css redundance/css/styles.css`
- 比较修改后的 CSS 代码与源代码文件的差异，`vimdiff wd01/start/css/styles.css redundance/css/styles.css`

## 避免使用 @import 声明

操作步骤如下：
- 运行 `wd03` 网站，`npx http-server wd03`
- 打开 Network 面板，在快速 3G 网络限流的条件下，过滤查看所有 CSS 文件的加载过程
- 是否看到 CSS 文件分四组串行加载，在每一组中 CSS 文件并行加载
- 查看引起加载的 CSS 代码文件，是否看到 `@import` 声明
- 思考为什么 `@import` 会导致 CSS 文件的串行加载
- 修改 `index.html` 文件，给每个 CSS 文件添加一个 `<link>` 标签
- 修改 CSS 文件，删除 `@import` 语句
- 运行 `wd03` 网站，`npx http-server wd03`
- 打开 Network 面板，在快速 3G 网络限流的条件下，过滤查看所有 CSS 文件的加载过程
- 是否看到 CSS 文件加载的方式，是否还有串行加载的现象？
- 这种串行加载是什么导致的？

## head-link vs body-link

操作步骤如下：
- 运行 `wd01/start` 网站，`npx http-server wd01/start`
- 打开 Network 面板，设置快速 3G 网络限流
- 在 Performance 面板，开启加载性能评测
- 把 Summary 中各部分时间汇总信息截图
- 修改 `wd01/start` 网站的 `index.html` 页面，把 `<link>` CSS 样式表代码移到 `<body>` 标签的底部 `<script>` 标签的前面
- 运行 `wd01/start` 网站，`npx http-server wd01/start`
- 在 Performance 面板，再次开启加载性能评测
- 观察浏览器页面是否出现无样式内容闪烁现象
- 把 Summary 中各部分时间汇总信息截图
- 跟上一次的 Summary 数据比对，渲染和绘制时间是否有区别
- 思考什么原因导致 `<body> <link>` 的渲染和绘制时间增加？

## 简单的过渡动画

操作步骤如下：
- 创建文件夹 `wd04`，添加 `index.html` 和 `styles.css`
- 页面上显示一个 150 X 150 像素的颜色方块
- 当鼠标点击此方块时，利用过渡效果将方块变成圆，并向下移动 200px
- 运行该页面验证程序的功能，`npx http-server wd04`

## 过渡动画 vs jQuery 动画

操作步骤如下：
- 复制 `wd01/start` 文件夹为 `transition`，`cp -r start transition`
- 修改 `css/styles.css` 代码和 `js/behaviors.js` 使用过渡动画实现预约对话框的弹出
- 启动修改后的网站，`npx http-server transition`
- 用 Performance 面板对预约对话框的弹出做性能测试
- 查看 Summary 中的各个阶段的耗时，截图保存
- 启用修改之前的网站，`npx http-server wd01/start`
- 用 Performance 面板对预约对话框的弹出做性能测试
- 查看 Summary 中的各个阶段的耗时
- 两个版本在渲染和绘制上耗时有什么差别？
- jQuery 动画除了渲染和绘制耗时长，另外，还有布局抖动的问题
- transition 版本的代码中也存在布局抖动的问题，思考问题处在哪里

## 延迟加载非关键 CSS

操作步骤如下：
- 启动 `wd05` 网站，`npx http-server wd05`
- 打开 Devtools 的 Performance 面板，评测网站的性能
- 在跟踪信息中，观察 FCP 和 CSS 完成加载在时间轴上的位置关系
- 思考这是什么现象？
- 打开 Coverage 工具，重新加载页面
- 在 Coverage 工具中，查看 `style.css` 的关键样式
- 关键样式和非关键样式的比例如何？（蓝色的为关键样式，红色的为非关键样式）
- 到底哪些代码是关键样式呢？点击 Coverage 中的 `style.css`
- 会打开 Source 面板，在代码左侧有蓝条和红条，标识出到底哪些代码是关键样式代码，哪些代码是非关键样式代码
- 下面操作会根据 Source 面板的内容，将关键样式代码内联到 `index.html` 中，并将非关键样式代码延迟加载
- 复制 `wd05` 网站，`cp -r wd05 critical-css`
- 打开 `index.html` 文件，添加 `style` 标签将关键 CSS 代码内联
- 编辑 `index.html` 文件的 `link` 标签，将 `style.css` 延迟加载
- 编辑 `style.css` 文件，删除关键样式代码
- 启动 `critical-css` 网站
- 打开 Devtools 的 Performance 面板，评测网站的性能
- 在跟踪信息中，观察 FCP 和 CSS 完成加载在时间轴上的位置关系
