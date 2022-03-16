# 第 7 章：SPA 和 MVC

## 阅读参考资料

- [SPA](http://www.code2succeed.com/single-page-application/)
- [MVC、MVP 和 MVVM](https://blog.nodejitsu.com/scaling-isomorphic-javascript-code/)
- [前端路由](https://blog.pshrmn.com/entry/how-single-page-applications-work/)
- [URL 中的井号](http://www.ruanyifeng.com/blog/2011/03/url_hash.html)

## 前端路由

基本要求：

- 在 spa 仓库创建 51-fe-router 目录
- 页面中有一个 div 块，宽 200px，高 200px，水平居中，默认绿色
- 使用前端路由，例如：`http://ip-addr:8080/#/red` 控制页面中 div 的颜色
- 在 chrome 中测试这个程序，改变 URL 地址后面的颜色单词，观察 div 块的变化
- 点击浏览器的导航键，前进、后退，观察 div 块颜色的变化

示例参考：
- [前端路由](http://fe.wangding.co/51-fe-router/)

## MVC

基本要求：

- 在 spa 仓库创建 52-mvc 目录
- 页面上品字摆放三个视图（View）
- 一个视图（View）作为控制器，利用滑杆控件改变整数 num，变化范围：[0-255]
- 另两个视图（View）用来可视化显示数值大小
- 其中一个视图用 DIV 块的大小来反映 num
- 另一个视图用 DIV 块的颜色来反映 num
- 用 MVC 框架实现整个程序，将后两个视图绑定到 num 上
- num 变化时，通知后两个视图，改变 DIV 的大小和颜色

示例参考：
- [MVC](http://fe.wangding.co/06-mvc/)

## jsnotepad 外壳

基本要求：

- 实现 jsnotepad 外壳 index.html 文件
- index.html 文件加载所有 UI 组件的 JS 和 CSS 文件
- 外壳页面加载完成后，在浏览器窗口依次显示：菜单栏、编辑器和状态栏三个组件
- 在菜单栏的特定菜单项中弹出相应的对话框组件
- 测试 jsnotepad

## jsnotepad 帮助菜单功能

基本要求：
- 实现 jsnotepad 帮助菜单下各菜单项的相应功能
- 菜单项的功能参考 win10 的记事本程序
- 测试 jsnotepad

## jsnotepad 查看菜单功能

基本要求：
- 实现 jsnotepad 查看菜单下各菜单项的相应功能
- 菜单项的功能参考 win10 的记事本程序
- 测试 jsnotepad

## jsnotepad 格式菜单功能

基本要求：
- 实现 jsnotepad 格式菜单下各菜单项的相应功能
- 菜单项的功能参考 win10 的记事本程序
- 测试 jsnotepad

## jsnotepad 编辑菜单功能

基本要求：

- 实现 jsnotepad 编辑菜单下各菜单项的相应功能
- 菜单项的功能参考 win10 的记事本程序
- 测试 jsnotepad
