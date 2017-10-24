ssx
==

what's ssx
--
```
天噬:
重做了shadowsocks客户端。在协议之上加了一层http隧道
模式使用tiny语法，必须是https模式
需要类似tiny的本地免流效果，请移步首页找蛋蛋的eggproxy
```
```
小夏:
1 SSX是SSR(SS)+代理(需CONNECT通道)
2 SSR是短链接所以SSX是短链接(OP 注射器长链接)
3 SSX代理必须是CONNECT,只有CONNECT才有通道能处理所有HTTP协议请求
4 SSX免流的检测是检测客户端向代理所发送的类容
5 SSX之所以能免UDP是因为付费版加入了能将UDP转TCP的GOST(多做一次处理)
6
tiny检测为: 请求>拦截>修改>发送>检测(免不免)>代理>获取>返回

SSR检测为: 请求>拦截>修改>发送>检测(免不免)>SOCKS5>获取>返回

SSX检测为: 请求>拦截>修改>发送>检测(免不免)>代理>Socks5>获取>返回

SSX付费版检测为: udp处理(TCP依旧上面处理)
请求>拦截>修改>发送>检测(免不免)>代理>gost UDP转TCP>Socks5>返回

大概就是这样
```
tiny & ssx
```
非玩:
- tiny需要root，ssx不需要root
- tiny需要http和https免，ssx只需https免
- tiny只免tcp，目前还免不了udp，下一步想免udp估计需要redsocks、tproxy和gost配合，转udp为tcp，也需要服务器。ssx用tun2socks建立tun虚拟网卡，抓取全部封包，有可能直接实现udp over tcp
- ssx 有点类似 openvpn
- ssr免套路太简单，很多地方不免，那就可以用 ssx + tiny中移植来的https模式实现免
```
常规配置
```
服务器 你的服务器ip
端口   你的端口port
加密   chacha20
密码   你的连接密码
代理   10.0.0.172
端口   80
代码   [M] / GET wap.10086.cn\r\nHost: [H]\r\nGET / [V]\r\nHost: wap.10086.cn\r\n
```
高级
--
```
小夏:
1 SSX支持非最新版SSR！
2 如果shadowsocks服务器同https代理服务器, shadowsocks服务器可用127.0.0.1回环地址表示, 避免服务器流量双开
3 除了请求GET POST CONNECT, HEAD PUT * OPTIONS  TRACE 也可以免！
```
![ssx](http://cdn-x-c.momentcdn.net/58f8974c2bf9484f120000a0/0.43.0.0.0/yaohuo.me/bbs/upload/1000/2017/05/09/26173_2017180-309f711d3cbf488.jpg.CM_WP.webp)
![ssx](http://cdn-x-c.momentcdn.net/58f8974c2bf9484f120000a0/0.43.0.0.0/yaohuo.me/bbs/upload/1000/2017/05/09/26173_2017181-58142fa45737142c.jpg.CM_WP.webp)

小结
--
- 关键 https代理服务器
- 抓包 分析数据包
