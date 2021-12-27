# 第 4 章：H5 内置控件

## 阅读参考资料

### 文本框类

- [text](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input/text)
- [textarea](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/textarea)
- [email](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/email)
- [tel](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/tel)
- [password](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/password)
- [number](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/number)
- [search](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/search)
- [url](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/url)

### 按钮类

- [button](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/button)
- [button](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/button)
- [image](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/image)
- [checkbox](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/checkbox)
- [radio](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/radio)
- [reset](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/reset)
- [submit](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/submit)

### 弹框类

- [alert()](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/alert)
- [prompt()](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/prompt)
- [confirm()](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/confirm)

### 列表类

- [select](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/select)
  - [option](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/option)
  - [optgroup](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/optgroup)
- [datalist](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/datalist)
  - [option](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/option)

### 时间日期类

- [time](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/time)
- [date](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/date)
- [month](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/month)
- [week](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/week)
- [datetime](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/datetime)
- [datetime-local](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/datetime-local)

### 其他

- [label](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/label)
- [range](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/range)
- [progress](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/progress)
- [color](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/color)
- [file](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/file)
- [hidden](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input/hidden)
- [form](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/form)
  - [fieldset](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/fieldset)
  - [legend](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/legend)
- [output](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/output)

## 作业统一说明

- 如果没有特别说明，后续任务代码放到 spa 仓库下
- spa 仓库需要同步到 gitee 远程仓库和 gogs 远程仓库
- spa 仓库需要用 grunt 进行自动化构建
- 实现 HTML、CSS、JavaScript 静态代码检查构建任务
- 实现 HTML、CSS、JavaScript 压缩构建任务
- 如有必要，添加单元测试构建任务
- 使用 drone 自动发布代码为 docker 镜像
- 执行命令 `wget https://sample.wangding.co/spa/spa.tar` 获取仓库初始代码

## 定时器按钮

基本要求：
- 创建 10-timer-button 目录
- 使用 H5 内置控件实现
- 按钮初始状态为禁用
- 禁用状态下，点击按钮，不会有任何响应
- 倒计时 6 秒
- 每隔一秒按钮文字显示剩余秒数
- 倒计时结束后，按钮状态为启用
- 启用状态下，点击按钮，会弹出 alert 弹框

示例参考：
- [定时器按钮](http://fe.wangding.co/01-html-widget/04-button.html)

## 密码可见

基本要求：
- 创建 11-password-visual 目录
- 使用 H5 内置控件实现
- 在文本框中输入任意字符，并不显示输入的字符，而显示为“点”（隐藏密码）
- 文本框的右侧有眼睛闭合的图标
- 当鼠标移到眼睛图标时
- 密码框中的密码可以正常显示
- 眼睛关闭的图标变成眼睛睁开的图标
- 当鼠标移出眼睛图标时
- 密码框中的密码不可见
- 眼睛睁开的图标变成眼睛闭合的图标
- 密码框设置为初始焦点

示例参考：
- [密码可见](http://fe.wangding.co/01-html-widget/13-password.html)

## 滑杆

基本要求：
- 创建 12-range 目录
- 使用 H5 内置控件实现
- 用滑杆控件输入自己的年龄，滑杆的最小值为 0，最大值为 100
- 滑块拖动后，下方显示年龄数据
- 初始滑块位于最左边，下方的年龄数据为 0 岁

示例参考：
- [范围控件](http://fe.wangding.co/01-html-widget/31-range.html)

## 进度条

基本要求：
- 创建 13-progress 目录
- 使用 H5 内置控件实现
- 用进度条控件模拟下载文件的进度
- 进度条控件下方有三个按钮：开始、暂停和重置
- 开始按钮点击后，进度条显示下载进度
- 暂停按钮点击后，下载进度暂停
- 重置按钮点击后，下载进度条恢复初始状态
- 多次点击开始按钮，点击一次暂停按钮，要求进度条能够暂停

示例参考：
- [进度条](http://fe.wangding.co/01-html-widget/41-progress.html)
