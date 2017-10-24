centos7配置iptables防火墙
==
停用自带防火墙firewalld
--
```
systemctl stop firewalld
systemctl disable firewalld
systemctl status firewalld  //查看是否关闭
```
安装防火墙iptables
--
```
yum install -y iptables
yum install iptables-services  //腾讯云默认没有安装
```
设置&保存
```
iptables -I INPUT -p tcp --dport 8080 -j ACCEPT //开放端口8080
service iptables save
```
启动
```
systemctl enable iptables
systemctl start iptables
systemctl status iptables
```
