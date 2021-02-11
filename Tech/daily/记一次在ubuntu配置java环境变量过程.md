# 记一次在ubuntu配置java环境变量过程

## 配置

用编辑器打开`/etc/profile`文件，在文件最后添加以下内容

```bash
#set Java environment

export JAVA_HOME=[your java home path]
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$PATH

```

保存退出，用`source /etc/profile`刷新配置

## 检验

使用`java -version`,`javac`，`java`等命令检测，一般只要不出现`xxx not fount`就ok