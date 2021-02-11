# 记一次在ubuntu解决navicat中文乱码问题

在navicat官网下载过来的navicat默认启动会出现中文乱码问题，解决方案如下：

1. 用文本编辑器打开`start_navicat`文件

2. 将export LANG="en_US.UTF-8"改为export LANG="zh_CN.UTF-8"，保存,关闭

    进行到这一步中文应该是不乱码了，打开发现英文又乱码了，这是英文选择的字体不支持英文导致的，需要把字体调成中英都支持的格式

3. "常规" "编辑器" "记录" 三个选项里都有字体设置，在右边下拉框中选择Noto Sans mono CJK SC Regular,这一个系列的字体都可以

4. 大功告成

