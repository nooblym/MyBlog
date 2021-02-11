# jsp指令详解

>JSP指令用来设置整个JSP页面相关的属性，如网页的编码方式和脚本语言。
语法格式如下：
<%@ directive attribute="value" %>指令可以有很多个属性，它们以键值对的形式存在，并用逗号隔开

## <%@ page attribute="value"... %>

属性        |描述   |补充
------------|------|-----
buffer      |指定out对象使用缓冲区的大小
autoFlush   |控制out对象的 缓存区
contentType |定当前JSP页面的MIME类型和字符编码
errorPage   |指定当JSP页面发生异常时需要转向的错误处理页面
isErrorPage |指定当前页面是否可以作为另一个JSP页面的错误处理页面
extends     |指定servlet从哪一个类继承
import      |导入要使用的Java类
info        |定义JSP页面的描述信息
isThreadSafe|指定对JSP页面的访问是否为线程安全
language    |定义JSP页面所用的脚本语言，默认是Java
session     |指定JSP页面是否使用session
isELIgnored |指定是否执行EL表达式
isScriptingEnabled |确定脚本元素能否被使用

## <%@ include attribute="value"... %>

>JSP可以通过include指令来包含其他文件。被包含的文件可以是JSP文件、HTML文件或文本文件。包含的文件就好像是该JSP文件的一部分，会被同时编译执行。

属性        |描述   |补充
------------|------|-----
file        |指定包含的文件url|

## <%@ taglib attribute="value"... %>

>JSP API允许用户自定义标签，一个自定义标签库就是自定义标签的集合。
Taglib指令引入一个自定义标签集合的定义，包括库路径、自定义标签。

属性        |描述   |补充
------------|------|-----