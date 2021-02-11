# 记一次如何在ubuntu创建启动器

在`/usr/share/applications`目录下，新建一个以`.desktop`结尾的文件，用编辑器写入以下内容保存就可以了

```properties
[Desktop Entry]
Encoding=UTF-8
Version=1.0
Type=Application
Name=Android-Studio
Comment=Android-Studio
Icon=/usr/local/program/android-studio/bin/studio.png
Exec=/usr/local/program/android-studio/bin/studio.sh
Categories=Development;IDE
Terminal=false;
```

+ Name

    在应用中看到的名字

+ Comment

    对这个desktop应用的描述

+ Icon

    显示的图标路径

+ 关键字"Type"：[必选]
     关键字"Type"定义了Desktop Entry文件的类型。常见的"Type"数值是"Application"和"Link"。"Type =  Application"表示当前Desktop Entry文件指向了一个应用程序；而"Type = Link"表示当前Desktop  Entry文件指向了一个URL (Uniform Resource Locator)。

+ Exec

    打开应用执行的脚本命令

+ Categories

    此软件的分类，有可选值

+ Terminal

    执行此应用是否打开终端



## 参考

[Linux Desktop Entry 文件深入解析](https://www.ibm.com/developerworks/cn/linux/l-cn-dtef/index.html)

