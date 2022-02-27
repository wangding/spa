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

## 消除渲染阻塞

操作步骤如下：
- 启动网站 `wd14`，`npx http-server wd14`
- 用 Performa 面板对网站 `wd14` 做性能评测
- 查看 FC、FCP 和 FLP 三个指标
- 复制 `wd06` 文件夹，`cp -r wd06 image-format && cd image-format`
- 根据优化建议详情，修改两个图片的格式，把 `flower_photo.jpg` 改成 webp 格式，把 `flower_logo.png` 改成 svg 格式
- 全局安装 `cwebp`，`npm i -g cwebp`
- 用 `cwebp` 做图片格式转换，`cwebp flower_photo.jpg -o flower_photo.webp`
- 检查 webp 和 jpg 格式的图片文件大小的差异，`ls -lh`
- 用 [IMG2GO](https://www.img2go.com/convert-to-svg) 将 `flower_photo.png` 转换成 svg 格式
- 检查 svg 和 jpg 格式的图片文件大小的差异，`ls -lh`
- 用 `svgo` 压缩 SVG 图片，`npx svgo flower_logo.svg -o flower_logo.min.svg`
- 观察压缩前后 SVG 图片尺寸的变化，`ls -al *.svg`
- 思考 SVG 尺寸变化背后的原因
- 修改 `index.html` 文件，使用两个新格式的图片
- 启动网站 `image-format`，`npx http-server image-format`
- 用 Lighthouse 对 `image-format` 网站做桌面性能评测
- 查看 Lighthouse 的优化建议，是否有 `Serve images in next-gen formats`
`
onctent
