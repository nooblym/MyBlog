# Spring AOP

## 使用

### 基于注解

在使用注解aop注解配置之前需要开启注解扫描，如果使用java config配置需要在config类上加上`@EnableAspectJAutoProxy`注解类启动注解扫描，如果使用xml需要加上`<aop:aspectj-autoproxy/>`开启注解扫描。

1. 定义切面类

   使用注解定义切面只需要在切面类上加上`@Aspect`注解就表明这是一个切面类，会对此类中的方法进行切面注解扫描

2. 定义通知

   只需要在切面类中的方法上加上通知注解，并在通知注解中加上pointcut表达式就可以了，例如：

   ```java
   @Aspect
   public class LogAspect {
       @Before("execution(* me.liu.bean.User.setName(..))")
       public void beforeLog(){
           System.out.println("执行之前log...");
       }
       @After("execution(* me.liu.bean.User.setName(..))")
       public void beforeLog(){
           System.out.println("执行之后log...");
       }
   }
   ```

   用`@Aspect`注解表明是一个切面类，用通知注解表明是一个通知，用pointcut表达式表明通知作用的方法；所以此切面类声明会在`me.liu.bean.User`类调用`setName`方法前后打印一些log

   **通知注解一共有5种：**

   + 前置通知（Before）：在目标方法被调用之前调用通知功能
   + 后置通知（After）：在目标方法完成之后调用通知，此时不会关心方法的输出是什么
   + 返回通知（After-returning）：在目标方法成功执行之后调用通 知
   + 异常通知（After-throwing）：在目标方法抛出异常后调用通知
   + 环绕通知（Around）：通知包裹了被通知的方法，在被通知的方法调用之前和调用之后执行自定义的行为

   pointcut表达式作用就是匹配切面作用的方法，格式为`AspectJ 指示器([返回值类型] [类全限定类名及方法名(方法参数)])`，如：`execution(* me.liu.bean.User.setName(..))`

   其中execution用于匹配模式是连接点的执行方法;*表示返回任意对象，`me.liu.bean.User`是user类的全限定类名，`setName`是方法，方法里的两个`..`表明任意参数

   **AspectJ 指示器一共有十种：**

   + arg()

     限制连接点匹配参数为指定类型的执行方法

   + @args()

     限制连接点匹配参数由指定注解标注的执行方法

   + execution()

     用于匹配是连接点的执行方法

   + this()

     限制连接点匹配AOP代理的bean引用为指定类型的类

   + target

     限制连接点匹配目标对象为指定类型的类

   + @target()

     限制连接点匹配特定的执行对象，这些对象对应的类要具有指定类 型的注解

   + within()

     限制连接点匹配指定的类型

   + @within()

     限制连接点匹配指定注解所标注的类型（当使用Spring AOP时，方 法定义在由指定的注解所标注的类里）

   + @annotation

     限定匹配带有指定注解的连接点

   

   

### 基于xml

