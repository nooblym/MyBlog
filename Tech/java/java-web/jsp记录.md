# jsp记录

## jsp语法

- <%! [声明代码] %>:声明成员变量，成员方法，在翻译后的[jsp_name]_jsp.java中位于成员块，在声明块中不能使用内置对象。
- <% 代码片段 %>：代码片段中翻译后在  public void _jspService(final HttpServletRequest request, final HttpServletResponse response){
    [代码片段]
}
在这里可以使用jsp内置对象

- <%= 表达式 %>：表达式必须有返回值
- <%-- 这里可以填写 JSP 注释 --%>
- <%@ directive attribute="value" %>：[jsp指令详解](jsp指令详解.md)
- <jsp:action_name attribute="value" />[jsp动作详解](jsp动作详解.md)