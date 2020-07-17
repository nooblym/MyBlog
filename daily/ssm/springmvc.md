# Spring mvc配置

## 初始化

使用springmvc需要在web.xml配置文件中注册全端控制器

```xml
 <!-- 配置前端控制器DispatcherServlet -->
    <servlet>
        <servlet-name>springmvc</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!-- 初始applicationContext.xml:applicationContext.xml配置文件也可以使用<init-param>标签在servlet标签中进行配置 -->
        <init-param>
            <!-- 配置spring文件 -->
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:spring/applicationContext.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>

    <!-- 配置请求地址拦截url -->
    <servlet-mapping>
        <servlet-name>springmvc</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
```

## 基于java配置

## 基于xml配置

## 基于注解