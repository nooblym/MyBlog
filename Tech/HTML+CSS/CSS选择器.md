# CSS笔记

## CSS选择器

### 基本选择器

- [通用选择器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Universal_selectors)（[Universal selector](https://wiki.developer.mozilla.org/en-US/docs/Web/CSS/Universal_selectors)）

  选择所有元素。（可选）可以将其限制为特定的名称空间或所有名称空间。 **语法：**`*` `ns|*` `*|*` 

  **例子：**`*` 将匹配文档的所有元素

- [元素选择器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Type_selectors)（[Type selector](https://wiki.developer.mozilla.org/en-US/docs/Web/CSS/Type_selectors)）

  按照给定的节点名称，选择所有匹配的元素。 **语法：**`elementname` 

  **例子：**`input` 匹配任何 [`<input>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/input) 元素

- [类选择器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Class_selectors)（[Class selector](https://wiki.developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors)）

  按照给定的 `class` 属性的值，选择所有匹配的元素。 **语法**：`.classname` 

  **例子**：`.index` 匹配任何 `class` 属性中含有 "index" 类的元素

- [ID 选择器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/ID_selectors)（[ID selector](https://wiki.developer.mozilla.org/en-US/docs/Web/CSS/ID_selectors)）

  按照 `id` 属性选择一个与之匹配的元素。需要注意的是，一个文档中，每个 ID 属性都应当是唯一的。 **语法：**`#idname` 

  **例子：**`#toc` 匹配 ID 为 "toc" 的元素

- [属性选择器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Attribute_selectors)（[Attribute selector](https://wiki.developer.mozilla.org/en-US/docs/Web/CSS/Attribute_selectors)）

  按照给定的属性，选择所有匹配的元素。 **语法：**`[attr]` `[attr=value]` `[attr~=value]` `[attr|=value]` `[attr^=value]` `[attr$=value]` `[attr*=value]` 

  **例子：**`[autoplay]` 选择所有具有 `autoplay` 属性的元素（不论这个属性的值是什么）

### 分组选择器

- [选择器列表](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Selector_list)（[Selector list](https://wiki.developer.mozilla.org/en-US/docs/Web/CSS/Selector_list)）

  `,` 是将不同的选择器组合在一起的方法，它选择所有能被列表中的任意一个选择器选中的节点。 **语法**：`A, B` 

  **示例**：`div, span` 会同时匹配 [`<span>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/span) 元素和 [`<div>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div) 元素。

### 组合器（Combinators）

- [后代组合器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Descendant_selectors)（[Descendant combinator](https://wiki.developer.mozilla.org/en-US/docs/Web/CSS/Descendant_combinator)）

  （空格）组合器选择前一个元素的后代节点。 **语法：**`A B` 

  **例子：**`div span` 匹配所有位于任意 [`<div>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div) 元素之内的 [`<span>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/span) 元素

- [直接子代组合器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Child_selectors)（[Child combinator](https://wiki.developer.mozilla.org/en-US/docs/Web/CSS/Child_combinator)）

  `>` 组合器选择前一个元素的直接子代的节点。 **语法**：`A > B` 

  **例子**：`ul > li` 匹配直接嵌套在 [`<ul>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/ul) 元素内的所有 [`<li>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/li) 元素。

- [一般兄弟组合器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/General_sibling_selectors)（[General sibling combinator](https://wiki.developer.mozilla.org/en-US/docs/Web/CSS/General_sibling_combinator)）

  `~` 组合器选择兄弟元素，也就是说，后一个节点在前一个节点后面的任意位置，并且共享同一个父节点。 **语法**：`A ~ B` 

  **例子**：`p ~ span` 匹配同一父元素下，[`<p>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/p) 元素后的所有 [`<span>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/span) 元素。

- [紧邻兄弟组合器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Adjacent_sibling_selectors)（[Adjacent sibling combinator](https://wiki.developer.mozilla.org/en-US/docs/Web/CSS/Adjacent_sibling_combinator)）

  `+` 组合器选择相邻元素，即后一个元素紧跟在前一个之后，并且共享同一个父节点。 **语法：**`A + B` 

  **例子：**`h2 + p` 会匹配所有紧邻在 [`<h2>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/h2) 元素后的 [`<p>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/p) 元素。

- [列组合器](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Column_combinator)（[Column combinator](https://developer.mozilla.org/en-US/docs/Web/CSS/Column_combinator)）

  `||` 组合器选择属于某个表格行的节点。 **语法：** `A || B` 

  **例子：** `col || td` 会匹配所有  [`<col>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/col)作用域内的 [`<td>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/td) 元素。

### 伪选择器（Pseudo）

- [伪类](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-classes)

  `:` 伪选择器支持按照未被包含在文档树中的状态信息来选择元素。 

  **例子：**`a:visited` 匹配所有曾被访问过的 [`<a>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a) 元素。

- [伪元素](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-elements)

  `::` 伪选择器用于表示无法用 HTML 语义表达的实体。 

  **例子：**`p::first-line` 匹配所有 [`<p>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/p) 元素的第一行

### 紧邻选择器

> 紧邻选择器是指通过组合普通的基本选择器来形成“且”的逻辑关系来更加准确的选择元素

- 标签带类选择器

  标签带类选择器选择指定标签且class属性含有指定值的节点，**语法：** `element.classvalue`

   **例子：** `div.header` 会匹配所有  [`<div>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/div)标签且class属性有header的元素

- 多类选择器

  多类选择器选择class属性含多个指定值的节点，**语法：** `.classvalue1.classvalue2`

   **例子：** `.header.container` 会匹配所有class属性同时含有header和container值的元素

- ...

### Tips

1. 选择器优先级

   !important>行内样式>ID选择器>类选择器>标签选择器>通配符选择器>浏览器默认样式

### Q&A

1. 多个选择器都可以选择同一个元素时应该选择哪一个选择器？

2. 如何选择class和id应不应该添加？

   class和id应该是作为一个模块来帮助css更好的定位元素，从class和id的特性可以看出，当有一个不会重复的大模块应该使用id选择器，而会重复出现的小模块或局部模块可以使用添加class属性

3. 如何避免class泛滥

   > 问题描述：“避免Web开发专家Jeffrey Zeldman说的“类泛滥——标记中的麻疹”出现。什么意思呢？就是说你不要像使用ID一样，每个类都指定一个不同的类名，然后再为每个类编写规则。如果你确实有这种随意使用类的习惯，那说明你可能像大多数对CSS充满激情的初学者一样，还不了解继承和上下文选择符的作用。于是，你可能会给每个标签都重复写同样的样式（比如为页面中很多标签分别指定相同的字体）。实际上，继承和上下文选择符能让不同的标签共享样式，从而降低你需要编写和维护的CSS量。”
