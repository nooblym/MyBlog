# Bootstrap如何禁用响应式

> 有时候我们并不需要适配屏幕小于??的设备，而bootstrap又默认有响应式，那么如何禁用它呢？

## 禁用bootstrap响应式需要以下几步

1. 移除 [此 CSS 文档](http://v3.bootcss.com/css/#overview-mobile)中提到的设置浏览器视口（viewport）的标签：`<meta>`。

2. 通过为 `.container` 类设置一个 `width` 值从而覆盖框架的默认 width 设置，例如 `width: 970px !important`

   请确保这些设置全部放在默认的 Bootstrap CSS 文件的后面。注意，如果你把它放到媒体查询中，也可以略去`!important` 

3. 如果使用了导航条，需要移除所有导航条的折叠和展开行为

4. 对于栅格布局，额外增加 `.col-xs-*` 类或替换掉 `.col-md-*` 和 `.col-lg-*`。 不要担心，针对超小屏幕设备的栅格系统能够在所有分辨率的环境下展开

## 参考链接

1. [「CSDN」Bootstrap如何禁止响应式布局 不适配](https://blog.csdn.net/weixin_30666943/article/details/94837000)

