# 第 8 章：数据存储

## 阅读参考资料

- [web storage](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage)
- [操作浏览器历史](https://developer.mozilla.org/zh-CN/docs/Web/API/History_API)
- [浏览器数据库 IndexedDB 入门教程](http://www.ruanyifeng.com/blog/2018/07/indexeddb.html)

## localstorage 状态保持

- 在 spa 仓库创建 61-store-clicking
- 用 localstorage 保存按钮点击的次数
- 页面上按钮的文字中显示被点击的次数
- 测试程序，点击按钮，检查点击次数，刷新页面，看点击数是否清零

示例参考：
- [保存点击次数](http://fe.wangding.co/07-storage/01-local-storage.html)

## localstorage 保存图片

- 在 spa 仓库创建 62-store-image
- 页面上文本框中输入图片的 URL 地址
- 点击保存按钮，将图片保存到 localstorage 中，并显示在页面上
- 测试程序，点击保存按钮，检查页面上是否有图片
- 刷新页面，看页面上的图片是否存在

示例参考：
- [保存图片](http://fe.wangding.co/07-storage/03-image-to-local-storage.html)

## history 状态保持

- 在 spa 仓库创建 63-click-history
- 用 history 保存按钮点击的次数
- 页面上按钮的文字中显示被点击的次数
- 测试程序，点击按钮，检查点击次数，刷新页面，看点击数是否清零
- 点击浏览器的导航键，前进、后退，观察按钮文字的变化

示例参考：
- [保存点击次数](http://fe.wangding.co/07-storage/02-history.html)

## jsnotepad 状态保持

基本要求：

- 保存 jsnotepad 应用的状态，用户下次访问应用时，能够恢复到上次退出时的状态
- 状态包括：
  - 编辑器中的文本内容
  - 编辑器中的文本字体、样式、字号
  - 编辑器中光标的位置
  - 编辑器是否换行
  - 是否显示状态栏

## jsnotepad 文件菜单功能

基本要求：

- 实现 jsnotepad 文件菜单下各菜单项的相应功能
- 菜单项的功能参考 win10 的记事本程序
- 测试 jsnotepad
