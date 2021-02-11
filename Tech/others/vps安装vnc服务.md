## CentOS7安装GNOME桌面

`yum groupinstall "GNOME Desktop" "Graphical Administration Tools"`

## 安装vnc服务

```

yum -y install tigervnc-server
配置
cp /lib/systemd/system/vncserver@.service /etc/systemd/system/vncserver@:1.service
设置VNC密码
vncpasswd
重启systemd
systemctl daemon-reload
设置永久开启VNC服务
systemctl enable vncserver@:1.service
启动VNC服务
systemctl start vncserver@:1.service
如遇报错：
Job for vncserver@:1.service failed because the control process exited with error code. See "systemctl status vncserver@:1.service" and "journalctl -xe" for details.
编辑/etc/systemd/system/vncserver@:1.service配置文件：
将Type=forking改为Type=simple
重新启动VNC服务
systemctl restart vncserver@:1.service
查看VNC服务状态
systemctl status vncserver@:1.service
如有Activie:failed则表示启动失败
编辑/etc/systemd/system/vncserver@:1.service配置文件：
将里面所有的<USER>替换为当前用户名(大致有两处)，如root；另，如果是root用户，应将PIDFile的/home/root改为/root
重新启动VNC服务
systemctl restart vncserver@:1.service
```

### 开启防火墙端口

1、如果使用iptables文件，即有/etc/sysconfig/iptables
则通过如下命令添加防火墙策略：
```
 iptables -A INPUT -p tcp --dport 5801 -j ACCEPT
 iptables -A INPUT -p tcp --dport 5901 -j ACCEPT
 iptables -A INPUT -p tcp --dport 6001 -j ACCEPT
```
保存并重启

 service iptables save

重启防火墙:

 systemctl enable iptables
 service iptables restart

2、如果使用CentOS默认防火墙（本文采用）
 firewall-cmd --permanent --add-service vnc-server

 systemctl restart firewalld.service