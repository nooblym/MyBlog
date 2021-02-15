# jsp动作详解

>与JSP指令元素不同的是，JSP动作元素在请求处理阶段起作用。JSP动作元素是用XML语法写成的。
利用JSP动作可以动态地插入文件、重用JavaBean组件、把用户重定向到另外的页面、为Java插件生成HTML代码。
动作元素只有一种语法，它符合XML标准：
<jsp:action_name attribute="value" />
动作元素基本上都是预定义的函数，JSP规范定义了一系列的标准动作，它用JSP作为前缀，可用的标准动作元素如下：

语法    |描述   |补充
--------|------|----
jsp:include |在页面被请求的时候引入一个文件。|
jsp:useBean |寻找或者实例化一个JavaBean。|
jsp:setProperty |设置JavaBean的属性。|
jsp:getProperty |输出某个JavaBean的属性。|
jsp:forward |把请求转到一个新的页面。|
jsp:plugin  |根据浏览器类型为Java插件生成OBJECT或EMBED标记。|
jsp:element |定义动态XML元素|
jsp:attribute   |设置动态定义的XML元素属性。|
jsp:body    |设置动态定义的XML元素内容。|
jsp:text    |在JSP页面和文档中使用写入文本的模板|