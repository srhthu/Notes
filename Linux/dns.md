几个工具
- resolvconf：需要apt安装，配置dns的工具
- systemd-resolved 提供域名解析服务

参考资料
- 博客https://www.keepnight.com/archives/1772/
- 博客 https://www.modb.pro/db/330295

### systemd-resolved
配置文件
```
# /etc/systemd/resolved.conf

[Resolve]
#DNS=
#FallbackDNS=
#Domains=
#LLMNR=no
#MulticastDNS=no
#DNSSEC=no
#Cache=yes
#DNSStubListener=yes
```
```
# /run/systemd/resolve/resolv.conf

nameserver 172.18.177.130
nameserver 192.168.100.1
search comp.nus.edu.sg

# /run/systemd/resolve/resolv.conf
nameserver 127.0.0.53
options edns0
search comp.nus.edu.sg
```
`/usr/lib/systemd/resolv.conf` 这个配置文件在dgx上没有，在Ubuntu20.04的本机上有。  

在18.04以前，dns的配置应该跟`/etc/resolv.conf`有关。现在这个文件是指向resolved生成的动态dns文件的一个软连接。文件中说如果要manage resolv.conf，需要删掉这个软连接，替换为一个静态文件，或者是一个别的软连接。  

```
ls -lh /etc/resolv.conf 
lrwxrwxrwx 1 root root 39 Sep 22  2020 /etc/resolv.conf -> ../run/systemd/resolve/stub-resolv.conf
```

systemd-resolved工作模式：
- 通过127.0.0.53提供dns服务
- 退化为老版本的模式，即通过/etc/resolv.conf进行配置。


#### 配置
查看状态：`systemd-resolve --status`

>DNS服务器来自于 **全局配置文件**(/etc/systemd/resolved.conf)、 针对单个连接的**静态配置文件**(/etc/systemd/network/*.network)、 针对单个连接的**动态配置**(从DHCP或其他系统服务得到的DNS服务器)。参见 [resolved.conf(5)](http://www.jinbuguo.com/systemd/resolved.conf.html#) 与 [systemd.network(5)](http://www.jinbuguo.com/systemd/systemd.network.html#) 以了解 systemd 自身的DNS服务器配置。为了提高兼容性， 仅在 /etc/resolv.conf 不是一个指向 /run/systemd/resolve/resolv.conf 的软连接的情况下， 才会从 /etc/resolv.conf 读取全局DNS服务器。

注：这里的动态配置，我理解可能也是包含netplan里面的配置，来源于networkd

>默认情况下ubuntu16.04和ubuntu18.04系统中/etc/resolv.conf软连接指向/run/resolvconf/resolv.conf，原因是ubuntu一般会安装resolvconf去管理dns地址。resolvconf通过获取DHCP自动设置的DNS（/etc/network/interfaces或者/etc/netplan/50-cloud-init.yaml）来维护/run/resolvconf/resolv.conf从而维护整个系统默认使用的dns）。

注：此为博客的解释。不过在resolvconf未安装的情况下，不太清楚是怎么运作的

另一篇博客：
> Ubuntu的网络配置使用的是netplan，DNS使用systemd-resolved。
```
ss -lunp
State      Recv-Q      Send-Q         Local Address:Port      Peer Address:Port                                                        
UNCONN     0           0                127.0.0.53%lo:53          0.0.0.0:*      users:(("systemd-resolve",pid=50365,fd=12))      
UNCONN     0           0      172.28.176.127%enp1s0f0:68          0.0.0.0:*      users:(("systemd-network",pid=49117,fd=22)) 
```
可以看到，systemd-resolve监听53，systemd-network监听68负责DHCP。

修改`/etc/systemd/resolved.conf`来修改全局DNS