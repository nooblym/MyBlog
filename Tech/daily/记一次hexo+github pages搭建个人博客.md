# 记一次hexo+github pages搭建个人博客

> 环境：
>
> ubuntu18.4

1. 开通github pages

2. 安装git

   > apt-get install git

3. 配置git

   > ```text
   > git config --global user.name "GitHub 用户名"
   > git config --global user.email "GitHub 邮箱"
   > ssh-keygen -t rsa -C "GitHub 邮箱"
   > ```

   执行完上面命令会在当前用户根目录下创建`.ssh`目录，里面存放了公匙和私匙

   使用`ssh git@github.com`检测

4. 安装node.js

   

5. 安装hexo

6. 配置hexo

   进行部署的时候,即(hexo d)不能使用root权限(用了之后就会去/root/.ssh中找密钥),会报以下错误

   > Error: [git@github.com](mailto:git@github.com): Permission denied (publickey).
   > fatal: 无法读取远程仓库。
   > 请确认您有正确的访问权限并且仓库存在。

   当报了以上错误时,不管你更新密钥还是以非root权限部署,会报另一个错误

   > FATAL Something’s wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
   > Error: EACCES: permission denied, unlink ‘/home/zx/blog/.deploy_git/archives/index.html’

   正确做法:

   1. sudo rm -rf .deploy_git
   2. hexo clean
   3. hexo g
   4. hexo d

7. 上传到github pages



参考连接

[GitHub+Hexo 搭建个人网站详细教程](https://zhuanlan.zhihu.com/p/26625249)

[使用 Hexo+GitHub 搭建个人免费博客教程（小白向）](https://zhuanlan.zhihu.com/p/60578464)

[git---如何解决The authenticity of host 'github.com (192.30.255.112)' can't be established.](https://blog.csdn.net/Wbiokr/article/details/73431199)

[npm和node升级的正确方式](https://juejin.im/post/5c09e47ee51d45721d71087d)

[Hexo之坑](https://rs11.xyz/articles/2.html)

