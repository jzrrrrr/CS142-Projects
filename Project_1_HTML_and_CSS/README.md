# CS142 Project 1: HTML and CSS

## Problem 1 (20 points)

创建一个 HTML 文档，该文档呈现两种不同的外观，由文档的 CSS 样式表决定。

- 您的 HTML 文件应命名为 `index.html`；
- 文档的标题应为 `CS142 Project 1`；
- 您还应该创建两个样式表，分别命名为 `styleA.css` 和 `styleB.css`。

如果 HTML 文件链接到 `styleA.css` ，则它应该看起来像这样（版本 A）：

![Version A](project1versionA.png)

如果 HTML 文件链接到 `styleB.css` ，则应呈现如下（版本 B）：

![Version B](project1versionB.png)

> **备注：上面的截图中的 D 被突出显示以显示文本应占用的空间。您的解决方案不应使用蓝色背景来样式化 D。**

### 样式 A 规范：

- 应该有六个盒子元素，垂直排列；
- 所有盒子水平居中且垂直等距。当浏览器窗口调整大小时，盒子之间的间距应改变（它们应垂直等距地分布在页面上）。然而，盒子本身不应重叠或改变大小；
- 每个盒子为 100x100 像素，顶部有 1 像素的线（颜色：#687291）。文本水平居中；
- 盒子颜色交替（颜色：#dfe1e7，#eeeff2）；
- 最后一个元素（颜色：#687291）具有 4 像素的黑色边框，文本垂直居中；
- 所有元素中的字体为 Tahoma，字重 40 pixels.

### 样式 B 规范

- 五个盒子元素，水平排列在左上角；
- 盒子不会随着窗口大小的调整而换行（即盒子 A 到 E 应保持在同一行，即使浏览器窗口太小无法显示它们全部）；
- 最后一个盒子定位在窗口的右下角，即使窗口调整大小也会保持在那个位置；
- 每个盒子大小为 100x150 像素（颜色：#eeeff2），左侧有 10 像素的虚线（颜色：#D0D0FF）。盒子之间间隔 10 像素。
- 鼠标悬停在盒子上时，光标变为手形，盒子及字体颜色变为黄色和金色；
- 所有元素中的字体为 Tahoma，字重 40 pixels；
- 字母与框边缘之间有 10 像素的空间。

如果某个属性在这些规范中没有明确说明（例如，样式 B 中元素与窗口边缘之间的空间），则应选择一个合理的值。

## Style Points (5 points)

您的 HTML 文件必须是一个有效的 XHTML 1.0 文档，且通过 http://validator.w3.org 的验证。此外，您的 HTML 和 CSS 必须整洁、可读、正确缩进且结构良好。

## Extra Credit (2 points)

创建一个第三种样式表 styleC.css ，该样式表利用以下几项中的 2 项：

- gradients  渐变
- transitions  过渡
- animations  动画
- web fonts  网页字体
- shadows  阴影

## Resources

使用 Chrome 浏览器完成此项目，以及本课程的所有项目。这将消除浏览器兼容性问题。

为了提交作业，您需要具备基本的 Unix 知识。[点击此处](https://web.stanford.edu/class/archive/cs/cs107/cs107.1194/resources/)了解浏览和操作 UNIX 文件系统的简介。

您**不得**使用任何 JavaScript 或外部库/样式表。您必须编写自己的代码。

## Hints

- 你可能会发现以下 CSS 样式属性对本次项目很有用（请去搜索具体使用细节的文档吧～）：

```css
display: inline-block;
height: 100%;
white-space: nowrap;
```

- 你至少需要在本作业的一个部分使用 [CSS Flexbox layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout)。

## Deliverables

使用 standard class [submission mechanism](https://web.stanford.edu/class/cs142/submit.html) 提交所有用于问题 1 的文件，包括 `index.html` 、 `styleA.css` 、 `styleB.css` 以及（可选） `styleC.css` 。

> Designed by Raymond Luong for CS142 at Stanford University