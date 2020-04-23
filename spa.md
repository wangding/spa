# SPA 富应用开发

## 1. 课程说明

### 课程资料

- 课程资料（https://spa.wangding.in）
- 参考书
	- JavaScript Web 应用开发
    - 单页 Web 应用 JavaScript 从前端到后端
- 常用网站
	- SegmentFault（https://segmentfault.com/）
	- GitHub（https://github.com/）
    - MDN（https://developer.mozilla.org/zh-CN/）



### 前置课程

- HTML
- CSS
- JavaScript
- JQuery
- Node.js


### 课程理念和思路

### 教学目标

### 课程结构及课时规划

总课时：20 次，一次半天，共三个小时

课时分配：
- 课堂讲授：一个半小时
- 课堂练习：一个半小时

课时规划:
- 课程简介：1 次
- 自动化构建：4 次
- 文本和图像：1 次
- 音频和视频：1 次
- V - 界面交互：10 次
	- UI 概述：1 次
	- H5 内置控件：1 次（对 H5 控件做扩展和定制）
	- 数据合法性校验：1 次
	- 第三方控件库：2 次
	- 自定义 UI 组件：3 次
	- SPA：1 次
	- MVC：1 次
- M - 数据存储：1 次
	- 本地存储
	- 历史状态
- C - 流程控制（略）
- 多媒体：2 次
    - 文本和图像：1 次
	- 音频和视频：1 次
- 综合案例实战：2 次

### Web 应用简介

#### 应用分类之一

#### 什么是 web app

#### 什么是 SPA

#### 什么是 RIA

#### 常见的 Web app

#### Web 技术发展概述

### 搭建开发环境

搭建开发环境
- IDE：Vim 插件
	- emmet-vim 插件，提高 HTML 代码的编写效率
	- .tern-project 配置，增加前端代码的自动补全
	- .vimrc 配置，增加 YCM 的 CSS 代码自动补全
	- .vimrc 配置，增加 HTML 代码模板快捷键
	- .vimrc 配置，增加 HTML、CSS、JavaScript 静态代码检查
- Git
	- user.name 和 user.email 设置
- Lint 工具
	- HTMLHint
	- CSSLint
	- ESLint
- 其他工具
	- Live Reload
	- Chrome DevTools
	- Grunt

### 第一个 web app

## 2. 自动化构建

### 问题引入

### 自动化构建概述

#### 三个环境

#### 两个模式

#### 工具比较

### 构建任务：预处理

### 构建任务：质量保证

#### 静态代码检查

#### 单元测试

#### 接口测试

### 构建任务：性能优化

#### 打包合并

#### 压缩代码

#### 压缩图片

### 构建任务：自定义任务

### 持续集成

- 工作原理
- Node.js 项目配置
-自动发布


## 3. UI 概述

### 接口概述

接口是什么？

In computing, an interface is a shared boundary across which two or more separate components of a computer system exchange information. 

The exchange can be between software, computer hardware, peripheral devices, humans, and combinations of these.

接口分类：

- 硬件接口
- 软件接口
	- API
    - ABI
- 人机接口
	- 硬件：各种输入/输出设备
    - 软件：用户界面
 
用户界面 User Interface 是接口中的一类，属于人机交互接口，并且是人机交互接口中的软件的一类。
 
这是本课程研究的重点，其他的接口，咱们这里不讨论。

### UI 类型

主要有六大类（不止这六类）：

- Batch Interface
- TUI
- GUI
- WUI
- TUI
- CLI

这里重点介绍两大类：

- CUI
- GUI，GUI 发展的两个分支：
    - WUI
    - MUI

### CUI 交互要素

- 命令行语法
- 管道和重定向
- 字符展开
- 命令类型
- 命令行提示符


### GUI 交互要素

Graphic User Interface，GUI，图形用户界面，主要就是窗体界面。

Windows App 组成，自顶向下分解为：

