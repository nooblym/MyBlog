# kotlin入门

## 运算符

+ ==相当于java中的equals

+ ===比较内存地址

+ $+变量名

    ```kotlin
    //字符串模板
    var name:String = "wang"
    println("hello$name") 	//输出hellowang
    
    ```

## 变量

+ 变量：

    var variableName Type = value(不能为null)

+ 不可变变量：

    val variableName Type = value(不能为null)

+ 类型推断

    - 在声明一个变量时，我们可以不需要显示声明数据类型，kotlin 会根据你为变量赋的值动态的推导出其类型。
    - 当一个变量被赋予了某个类型的数值之后，不能再赋给他其他类型的数值，否则，会报 类型错误。

+ kotlin默认规定在声明变量的时候必须初始化，而且不能初始化为null，如果不想在声明变量的时候初始化变量，那么可以在类型后面加个"?"告诉kotlin这个变量先不赋值

    var variableName Type? = value(可以为null)

+ 一个可以为null的变量没办法直接赋值给一个同类型不能为null的变量，如果想让一个可以为null的变量赋给一个不能为null的同类型变量可以使用强制转换，在可以为null的变量后面加上两个叹号"!!"

    一个不能为null的变量可以赋给一个同类型的能为null的变量

    ```kotlin
    var str1:String = "str1"
    var str2:String?=null
    str1 = str2(报错)
    str1=str2!!
    str2 = str1
    ```

+ 

## 函数

+ 声明函数

    ```kotlin
    fun funName(varName:Type):returnType{	
        ...
    	return var
    }
    ```

+ Kotlin函数可以有默认值

    ```kotlin
    fun funName(varName:Type="defaultValue"):returnType{	
        ...
    	return var
    }
    ```

+ 当函数体只有一行时可以简写

    ```kotlin
    fun funName(varName:Type[="defaultValue"])[:returnType] = MethodBody
    ```

+ kotlin函数可以嵌套

    ```kotlin
    fun funName(varName:Type="defaultValue"):returnType{	
    
        fun subFunName(varName:Type[="defaultValue"]):returnType{	
            ...
            return var
    	}
            ...
    	return var
    }
    ```

+ 扩展函数

    

## kotlin java互调

