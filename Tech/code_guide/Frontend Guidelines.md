# Frontend Guidelines

## HTML

### 语义化使用标签

1. HTML5为我们提供了大量的语义元素，旨在精确描述内容。确保你能从它丰富的词汇中获益。

   ```html
   <!-- bad -->
   <div id=main>
     <div class=article>
       <div class=header>
         <h1>Blog post</h1>
         <p>Published: <span>21st Feb, 2015</span></p>
       </div>
       <p>…</p>
     </div>
   </div>
   
   <!-- good -->
   <main>
     <article>
       <header>
         <h1>Blog post</h1>
         <p>Published: <time datetime=2015-02-21>21st Feb, 2015</time></p>
       </header>
       <p>…</p>
     </article>
   </main>
   ```

2. 确保你理解你所使用的元素的语义。以错误的方式使用一个语义元素比保持中立更糟糕。

   ```html
   <!-- bad -->
   <h1>
     <figure>
       <img alt=Company src=logo.png>
     </figure>
   </h1>
   
   <!-- good -->
   <h1>
     <img alt=Company src=logo.png>
   </h1>
   ```

   #### 有用的链接

   [Semantics（语义） - 术语表 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Glossary/Semantics#html_中的语义)

   ### html应尽量保持简洁

   1. 保持你的代码简洁。忘记你以前的XHTML习惯。

      ```html
      <!-- bad -->
      <!doctype html>
      <html lang=en>
        <head>
          <meta http-equiv=Content-Type content="text/html; charset=utf-8" />
          <title>Contact</title>
          <link rel=stylesheet href=style.css type=text/css />
        </head>
        <body>
          <h1>Contact me</h1>
          <label>
            Email address:
            <input type=email placeholder=you@email.com required=required />
          </label>
          <script src=main.js type=text/javascript></script>
        </body>
      </html>
      
      <!-- good -->
      <!doctype html>
      <html lang=en>
        <meta charset=utf-8>
        <title>Contact</title>
        <link rel=stylesheet href=style.css>
      
        <h1>Contact me</h1>
        <label>
          Email address:
          <input type=email placeholder=you@email.com required>
        </label>
        <script src=main.js></script>
      </html>
      ```

   ### 尽可以改善站点的易用性

   易用性不应该是一个事后的想法。你不需要成为WCAG(Web内容无障碍指南)专家来改善你的网站，你可以立即开始修复那些会产生巨大变化的小东西，例如：

   + 尝试使用`alt`属性

     *alt* 属性用来为图像定义一串预备的可替换的文本

   + 不仅仅依靠颜色传递信息

   + 准确使用表单

   ```html
   <!-- bad -->
   <h1><img alt=Logo src=logo.png></h1>
   
   <!-- good -->
   <h1><img alt=Company src=logo.png></h1>
   ```

### 声明语言和字符编码

虽然定义语言是可选的，但建议总是在根元素上声明它。

HTML标准要求页面使用UTF-8字符编码且必须被声明，虽然它可以在HTTP头中Content-Type 声明，但强烈建议在文档级别声明它。

```html
<!-- bad -->
<!doctype html>
<title>Hello, world.</title>

<!-- good -->
<!doctype html>
<html lang=en>
  <meta charset=utf-8>
  <title>Hello, world.</title>
</html>
```

### 性能

1. 没有特殊情况不要把script放在html body之前，那样会阻塞页面渲染
2. 如果样式很多很复杂，应把一部分必要的分离出来先加载，延迟加载另一部分比较重的样式；尽管两个HTTP请求明显比一个请求慢，但先给用户一个能看的页面是必要的

```html
<!-- bad -->
<!doctype html>
<meta charset=utf-8>
<script src=analytics.js></script>
<title>Hello, world.</title>
<p>...</p>

<!-- good -->
<!doctype html>
<meta charset=utf-8>
<title>Hello, world.</title>
<p>...</p>
<script src=analytics.js></script>
```

## CSS

### 分号

给每一行样式加上分号

```css
/* bad */
div {
  color: red
}

/* good */
div {
  color: red;
}
```

### 文档流

尽可能不要改变元素的默认行为

尽量让元素处于自然的文档流程中

```css
/* bad */
img {
  display: block;
}
/* good */
img {
  vertical-align: middle;
}

/* bad */
div {
  width: 100px;
  position: absolute;
  right: 0;
}
/* good */
div {
  width: 100px;
  margin-left: auto;
}
```

### 定位

在CSS中定位元素的方法有很多，多多使用现代布局规范，如Flexbox和Grid，避免从正常的文档流程中删除元素，例如使用position：absolute

### 选择器

尽量减少与DOM紧密耦合的选择器，当你的选择器超过3个结构伪类或子代或同级组合体时，考虑给你要匹配的元素添加一个类

```css
/* bad */
div:first-of-type :last-child > p ~ *

/* good */
div:first-of-type .info
```

Avoid overloading your selectors when you don't need to.

```css
/* bad */
img[src$=svg], ul > li:first-child {
  opacity: 0;
}

/* good */
[src$=svg], ul > :first-child {
  opacity: 0;
}
```

### 特殊标记

不要让样式声明和选择器难以覆盖，应尽量减少id的使用，避免使用!important

```css
/* bad */
.bar {
  color: green !important;
}
.foo {
  color: red;
}

/* good */
.foo.bar {
  color: green;
}
.foo {
  color: red;
}
```

### 重叠样式

重叠样式会让选择器和debug更难，可以的话应尽量避免重叠样式

```css
/* bad */
li {
  visibility: hidden;
}
li:first-child {
  visibility: visible;
}

/* good */
li + li {
  visibility: hidden;
}
```

### 样式的继承

不要重复声明可以被继承的样式，当多种元素需要同一种可以被继承的样式时，无需给每一种元素都加一个选择器，应该给这些元素的父元素添加一个共有样式由他们继承，如果不影响其他元素的话

```css
/* bad */
div h1, div p {
  text-shadow: 0 1px 0 #fff;
}

/* good */
div {
  text-shadow: 0 1px 0 #fff;
}
```

### 保持代码整洁

尽量多多使用简写属性

```css
/* bad */
div {
  transition: all 1s;
  top: 50%;
  margin-top: -10px;
  padding-top: 5px;
  padding-right: 10px;
  padding-bottom: 20px;
  padding-left: 10px;
}

/* good */
div {
  transition: 1s;
  top: calc(50% - 10px);
  padding: 5px 10px 20px;
}
```

### 语言

使用英语而不是数学

```css
/* bad */
:nth-child(2n + 1) {
  transform: rotate(360deg);
}

/* good */
:nth-child(odd) {
  transform: rotate(1turn);
}
```

### 浏览器前缀

积极清楚无用的浏览器前缀，如果使用浏览器前缀属性，请将他们放到标准属性的前面

```css
/* bad */
div {
  transform: scale(2);
  -webkit-transform: scale(2);
  -moz-transform: scale(2);
  -ms-transform: scale(2);
  transition: 1s;
  -webkit-transition: 1s;
  -moz-transition: 1s;
  -ms-transition: 1s;
}

/* good */
div {
  -webkit-transform: scale(2);
  transform: scale(2);
  transition: 1s;
}
```

### 动画

尽可能使用过渡而不是动画，除了opacity和transform外，避免让其他属性动画化。

```css
/* bad */
div:hover {
  animation: move 1s forwards;
}
@keyframes move {
  100% {
    margin-left: 100px;
  }
}

/* good */
div:hover {
  transition: 1s;
  transform: translateX(100px);
}
```

### 单位

+ 值为0不使用单位
+ 相对值使用rem
+ 尽可能使用s(秒)不用ms(毫秒)

### 颜色

除非你需要透明度使用`rgba`，否则总是使用十六进制rgb

```css
/* bad */
div {
  color: hsl(103, 54%, 43%);
}

/* good */
div {
  color: #5a3;
}
```

### Drawing

属性值应尽量避免HTTP请求，如果可以在css中填充的话

```css
/* bad */
div::before {
  content: url(white-circle.svg);
}

/* good */
div::before {
  content: "";/* svg图片就是文本格式，可以填充在这里*/
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #fff;
}
```

### Hacks

不要使用搞怪代码

```css
/* bad */
div {
  // position: relative;
  transform: translateZ(0);
}

/* good */
div {
  /* position: relative; */
  will-change: transform;
}
```

## JavaScript



## reference

1. [bendc/frontend-guidelines: Some HTML, CSS and JS best practices. (github.com)](https://github.com/bendc/frontend-guidelines)
2. [CSS Guidelines (2.2.5) – High-level advice and guidelines for writing sane, manageable, scalable CSS](https://cssguidelin.es/)
3. [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html)
4. [airbnb/javascript: JavaScript Style Guide (github.com)](https://github.com/airbnb/javascript)
5. [腾讯前端规范-快速上手掌握 · TGideas文档库 (qq.com)](https://tgideas.qq.com/doc/frontend/)
6. [京东前端规范-Aotu.io - 前端代码规范](https://guide.aotu.io/index.html)
7. [百度前端规范-ecomfe/spec: This repository contains the specifications. (github.com)](https://github.com/ecomfe/spec)
8. [standard/standard: 🌟 JavaScript Style Guide, with linter & automatic code fixer (github.com)](https://github.com/standard/standard)
9. [vue风格指南 — Vue.js](https://cn.vuejs.org/v2/style-guide/index.html)
10. [编码规范 by @mdo (bootcss.com)](https://codeguide.bootcss.com/)