# java异常

## 基本使用

1. 抛出异常

   ```java
   throw [exception 对象]
   ```

2. 处理异常对象

   继续向上抛出

   ```java
    void method()throws Exception{
        doSomething();		//doSometing会抛出异常
    }
   ```

   当下处理异常

   ```java
   void method(){
       try{
           
       }catch(SubException e){
           doSomething();		//doSometing会抛出异常
       }catch(Exception e){
           doSomething();		//doSometing会抛出异常
       }finally{   //finally中的代码不管有没有异常都会执行，所以一般都是资源关闭操作
           code...
       }
   }
   
   java8 新特性
   java8对finally进行增强
   void method(){
       
   }
   ```

   

### 自定义异常

- 什么出了错?
- 在哪出的错?
- 为什么出错?

自定义异常最重要的就是类名和异常类的继承关系

## 异常处理

## Q&A

#### Q:

