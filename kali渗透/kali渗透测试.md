# KaliLinux渗透测试

## 1.配置IP地址

### 1.1临时配置IP地址

重启以后就没了

1. dhclient eth0

   自动从DHCP中获取一个IP地址

2. ifconfig eth0 指定的IP地址/掩码(通常为24(位)) 例如：ifconfig eth0 192.168.1.111/24

   指定一个IP地址

3. route add default gw 网关地址(例如：192.168.1.1)

   指定网关

```asdqw```