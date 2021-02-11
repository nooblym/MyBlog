# 记一次Spring整合Mybatis



## 1.配置jar包依赖

需要的依赖有：

mybatis：基本的mybatis运行jar包

mybatis-spring：spring整合mybatis需要使用的jar包

druid：阿里巴巴的数据库连接池，也可以使用其他的

spring-context：spirng运行环境

```xml
 <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.3</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>2.0.3</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/com.alibaba/druid -->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.1.21</version>
    </dependency>

    <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.2.1.RELEASE</version>
    </dependency>
```

## 2.配置项目环境

新建一个java项目，应该有如下包：

mapper：用于存放mapper类

bean：用于存放mybatis实体类

test：用于存放test类

还应该有以下配置文件：

applicationContext：spring配置文件

jdbc.properties：数据库配置文件

## 3. 配置spirng配置文件applicationContext.xml

1. 配置阿里巴巴数据源

    [DruidDataSource配置属性列表](https://github.com/alibaba/druid/wiki/DruidDataSource配置属性列表)

    ```xml
    <!--数据源使用阿里巴巴的druid-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="driverClassName" value="${jdbc.driver}"/>
    </bean>
    ```

2. 配置 SqlSessionFactoryBean

    在 MyBatis 的使用中，我们通过 SqlSessionFactoryBuilder 来构建一个 SqlSessionFactory 对象，而在 Spring 整合包中，我们需要使用 SqlSessionFactoryBean 来创建 SqlSessionFactory 的 Spring bean 实例

    ```xml
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <!--dataSource 是 Spring 容器管理的数据源-->
        <property name="dataSource" ref="dataSource"/>
        <!--通过configLocation属性指定mybatis核心配置文件mybatis-config.xml路径-->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
    </bean>
    ```

3. 配置MapperFactoryBean

    配置完sqlSessionFactory接下来就要配置mapperBean了

    ```xml
    <bean id="userMapper" class="org.mybatis.spring.mapper.MapperFactoryBean">
        	<!--mapperInterface配置mapper借口的全限定类名-->
          <property name="mapperInterface" value="package.MapperInterface" />
        	<!--sqlSessionFactory用于指定一个SqlSessionFactoryBean-->
          <property name="sqlSessionFactory" ref="sqlSessionFactory" />
    </bean>
    ```

4. 配置MapperScannerConfigurer

    上面的配置有一个很大的缺点，就是系统有很多的mapper配置文件时全部需要手动编写，而且维护麻烦；mybatis为我们提供了一个很好的bean--MapperScannerConfigurer，使用它没有必要在 Spring 的 XML 配置文件中注册所有的映射器，只需要配置一个 MapperScannerConfigurer , 它 将 会 查 找 类 路 径 下 的 映 射 器 并 自 动 将 它 们 创 建 成 MapperFactoryBean

    ```xml
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        	<!--可以使用分号或逗号作为分隔符设置多于一个的包路径,每个映射器将会在指定的包路径中递归地被搜索到-->
          <property name="basePackage" value="mapper包路径" />
        	<!--当只有一个sqlSessionFactory时可以不指定-->
        	<property name="sqlSessionFactoryBeanName" value="sqlSessionFactory" />
    </bean>
    ```

    MapperScannerConfigurer支持通过接口或注解过滤映射器；annotationClass 属性指定了要寻找的注解名称;markerInterface 属性指定了映射器要实现的接口。如果两者都被指定了,加入到接口中的映射器会匹配两种标准。默认情况下,这两个属性都是null,所以在基包中给定的所有接口可以作为映射器加载

## 4.测试

create table admin(id varchar(128),userid varchar(128));