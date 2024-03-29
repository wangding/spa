# 第 4 章：数据合法性校验

## 阅读参考资料

- [表单验证](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Forms/Data_form_validation)

## 表单级校验

要求：

- 在 spa 仓库创建 05-form-validation 目录
- 复制 rectangle 仓库 v0.5 版本的代码
- 做以下几个方面的校验：
  - 数据不能为空
  - 数据类型不对，数据不能是字符串，而应该是数字
  - 数据的取值范围错误，宽度和高度都应该大于零
- Tab 键进行焦点切换时不进行数据合法性验证
- 键盘输入字符时不对非法字符进行判断，不拦截非法字符
- 只有点击计算按钮时才进行数据合法性校验
- 出现验证错误时，只报告第一个验证的错误
- 只有数据验证都通过之后，才计算矩形的周长和面积

参考示例：

- [表单级验证](http://fe.wangding.co/02-validation/02-form-validation.html)

## 矩形计算器 v1.0

要求：

- 进一步完善 rectangle 仓库代码
- 对矩形的宽度和高度两个字段进行字段级数据合法性校验
- 数据合法性校验的方面跟表单级验证相同
- 对非法数据提供清晰明确的错误提示
- 初始焦点在宽度文本框上，按 Tab 键时，进行数据合法性校验
- 如果数据不合法，Tab 键不移动到下一个文本框
- 如果宽度和高度是错误的（上面三种错误的任意一种），点击计算按钮（可以点击多次），不应该计算出周长和面积
- 对数据合法性校验模块增加单元测试

示例参考：

- [矩形计算器 v1.0 字段级校验](https://bitbucket.org/wngding/rectangle/commits/d7c4afa37b7a3445bdab8fc1b9f17040c9108b6e)

## 矩形计算器 v1.1

要求：

- 进一步完善 rectangle 仓库代码
- 在字段级验证的基础上添加字符级验证
- 合法的字符包括：0~9 十个数字、小数点、负号和科学计数法的 e 和 E
- 非法字符，除了上面合法字符以外的字母和标点符号
- 在矩形的宽度和高度输入框中输入非法字符，非法字符不会出现在文本框中
- 对字符过滤模块增加单元测试

参考示例：
- [矩形计算器 v1.1 字符级校验](https://bitbucket.org/wngding/rectangle/commits/d4d2fc41d15d77da3243621f947834b9dbce157f)


## H5 校验

要求：

- 在 spa 仓库创建 06-h5-validation 目录
- 复制 rectangle 仓库 v1.0 版本的代码
- 利用 H5 内置控件提供的数据合法性校验功能
- 实现字段级和字符级数据合法性校验
- 通往 H5 验证的伪类来提供数据验证与否的标记

参考示例：

- [H5 校验](http://fe.wangding.co/02-validation/03-h5-validation.html)
