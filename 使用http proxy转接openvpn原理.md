OpenVPN本身可以使用http代理.

这种情况下, OpenVPN客户端不是直接和OpenVPN服务器连接，而是使用http代理进行连接. 这个特性是OpenVPN的外围特性，不是其核心的，然而却能解决很多实际问题，它相当于隧道外面又套了一个隧道，不过这个外面的隧道并不是真实的隧道，因为它并没有封装，**仅仅是伪装端口信息** , 它还是使用http代理服务器的connect方法的。

具体流程就是：
1. OpenVPN客户端连接http代理服务器(CONNECT方法)；
2. http代理服务器连接OpenVPN服务器；
3. http代理服务器在OpenVPN客户端和OpenVPN服务器之间中转数据。

为什么要使用http代理连接OpenVPN服务器呢？一般是为了对付防火墙的封堵; 其次一般很容易在公网上找到http代理服务器，且该http代理支持CONNECT方法。这样的话，所有的OpenVPN的数据全部被伪装到了代理服务器的端口，成功绕过防火墙。一般而言，http的80端口或者https的443端口是不被封锁的。

使用http代理服务器唯一的副作用就是，OpenVPN服务器将得不到OpenVPN客户端的真实IP地址，所看到的只是http代理服务器的IP地址，这对于管理接口而言很不方便，也不便于根据用户IP设置策略。

使用http代理的方式及其简单，那就是在OpenVPN客户端配置文件中加入一行：
```
http-proxy 代理ip 代理port
```