- 用户界面 - 窗体 - V(iew)
  - 标题栏
  - 菜单栏
    - 系统菜单
    - 下拉菜单
    - 快捷菜单
  - 工具栏
  - 主窗体
  - 状态栏
  - 对话框
    - 模态对话框
    - 无模态对话框
    - 控件
- 数据存储 - M(odel）
- 逻辑控制 - C(ontroler)


#### 窗体

按处理文档数量分类：

- SDI
- MDI

按窗体形状分类：

- 规则窗体
- 不规则窗体

主窗体自上而下包含的元素：

- 标题栏 titlebar
  - App Logo
  - App Name
  - Doc Name
  - titlebar Button
- 菜单栏 menu bar
- 工具栏 tool bar
- 内容区 window content
- 状态栏 status bar

#### 对话框

dialog box

分两大类：

- 模态对话框 modal
- 非模态对话框 modeless

特殊的对话框：向导

注意对话框标题栏跟窗体标题栏的区别

常见对话框：

- about box
- alert box

#### 菜单栏

- 下拉菜单 pull down menu
- 系统菜单 system menu
- 快捷菜单 context menu （上下文菜单）

#### 工具栏

#### 内容区

#### 状态栏

#### 控件 →

### GUI 视觉要素

- 字体
- 颜色
- 图像
- 图形
- 图标

### UI 设计原则

### WUI

- WUI 和 GUI 的差异
    - 开发方式
    - 交互要素

以百度脑图 web app 作为研究对象

- 交互要素，逐一检查
- 视觉要素，逐一检查

## 4. H5 内置控件

- 常用控件类别
  - 该类别下的控件列表
- 每种控件
  - 常用属性
  - 核心属性
  - 样式属性
  - 通用样式属性
    - 宽度
    - 高度
    - 字体
    - 颜色
    - 背景色
    - 文字颜色
    - 背景
    - 特殊样式属性
  - 常用方法
  - 常用事件
- DemoCode

### H5 内置控件

### 控件分类

#### 文本框类

- 单行文本框
```
<input type="text">
```
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text

- 多行文本框
```
<textarea>
```
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea

- 文本框变种
	- 密码框
	- Email 框
	- 数字框
	- Search
	- tel
	- url


#### 按钮类

- Button
```html
<input type="button" value=“按钮”>
<button>按钮</button>
```
- Image Button
```
<input type="image">
<button><img></button>
```
- Radio Button
- Check Box
- Reset Button
```html
<input type="reset" value="重置">
```
- Submit Button
```html
<input type="submit" value="提交">
```

- 经典案例：计算器


#### 弹框类

- alert
https://developer.mozilla.org/zh-CN/docs/Web/API/Window/alert

- prompt
https://developer.mozilla.org/zh-CN/docs/Web/API/Window/prompt

- confirm
https://developer.mozilla.org/zh-CN/docs/Web/API/Window/confirm

#### 列表类

- ListBox（无）
- DropDown
```
<select>
  <option value="volvo">Volvo</option>
  <option value="saab">Saab</option>
  <option value="opel">Opel</option>
  <option value="audi">Audi</option>
</select> 
```

https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select

```
<datalist>
```

http://www.runoob.com/tags/tag-datalist.html
- Combox（无）

#### 时间日期类

- 时间框
```
<input id="time" type="time">
```
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/time

- 年月框
```
<input id="month" type="month">
```
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/month

- 日期框
```
<input type="date">
```
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date

- 时间日期框
```
<input type="datetime-local">
```
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/datetime-local


- 星期框
```
<input id="week" type="week">
```
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/week

#### 其他

##### 标签

##### 滑杆

```
<input type="range">
```

https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/range

##### 进度条

##### 颜色框

```
<input type="color">
```
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/color

##### 表单容器

##### 文件上传

```
<input name="myFile" type="file">
```
https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file

### 控件三要素

#### 属性

#### 方法

#### 事件

### UI 代码风格 1

#### JQuery 代码风格

#### 原生 API 代码风格

### UI 代码风格 2

#### 代码分离

#### 代码不分离

### 案例演示

## 5. 数据合法性校验

### 什么是数据合法性校验

### 校验内容

### 校验流程

### 校验意义

### 校验方案

#### 校验方式，分类一

按校验执行的位置分类：

- 客户端校验
- 服务器端校验


#### 校验方式，分类二

按校验的颗粒度分类：

- 表单级校验
- 字段级校验
- 字符级校验

#### 校验方式，分类三

按校验代码的编写人分类：

- 自己验证
- H5 验证
- 混合验证


### 如何实现

#### 表单级

#### 字段级

#### 字符级

#### H5 校验

#### 混合校验

### 技术细节

- 事件
  - submit 事件，集中校验
  - focusout 事件，字段校验
  - keypress 事件，字符检验
- 正则表达式
- 焦点和 Tab 键顺序
- H5 校验技术
  - 语义化标签
  - 验证属性
  - 伪类
  - validity API
  - setCustomeValidity API


## 6. 第三方组件

### 第三方组件库

- JQuery UI
- jQuery Mobile UI
- jQuery EasyUI
- LayUI
- WeUI
- YUI


### 常用第三方组件

#### 图表组件

#### 地图组件

#### 语法高亮

#### 集成开发环境

#### 表格组件

#### 公式组件

#### 整页轮播组件

## 7. 自定义 UI 组件

### 组件化的背景

### 组件化的思路

### 组件化的思想

### 组件化的优势

#### 便于重用，提高开发效率

#### 利于并行开发，提高开发效率

#### 降低问题的规模和复杂度

#### 便于代码维护，形成隔离带

### 组件分类

#### 分类方式一

按组件是否需要指定容器分类

##### 指定容器组件

##### 不指定容器组件

#### 分类方式二

按组件的生命周期分类

##### 长期组件

##### 临时组件

#### 分类方式三

按zu'jian是否绘制 DOM 分类

##### 自绘制 DOM 组件

##### 不绘制 DOM 组件

#### 分类方式四

安装组件是否依赖其他库fen'lei

##### 独立组件

##### 非独立组件

### 组件化技术细节

#### 组件封装

- JavaScript 代码封装
- CSS 代码封装


#### 组件绘制

- 模板字符串生成
- 操作 DOM 节点生成

#### 组件样式

- 外部样式表，可以人为修改样式表
- 动态设置样式，可以把样式参数化

#### 组件参数化

组件的输入/输出

- 输入
  - 初始化
     - 父容器
     - 参数
     - 样式
  -用户输入
- 输出
  - 事件机制
  - 回调函数，初始化注入
  - 数据绑定


#### 组件事件绑定

#### 组件实例化

#### 组件生命期

生命期各阶段：
- 创建
- 活动
- 销毁

组件寿命：
- 永久的，与应用生命期等长
- 临时的，短与应用生命期

#### CSS 模块化

#### require.js

## 8. SPA & MVC

### 多页

多页之间数据共享方式

- 扩文档通信
- 客户端存储技术
  - cookie
  - local storage
  - 等

#### 多页跳转

#### 多页嵌套

### 单页

Shell 外壳的写法

### 前后端分离

两者比较：
- 前后端分离的单页或多页
- 后台渲染的多页

### 前端路由

### MVC 是什么？

### MVP 是什么？

### 如何实现 MVC？

### jsnotepad 分析

## 9. 数据存储

### 解决问题

#### 状态保持

#### 数据持久化

### 存储分类

#### 服务器端存储

#### 客户端存储

### 客户端存储方式

#### cookies

cookies
	H5 之前的存储方式
	Cookies 的问题


#### local storage

#### session storage

#### Application Cache

#### indexDB

### 服务端存储方式

- cache
- 内存
- 磁盘文件
- 数据库


## 10. 综合案例实战

### rectangle

### jsnotepad

### adim
