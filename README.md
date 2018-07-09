---
description: >-
  欢迎使用前端代码规范，使用过程中如碰到问题，请到 Github(https://github.com/vitorlee/documents/issues)
  进行提问。
---

# 前端代码规范

## 概述

本前端代码规范是由 [三体云动](https://www.styd.cn/) ⬀ 前端团队整理的，基于 [W3C](http://www.w3.org/) ⬀、[Google开发者](https://developers.google.com/style/) ⬀ 等官方文档，并结合团队日常业务需求以及团队在日常开发过程中总结提炼出的经验而制定。

★ 核心目标：

1. 增强团队开发协作、提高代码质量、可读性和维护性
2. 表现、内容和行为的分离
3. 标记结构良好、语义正确、普遍合法

以下规范是团队基本约定的内容，必须严格遵循。

[文件命名规范](./#wen-jian-ming-ming-gui-fan)

从 `图片`、`HTML/CSS文件`、`脚本文件` 的命名等层面约定规范团队的命名习惯，增强团队代码的可读性。

[图片规范](./#tu-pian-gui-fan)

了解各种图片格式特性，根据特性制定图片规范，旨在从图片层面优化页面性能。

[HTML 规范](./#html-gui-fan)

使 HTML 代码风格保持一致，容易被理解和被维护。

[CSS 规范](./#css-gui-fan)

统一规范团队 CSS 代码书写风格和使用 CSS 预编译语言语法风格，提供常用媒体查询语句和浏览器私有属性引用，并从业务层面统一规范常用模块的引用。

[JavaScript 规范](./#javascript-gui-fan)

统一团队的 JS 语法风格和书写习惯，减少程序出错的概率，其中也包含了 ES6 的语法规范和最佳实践。

## 文件命名规范

★ 核心目标：

1. 统一文件名称
2. 优化目录结构

因个人习惯引起的文件命名不统一，增加不同成员维护项目成本。所有命名类规范基本参照 [BEM](https://en.bem.info/methodology/quick-start/) ⬀方法，连字符或大小写等各有要求，请详细阅读。

### 图片文件

图片命名建议按照以下顺序命名，**中间用 "\_" 下划线连接**：

**图片功能类别\(必选\) + 图片模块名称\(必选\) + 辅助修饰名称\(可选\)**

* 图片功能类别：
  * mod\_\*：是否公共，可选
  * icon\_\*：图标
  * logo\_\*：LOGO类
  * spr\_\*：雪碧图
  * btn\_\*：按钮类
  * bg\_\*：背景类
* 图片模块名称
  * courselist：课程列表
  * courseinfo：课程信息
  * useravatar：用户头像
* 辅助修饰名称：
  * 高清图：2x \| 3x
  * 固定尺寸（宽 x 高）：200x100
  * 序号：1 \| 2 \| 3 \| ∞

⚑ 例：

```text
公共模块：
mod_btn_courselist.png
mod_icon_useravatar_2x.png
mod_bg_courseinfo_200x200.png

非公共模块：
btn_courselist.png
icon_useravatar_2x.png
bg_courseinfo_200x200.png
```

### HTML 文件

包括所有视图文件。

**文件命名总是以字母开头而不是数字，且字母一律小写，以下划线连接且不带其他标点符号**

⚑例：

```text
视图文件:
index.html
product_info.tpl
app.vue
```

### CSS / LESS 文件

CSS命名规范请参照 [HTML文件](./#html-wen-jian)，LESS稍有不同。

在LESS文件中，**库文件和无需编译生成的文件，在开头用下划线标记**。

⚑例：

```text
css:
index.css
main.css

less:
_button.less
_typography.less
index.less
```

### 脚本文件

按以下顺序，类型用 “.” 连接，名称用 “\_” 下划线连接。

**库类型\(可选\) + 功能名称\(必选\) + 打包状态\(可选\) + 压缩类别\(可选\) + 修饰\(可选\)**

* 库类型：
  * jquery.\*
  * mootools.\*
  * dojo.\*
* 功能名称：
  * album.\*
  * album\_list.\*
* 打包状态：
  * full.\*
  * package.\*
  * bundle.\*
  * all.\*
* 压缩类别：
  * min.\*
* 修饰：
  * \*.map

⚑例：

```text
脚本文件：
jquery.lightbox.js
jquery.lightbox.min.js
plupload.full.min.js
bootstrap.min.js.map
album_list.js
```

## 图片规范

★ 核心目标：

1. 规范图片格式
2. 优化图片质量
3. 减少加载耗时

### 格式

常见的图片格式有 GIF、PNG8、PNG24、JPEG、WEBP、SVG，根据图片格式的特性和场景需要选取适合的图片格式。

* 颜色丰富图片，且有透明通道，优先推荐使用 PNG 格式
* 动图和颜色单一，推荐使用 GIF 格式
* UGC - 用户行为产生的图片，如用户上传的内容，推荐使用 JPEG 格式
* 颜色唯一的icon，推荐使用 `webfont`，详细见 [字体规范](./#zi-ti-gui-fan)

为减少 HTTP 请求，而衍生出的 Css Sprites 和 Base64 技术，建议按照以下方式处理：

**Css Sprites 说明：**

* 适合使用频率高、更新频率低、颜色丰富的小图标
* 尽量不留太多的空白
* 体积较大的图片不合并
* 确保要合并的小图坐标数值和合并后的 Sprites 图尺寸均为偶数

**Base64 说明：**

* 适合更新频率高的小图片，如某些具备自定义功能的标题icon等
* 转换成 Base64 编码的图片应小于 2KB
* **移动端不使用 Base64 编码**

### 大小

网站响应时间中，图片资源消耗占据 ≥30%，图片大小需受到严格控制。

**所有图片必须经过一定的压缩和优化才能发布**

* PNG 图片使用 [Tinypng](https://tinypng.com/) ⬀ 压缩
* JPEG 导出前选择质量范围在 60 ~ 75

PC 端单张图片不能 ＞300kb

移动端单张图片不能 ＞100kb

### 尺寸

**所有图片尺寸必须为偶数**。如：100x50，400x400，122x58。

可以使用 [七牛图片API](https://developer.qiniu.com/dora/manual/3683/img-directions-for-use) ⬀ 功能对用户上传图片进行裁剪显示，裁剪结果也必须为**偶数**。

⚑例：

```text
原始图片：
https://pic3-s.styd.cn/o_1b4iam0mh54bvrn1qcgsa5gr67.jpg

裁剪后图片：
https://pic3-s.styd.cn/o_1b4iam0mh54bvrn1qcgsa5gr67.jpg?imageView2/1/w/200/h/200/
```

### 引入方式

测试内容图应该标明图片尺寸，[在线生成占位图](https://dn-placeholder.qbox.me/) ⬀。

⚑例：

```text
https://dn-placeholder.qbox.me/300x200
```

![](.gitbook/assets/300x200.bin)

## HTML 规范

### 代码规范

★ 核心目标：

1. 遵循 HTML 标准和语义
2. 减少标签数量和嵌套
3. 代码风格保持一致
4. 提高效率及协同开发的便捷性

#### 缩进

用两个空格来代替 tab

```markup
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <h1>这个DEMO</h1>  
</body>
</html>
```

#### doctype

为每个 HTML 页面的第一行添加标准模式（standard mode）的声明，这样能够确保在每个浏览器中拥有一致的展现。统一使用 HTML5 的文档声明：

```markup
<!DOCTYPE html>
```

#### 字符编码

以 UTF-8 无 BOM 编码作为文件格式，BOM 介绍请参考 [「附录 - 文档 - 第 2 条 」](./#wen-dang)

```markup
<meta charset="UTF-8">
```

#### IE 兼容模式

IE 支持通过特定的 `<meta>` 标签来确定绘制当前页面所应该采用的 IE 版本。除非有强烈的特殊需求，否则最好是设置为 **edge mode**，从而通知 IE 采用其所支持的最新的模式。

```markup
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

#### 语言属性

根据 HTML5 规范：

> 强烈建议为 html 根元素指定 lang 属性，从而为文档设置正确的语言。这将有助于语音合成工具确定其所应该采用的发音，有助于翻译工具确定其翻译时所应遵守的规则等等。

更多关于 `lang` 属性的知识可以从 [此规范](https://www.w3.org/International/articles/language-tags/) ⬀ 中了解。

```markup
<html lang="zh-CN">
```

#### 引入文件

不需要为 CSS、JS 指定类型属性，HTML5 中默认已包含

```markup
<!-- 推荐 -->
<link rel="stylesheet" href="" >
<script src=""></script>

<!-- 不推荐 -->
<link rel="stylesheet" type="text/css" href="" >
<script type="text/javascript" src="" ></script>
```

#### 布尔型属性

布尔（boolean）型属性可以在声明时**不赋值**。XHTML 规范要求为其赋值，但是 HTML5 规范不需要。

> 元素的布尔型属性如果有值，就是 true，如果没有值，就是 false。

```markup
<input type="text" disabled>
<input type="checkbox" value="1" checked>
<select>
  <option value="1" selected>1</option>
</select>
```

#### 小写

HTML标签名、类名、标签属性和大部分属性值统一用小写

```markup
<!-- 推荐 -->
<div class="demo"></div>

<!-- 不推荐 -->
<div class="DEMO"></div>
<DIV CLASS="DEMO"></DIV>
```

#### 属性引号

对于属性的定义，全部使用双引号，绝不用单引号或无引号。

```markup
<!-- 推荐 -->
<div class="demo"></div>

<!-- 不推荐 -->
<div class='demo'></div>
<div class=demo></div>
```

#### 嵌套 & 闭合

遵循 HTML 标准和语义，使用最少的标签提高可读性。

* 块级元素应缩进
* 行内元素嵌套根据内容选择性缩进，以长度不超过编辑器一屏为宜
* 不要在 [空元素](https://www.w3.org/TR/html5/syntax.html#void-elements) ⬀ 的尾部添加 `/` 
* 所有具有开始标签和结束标签的元素都要写上起止标签
* 不推荐行内元素包含块级元素

```markup
<!-- 推荐 -->
<div>
  <h1>我是h1标题</h1>
  <p>我是一段文字，我有始有终，<b>浏览器</b>能正确解析</p>
</div>
<br>

<!-- 不推荐 -->
<div>
  <span>
    <h1>我是h1标题</h1>
  </span>
  <p>
    我是一段文字，我有始有终，
    <b>
      浏览器
    </b>
    能正确解析
  </p>
</div>
<br/>
```

#### 多媒体替代方案

* 为 `img` 元素加上 `alt` 属性
* 为视频内容提供音轨替代
* 为音频内容提供字母替代

```markup
<!-- 推荐 -->
<img src="banner.jpg" alt="三体商学院 - 做更有品质的健身行业培训与教育" />

<!-- 不推荐 -->
<img src="banner.jpg" />
```

### 注释规范

详细的注释能区分业务功能、帮助团队成员快速了解代码，增强可维护性。

* 简单的描述，如某些状态描述、属性描述等
* 注释内容前后各一个空格字符，注释位于要注释代码的上面，单独占一行

#### 单行类型注释

```markup
<!-- Comment Text -->
<div>...</div>
```

#### 模块类型注释

对多行和大功能模块，使用双注释标注，`<!-- 注释 -->` 和 `<!-- /注释 -->`

```markup
<!-- Comment Text -->
<div>
  ...
</div>
<!-- /Comment Text -->
```

#### 区域类型注释

用于功能取消或代码下线注释

```markup
<!-- Comment Text
<div>
  ...
</div>
-->
```

#### 提示类型注释

提醒开发成员注意的区域，一般包含 3 类型：

1. 需持续开发：TODO
2. 需特别说明：NOTE
3. 需修复错误：FIXME

```markup
<!-- TODO：Comment Text -->
<div>...</div>

<!-- NOTE：Comment Text -->
<div>...</div>

<!-- FIXME：Comment Text -->
<div>...</div>
```

### 文件模板

{% code-tabs %}
{% code-tabs-item title="PC端" %}
```markup
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="keywords" content="keywords1,keywords2">
  <meta name="description" content="your description">
  <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
  <link rel="icon" href="favicon.ico">
  <title>PC端模版</title>
</head>
<body>
  ...
</body>
</html>
```
{% endcode-tabs-item %}

{% code-tabs-item title="移动端" %}
```markup
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no, viewport-fit=cover">
  <meta name="format-detection" content="telephone=no" searchtype="map">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black">
  <link rel="icon" href="favicon.ico">
  <title>移动端模版</title>
</head>
<body>
  ...
</body>
</html>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## CSS 规范

★ 核心目标：

1. 代码风格保持一致
2. 易于理解和维护
3. 遵循 CSS 设计，其它预处理器（LESS，SASS等）尽量统一

### 代码规范

#### 编码

使用无 BOM 的 UTF-8 编码

#### 缩进

使用 2 个空格代替制表符（Tab）

#### 冒号

每条声明语句的 `:` 后应该插入一个空格

#### 分号

所有声明语句都应当以分号 `;` 结尾，包括最后一条。

#### 风格

* 使用展开（Expanded）格式
* 样式选择器，属性名必须用小写
* 每个声明块的左花括号 `{` 左侧有空格，并于选择器同行
* 声明块的右花括号 `}` 应当单独成行

⚑ 例：

```css
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
}
```

#### 简写形式

对于属性值或颜色参数，省略小于 1 的小数前面的 0。

```css
.selector {
  background-color: rgba(0,0,0,.5);
}
```

使用简写形式的十六进制值

```css
.selector {
  background-color: #fff;
}
```

避免为 0 值指定单位

```css
.selector {
  padding: 0 10px;
}
```

### 命名规范

* 采用 **模块名称 + 功能名称 + 修饰名** 方式
* 使用小写字母，以下划线 `_` 分隔
* 名称应当尽可能短，并且意义明确
* **禁止** 单独使用 hook 等钩子类标识行为，造成 className 占用

### Hack & 兼容规范

* 尽量减少对Hack的使用和依赖
* 兼容需按照版本从旧到新的原则
* 两者都需有清晰注释

⚑ 例：

```css
.hack {
　　　color: #000;       /* For all */
　　　*color: #666;      /* For IE7 and earlier */
　　　_color: #777;      /* For IE6 and earlier */
}

.compatibility {
    display: box;              /* OLD - Android 4.4- */
    display: -webkit-box;      /* OLD - iOS 6-, Safari 3.1-6 */
    display: -moz-box;         /* OLD - Firefox 19- (buggy but mostly works) */
    display: -ms-flexbox;      /* TWEENER - IE 10 */
    display: -webkit-flex;     /* NEW - Chrome */
    display: flex;             /* NEW, Spec - Opera 12.1, Firefox 20+ */
}
```

### 选择器

避免使用类型选择器，CSS 选择器是从右至左解析

```css
/* 不推荐 */
div#element { 
  width: 100px;
}

/* 推荐 */
#element { 
  width: 100px;
}
```

避免多 id 嵌套

```css
/* 不推荐 */
#block #element { 
  width: 100px;
}

/* 推荐 */
#element { 
  width: 100px;
}
```

### 注释规范

#### 普通注释

单行或功能模块说明注释，可以使用 `/**/` 或 `//`

```css
/* Comment Text */
// Comment Text
```

#### 区块注释

区块或文档注释方法：

```css
/**
 * Comment Text
 */
```

### LESS 规范

#### 组织顺序

1. @import
2. 变量声明
3. 样式声明

⚑ 例：

```css
@import "mixins/size.less"; /* .less 后缀不得省略 */

@default_color: #333;

.selector {
  width: 960px;
  color: @default_color;
}
```

#### 运算

`+`  `-`  `*`  `/` 四个运算符两侧**必须**保留一个空格。`+`  `-` 两侧的操作数**必须**有相同的单位，如果其中一个是变量，另一个数值**必须**书写单位。

```css
/* 不推荐 */
@a: 200px;
@b: (@a+100)*2;

/* 推荐 */
@a: 200px;
@b: (@a + 100px) * 2;
```

#### 变量

* 变量根据逻辑进行分组列出
* 使用驼峰式命名变量 `@blockElement`

```css
@colorBorder: #f5f5f5;
@staticVersion: "?ver=1510712523";
```

#### 继承（Extend）

使用继承时，如果在声明块内书写 `:extend` 语句，必须写在开头：

⚑ 例：

```css
/* 不推荐 */
.selector {
  color: red;
  &:extend(.mod all);
}

/* 推荐 */
.selector {
  &:extend(.mod all);
  color: red;
}
```

#### 混入（Mixins）

1. 在定义 `mixin` 时，如果 `mixin` 名称不是一个需要使用的 className，必须加上括号，否则即使不被调用也会输出到 CSS 中。
2. 如果混入的是本身不输出内容的 mixin，需要在 mixin 后添加括号（即使不传参数），以区分这是否是一个 className。

⚑ 例：

```css
.selector() {
  font-size: 2em;
}

h3 {
  .selector(); 
}
```

#### 嵌套

* 将嵌套深度限制在 2 级。对于超过 3 级的嵌套，给予重新评估。
* 避免大量的嵌套规则。当可读性受到影响时，将之打断。推荐避免出现多于20行的嵌套规则出现。

## JavaScript 规范

★ 核心目标：

## 字体规范

★ 核心目标：

## 附录

### 参考

* [支付宝 - 移动 Web 开发经验](http://am-team.github.io/amg/dev-exp-doc.html) ⬀
* [腾讯 Web 前端团队规范](http://alloyteam.github.io/CodeGuide/) ⬀

### 工具

1. 在线代码编辑器：[CodePen](https://codepen.io/) ⬀
2. 在线图表编辑器：[Diagram](https://www.draw.io/) ⬀
3. Unicode查询：[Unicode table](https://unicode-table.com/en/) ⬀
4. 在线正则校验：[Regex](https://regex101.com/) ⬀
5. json美化：[JSON formater ](https://jsonformatter.org/) ⬀
6. 浏览器兼容语法检查：[Can I use](https://caniuse.com/) ⬀
7. css 在线生成工具：[Mastering the :nth-child](http://nthmaster.com/) ⬀ 、[CSS 三角生成](http://lugolabs.com/caret) ⬀ 、[CSS 渐变生成器](https://cssgradient.io/) ⬀

### 文档

1. HTML 中 `meta` 属性：[常见的 HTML 头部标签](https://github.com/yisibl/blog/issues/1) ⬀
2. BOM 参考： [BOM的介绍](https://zh.wikipedia.org/wiki/位元組順序記號) ⬀ 、 [「带 BOM 的 UTF-8」和「无 BOM 的 UTF-8」有什么区别？](http://www.zhihu.com/question/20167122) ⬀

