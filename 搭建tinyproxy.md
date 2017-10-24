
如何快速搭建tinyproxy
==
安装
--
```
yum update
yum install tinyproxy
```
注意
--
1. 先尝试运行一次tinyproxy, 否则tinyproxy.conf配置文件的默认内容不会加载出来
2. 关闭防火墙或开放端口访问代理服务器, 否则访问不到服务器
```
systemctl start tinyproxy.service
```
配置
--
```
vi /etc/tinyproxy/tinyproxy.conf
```
修改配置文件内容
```
User root
Group root
Port 8080
#Allow 127.0.0.1

#其他内容保持默认
```
启动(或设置开机启动)
--
```
systemctl start tinyproxy.service
systemctl enable tinyproxy.service
```

相关命令
```
systemctl start tinyproxy.service
systemctl restart tinyproxy.service
systemctl stop tinyproxy.service
systemctl enable tinyproxy.service  //设置开机自启
```
