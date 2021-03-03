# git设置http/ssh代理

## http代理

```
# http & https
# 1080 可自行切换真实代理端口

git config --global http.proxy socks5h://127.0.0.1:1080
git config --global https.proxy socks5h://127.0.0.1:1080
# 此处不一定非要是socks5h协议，sockets,http也可以
# socks5h 具备远程解析的功能，可以有效的避免 CDN 污染等问题

# 取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy

```

## ssh代理

ssh代理需要在`用户目录下/.ssh/config`文件中修改配置，默认可能没有需要创建

